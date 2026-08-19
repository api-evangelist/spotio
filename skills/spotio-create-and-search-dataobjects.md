---
name: Create, search and page SPOTIO DataObjects
description: Create a lead/prospect record as a SPOTIO DataObject with the correct typeId, stageId and fieldId values, then search and page the collection using the scrollId cursor.
api: openapi/spotio-dataobjects-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json + https://developer.spotio2.com/docs/spotio2/s12ejhvxsb6hf-creating-data-objects
operations:
  - POST /api/DataObjects
  - GET /api/DataObjects/{dataObjectId}
  - DELETE /api/DataObjects/{dataObjectId}
  - PATCH /api/DataObjects/{dataObjectId}/jsonp
  - GET /api/DataObjects/many
  - GET /api/DataObjects/{dataObjectId}/duplicatesByAddress
  - GET /api/DataObjectsSearch/simple
  - GET /api/DataObjectsSearch
  - GET /api/workflow/dataObjects/full
---

# Create, search and page SPOTIO DataObjects

Run **spotio-authenticate-and-read-workflow** first. You cannot write a DataObject
without the tenant's `typeId`, `stageId` and `fieldId` values.

## Create

`POST /api/DataObjects`

```json
{
  "dataObject": {
    "fields": [
      { "fieldId": "100004", "value": "Peju Winery" },
      { "fieldId": "20", "value": "Custom Text" }
    ],
    "pin": { "address": "8466 St. Helena Hwy, Rutherford, CA 94573" },
    "stageId": "1",
    "ownerId": "534624",
    "typeId": "1"
  }
}
```

Rules taken from SPOTIO's own guide:

- `typeId` is **required**.
- `pin.address` is what geocodes the record; SPOTIO resolves it into `lat`, `lng`,
  `placeId` and a normalised address on the response.
- `ownerId` defaults to the user who created the API key. `stageId` defaults to `"1"`.
  **Set both explicitly** rather than relying on the defaults - the default owner is a
  service account and is rarely the rep who should own the lead.
- Field values are addressed by `fieldId`, resolved from
  `GET /api/workflow/dataObjects/full`. Field *names* are never accepted.
- The returned `dataObject.id` is a 24-character hex string, not an integer.

Related shapes:

- `POST /api/DataObjects/withChildren` when the record has child records.
- `POST /api/DataObjects/move` to reassign records.
- `GET /api/DataObjects/{dataObjectId}/duplicatesByAddress` before creating, if the
  source data is dirty - this is the closest thing SPOTIO has to a dedupe check.

## Update

`PATCH /api/DataObjects/{dataObjectId}/jsonp` accepts JSON Patch
(`application/json-patch+json`) or merge-patch (`application/merge-patch+json`).

Use `PATCH /api/DataObjects/{dataObjectId}/jsonp/withActivity` when the change should
also be recorded as a logged activity on the record's timeline - that is usually what a
field-sales workflow wants.

If you use `PUT` semantics anywhere else in SPOTIO, remember: **`PUT` bodies must carry
the complete resource**. DataObjects are the documented exception - a missing top-level
key is not treated as a deletion.

## Search and page

`GET /api/DataObjectsSearch/simple?q=Tire`

```json
{
  "scrollId": "lXTD",
  "totalCount": 223,
  "items": [ { "navigationId": "...", "id": "...", "typeId": "1", "name": "Randy's Discount Tires" } ]
}
```

Paging contract:

1. Issue the first request with no `scrollId`.
2. Re-issue the same request with `scrollId=<returned value>`.
3. Stop when `scrollId` comes back `null`. That, not an empty `items` array, is the
   end-of-collection signal.
4. `perPage` overrides page size where the operation declares it (5 operations do).

`GET /api/DataObjectsSearch` is the richer search; `POST` variants of both accept a
body instead of query parameters when the query is too large for a URL.

**Never loop for a cursor on Stages, Custom Fields, Activity Templates or Users** -
SPOTIO documents these four as unpaginated, returning everything in one response.

## Filtering a collection

Filters are persisted objects, not inline query parameters. Create one, then pass its id:

- `POST /api/v2/filters` with `{ "title": "...", "startDate": "...", "endDate": "...", "dataObjectTypeIds": ["1"] }`
- pass `filterId=<id>` on any operation that declares it (43 do)
- `GET /api/Filters` lists existing filters; `GET /api/v2/filters/options` lists what can be filtered on

## Delete

`DELETE /api/DataObjects/{dataObjectId}`. Deleted records remain readable through
`GET /api/DataObjects/deleted`.

## Failure modes

- `422` with `{"errors": {"stageId": "Stage with id: 3 does not exist."}}` - your cached
  workflow is stale. Re-read `GET /api/workflow/dataObjects/full`.
- On large writes you may supply a `fieldTempId` per field; SPOTIO echoes it back as the
  error key so a message can be bound to the exact input that failed.
- No idempotency key exists. A retried `POST /api/DataObjects` creates a duplicate.
  Set `externalDataObjectId` to your own primary key so a duplicate is at least
  detectable afterwards.
