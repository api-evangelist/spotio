---
name: Authenticate to SPOTIO and read the tenant workflow
description: Mint a SPOTIO bearer token and load the tenant's DataObject workflow (types, stages, field ids) before attempting any read or write. This is the mandatory first step for every other SPOTIO skill.
api: openapi/spotio-workflowsettings-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json + https://developer.spotio2.com/docs/spotio2/3f682d2s8ezln-authenticating-to-the-rest-api
operations:
  - POST /api/users/apitoken
  - GET /api/workflow/dataObjects/full
  - GET /api/BusinessCards
---

# Authenticate to SPOTIO and read the tenant workflow

SPOTIO's OpenAPI declares **no `operationId` on any of its 295 operations**, so every
step below is bound to a verified `METHOD` + path from the published document. Do not
substitute an invented operationId.

## Preconditions

- A SPOTIO subscription. There is no free tier and no self-serve sandbox.
- A `clientId` and `secret` pair, created by a SPOTIO **Admin** in the web app under
  `Settings -> Integrations -> API Access`. The secret is shown once and cannot be
  retrieved afterwards.
- Base URL `https://api.spotio2.com`. All traffic is HTTPS, JSON only.

## Step 1 - mint a bearer token

`POST /api/users/apitoken` with `Content-Type: application/merge-patch+json`:

```json
{ "clientId": "YOUR_CLIENT_ID", "secret": "YOUR_SECRET_KEY" }
```

Take `accessToken` from the response and send it as `Authorization: Bearer <token>` on
every subsequent call.

**Token rules that matter operationally:**

- Tokens are valid for **30 days**, then revoked; an expired token returns `401`.
- The key inherits the **role and privileges of the user account that created it**. If
  that user is suspended, the integration loses access. Mint production keys under an
  account that will not be deactivated.
- Cache the token and its issue time; re-mint on `401` rather than on every request.

## Step 2 - verify the token

`GET /api/BusinessCards` is the cheapest authenticated read and is the call SPOTIO's own
quickstart uses. A `200` proves the token works.

## Step 3 - load the workflow (do not skip this)

`GET /api/workflow/dataObjects/full`

This returns the tenant's entire schema: DataObject **types** (`typeId`), **stages**
(`stageId`) and every **field** with its numeric `id`. SPOTIO has no fixed Lead entity -
a lead is a DataObject of a tenant-defined type, and writes address fields by
`fieldId`, never by field name.

Per-type field detail, including `stageConstraints`, `systemRole` and select options:

`GET /api/workflow/dataObjects/{dataObjectId}/fields`

Cache the workflow. Re-read it when a write fails validation with an unknown
`fieldId` or `stageId`, because an admin can change the schema at any time.

## What you now know

- `typeId` values you may create.
- `stageId` values valid for each type, and which fields each stage constrains.
- `fieldId` for every system field (high-numbered, e.g. `100004` Company,
  `100013` Last Name) and every tenant custom field (low-numbered).

## Error handling

| Status | Meaning | Do |
|---|---|---|
| 400 | Malformed JSON body | Validate the JSON; SPOTIO accepts JSON only |
| 401 | Token missing, expired or revoked | Re-mint at `POST /api/users/apitoken`, retry once |
| 403 | The key's user role lacks this operation | Re-mint under an Admin account |
| 422 | Validation failure | Read the `errors` object; keys are field names |

The error envelope is `{"errors": {"<field>": "<message>"}}` - **not** RFC 9457
problem+json. Entity-level failures use the key `_`.

## Retry discipline

SPOTIO publishes **no idempotency mechanism and no rate limits**. There is no
`Idempotency-Key`, no `429`, and no `Retry-After`. Never blind-retry a write: a repeated
`POST /api/DataObjects` creates a second record. Retry reads freely; for writes,
re-read before retrying, or use `externalDataObjectId` to detect a record you already
created.
