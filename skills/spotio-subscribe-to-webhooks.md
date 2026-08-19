---
name: Subscribe to SPOTIO webhooks and verify deliveries
description: Register an outbound webhook endpoint, discover the available scopes, verify the X-Signature HMAC, and handle SPOTIO's retry and timeout behaviour. Covers all 10 published events.
api: openapi/spotio-webhooks-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json + https://support.spotio.com/hc/en-us/articles/360057063834-Webhooks
operations:
  - GET /api/Webhooks/scopes
  - GET /api/Webhooks
  - POST /api/Webhooks
  - PUT /api/Webhooks/{id}
  - DELETE /api/Webhooks/{id}
---

# Subscribe to SPOTIO webhooks and verify deliveries

Run **spotio-authenticate-and-read-workflow** first. Webhook management is authenticated
with the same bearer token.

## Step 1 - discover the scopes

`GET /api/Webhooks/scopes` returns the subscribable scopes as an array of strings.

**Call this rather than hard-coding.** SPOTIO's OpenAPI declares the response as an
untyped `array of string` with no enum, so the authoritative vocabulary exists only at
runtime. The knowledge base documents ten events, which is the set to expect:

| Entity | Events |
|---|---|
| Lead (a DataObject of the tenant's lead type) | `lead.added`, `lead.updated`, `lead.deleted` |
| Activity | `activity.created`, `activity.updated`, `activity.deleted`, `activity.done` |
| Appointment | `appointment.created`, `appointment.updated`, `appointment.deleted` |

Note the vocabulary mismatch: the events say **lead**, the API says **DataObject**.
Resolve `data` back through `GET /api/DataObjects/{dataObjectId}` if you need the full
record with its custom fields.

## Step 2 - create the subscription

`POST /api/Webhooks` with a `NewWebhookDto`. The endpoint object carries:

| Field | Purpose |
|---|---|
| `callback` | your HTTPS receiver URL |
| `scopes` | the events to subscribe |
| `active` | enable/disable without deleting |
| `customHeaders` | headers SPOTIO adds to each delivery (use for your own routing/auth) |

`GET /api/Webhooks` lists the company's endpoints, `PUT /api/Webhooks/{id}` updates one,
`DELETE /api/Webhooks/{id}` removes it.

## Step 3 - handle the delivery

SPOTIO POSTs a **batched** envelope:

```json
{
  "payload": [
    { "data": { }, "type": "lead.updated", "date": "2026-08-13T14:02:11Z" }
  ]
}
```

`payload` is an array - always iterate it, never assume one event per request.
`data`'s shape depends on `type` and is **not published per event**; there is no
AsyncAPI document and no per-event schema, so treat `data` defensively and re-read the
entity by id when you need a guaranteed shape.

## Step 4 - verify the signature

Every request carries `X-Signature`: a **hex-encoded HMAC-SHA256 of the raw request
body**, keyed with your secret. Compute over the raw bytes before JSON parsing, and
compare in constant time. Reject anything that does not match.

## Step 5 - respond correctly

- Return **200**. Any other status is treated as a failure.
- SPOTIO retries **up to 3 times with increasing intervals**.
- Each delivery **times out after 10 seconds**. SPOTIO's explicit guidance is to process
  asynchronously: acknowledge fast, queue the work.
- Deliveries are at-least-once by construction (retries with no idempotency key), so
  make your handler idempotent on your side - key off `type` + `date` + the entity id.

## Realtime alternative

SPOTIO's developer Introduction states: *"You can use HTTP webhooks or Ably realtime
events to achieve this functionality."* No channel names, token endpoint, connection
guide or schema for the Ably surface is published anywhere on the developer portal or
knowledge base as of 2026-08-13. Do not build against it from inference - ask SPOTIO
support for the channel contract first.
