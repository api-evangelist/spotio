---
name: Bulk import DataObjects and export to CSV
description: Move records in and out of SPOTIO at volume - the NDJSON bulk-job lifecycle for writes, and the submit-then-poll export lifecycle for reads. Both are asynchronous and neither is idempotent.
api: openapi/spotio-dataobjectsbulkjobs-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json + https://developer.spotio2.com/docs/spotio2/8zeggtfnhfk9t-working-with-bulk-jobs
operations:
  - POST /api/jobs/dataObjects/bulk
  - PUT /api/jobs/dataObjects/bulk/{id}/data
  - POST /api/jobs/dataObjects/bulk/{id}/start
  - GET /api/jobs/dataObjects/bulk/{id}/progress
  - GET /api/jobs/dataObjects/bulk/{id}/results/succeeded
  - GET /api/jobs/dataObjects/bulk/{id}/results/failed
  - DELETE /api/jobs/dataObjects/bulk/{id}/cleanup
  - GET /api/jobs/dataObjects/bulk/inprogress
  - POST /api/Exports/dataObjects
  - POST /api/Exports/activities
  - GET /api/Exports/dataObjects/data
---

# Bulk import DataObjects and export to CSV

Run **spotio-authenticate-and-read-workflow** first - bulk writes address fields by
`fieldId` exactly like single writes.

SPOTIO's stated reason this surface exists: *"Instead of making individual API calls for
each record, you can batch thousands of records into a single job."* With no published
rate limits and no idempotency, batching is also the safest way to move volume.

## Import - the six-step bulk job

1. **Create** - `POST /api/jobs/dataObjects/bulk`, naming the DataObject type and the
   operation. Returns a job id. Job state is now `Open`.
2. **Upload** - `PUT /api/jobs/dataObjects/bulk/{id}/data` with an **NDJSON** file: one
   JSON object per line, each a `BulkDataObjectRequest`:

   ```json
   {"id":null,"typeId":1,"stageId":1,"ownerId":534624,"externalDataObjectId":"crm-8821","pin":{"address":"..."},"fields":[{"fieldId":"100004","value":"Peju Winery"}]}
   ```

   Multiple files may be uploaded to one job. File state moves `Uploaded -> Processing
   -> Processed` (or `Failed`).
3. **Start** - `POST /api/jobs/dataObjects/bulk/{id}/start`. This locks the job against
   further uploads; state becomes `UploadComplete`.
4. **Poll** - `GET /api/jobs/dataObjects/bulk/{id}/progress` for processed and failed
   counts. State walks `InProgress -> Ingested -> JobComplete`.
5. **Download results** -
   `GET /api/jobs/dataObjects/bulk/{id}/results/succeeded` and
   `GET /api/jobs/dataObjects/bulk/{id}/results/failed`.
   **Always read the failed file.** `JobComplete` means the job finished, not that every
   record landed - SPOTIO's own definition is *"All records were processed (some may
   have failed)"*.
6. **Clean up** - `DELETE /api/jobs/dataObjects/bulk/{id}/cleanup` to release
   server-side resources.

`GET /api/jobs/dataObjects/bulk/inprogress` lists jobs still running - check it before
submitting another large job, and to recover state after a crash.

### The `id` field decides create vs update

Line-level `id` refers to the **SPOTIO DataObject id**. Supply it to update an existing
record; leave it null to create. Carry your own key in `externalDataObjectId` so a
re-run is reconcilable - it is the only duplicate-detection handle SPOTIO gives you,
because there is no `Idempotency-Key` anywhere in this API.

### Terminal states

| State | Meaning | Do |
|---|---|---|
| `JobComplete` | Finished; some records may have failed | Download both result files |
| `Failed` | Critical error, e.g. malformed NDJSON | Fix the file, create a new job |
| `Aborted` | Cleaned up before or during processing | Re-create |

## Export - submit then poll

1. `POST /api/Exports/dataObjects` with at minimum:

   ```json
   { "reportType": "current", "singleType": 1 }
   ```

   `reportType` is `"current"` or `"historical"`. Pass `filterId` to scope the export.
   The response carries `id` and `state: "preparing"`.

2. Poll the export by id until `state` is `"ready"`, at which point `url` holds the
   CSV download link.

   **Documentation divergence, verified 2026-08-13:** the Working with Exports guide
   tells you to poll `GET https://api.spotio2.com/api/exports/{export_id}`, but no such
   path exists in SPOTIO's own published OpenAPI - the document declares
   `GET /api/Exports/dataObjects/data` and nothing matching `/api/Exports/{id}`.
   Treat the guide's path as the operational instruction (it is SPOTIO's own worked
   example) but expect the spec not to describe it, and confirm against a live tenant
   before building a poller on it.

3. Download the CSV from `url` before it expires.

Activity exports use the same pattern via `POST /api/Exports/activities`,
`POST /api/Exports/activities/data` and `POST /api/Exports/activities/data/flexible`.

## Operational notes

- No poll interval is published. Use a few seconds with backoff; SPOTIO says generation
  "may take a few seconds".
- No rate limits and no `429` are documented, so there is no signal to back off on -
  pace yourself rather than waiting to be told.
- Errors follow the standard envelope: `{"errors": {"<field>": "<message>"}}`.
