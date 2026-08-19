---
name: Manage SPOTIO territories, reps and teams
description: Create and read sales territories (including GeoJSON boundaries), manage users and teams, and log the field activity and appointments that hang off them.
api: openapi/spotio-territories-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json
operations:
  - GET /api/Territories/all
  - POST /api/Territories
  - GET /api/Territories/{id}
  - PUT /api/Territories/{id}
  - GET /api/Territories/{id}/geojson
  - GET /api/users
  - POST /api/Users
  - POST /api/v2/activities
  - POST /api/v2/appointments
---

# Manage SPOTIO territories, reps and teams

Run **spotio-authenticate-and-read-workflow** first. Most operations here require an
Admin-privileged key, because the API key inherits the creating user's role.

## Territories

| Action | Call |
|---|---|
| List all | `GET /api/Territories/all` |
| Read one | `GET /api/Territories/{id}` |
| Create | `POST /api/Territories` |
| Update | `PUT /api/Territories/{id}` |
| Boundary as GeoJSON | `GET /api/Territories/{id}/geojson` |

`GET /api/Territories/{id}/geojson` is the interoperability seam - it hands you an
RFC 7946 geometry you can drop straight into a map, a PostGIS table or a spatial join
against your own coverage data. It is the only standards-shaped payload in the whole
SPOTIO API.

`PUT` here means **complete resource**: SPOTIO's convention is that a PUT body carries
every field. Read the territory first, mutate, then write it back whole. The DataObject
partial-update exception does not apply.

There is no delete operation for a territory in the published document.

## Users and teams

- `GET /api/users` - list users. **This collection is not paginated**; SPOTIO returns
  every user in one response. Do not loop for a `scrollId`.
- `POST /api/Users` - create a user.
- `GET /api/users/list` - **deprecated**. It is the only operation in the entire
  295-operation document flagged `deprecated: true`, and SPOTIO names no replacement and
  publishes no sunset date. Move to `GET /api/users`.
- Teams live under the `Teams` capability (`openapi/spotio-teams-api-openapi.yml`,
  10 operations) and carry the hierarchy that drives leaderboards and territory
  permissions.

## Activity and appointments

Field work is recorded against a DataObject:

- `POST /api/v2/activities` - log a visit, call, note or stage change. The V2 path and
  `/api/ActivitiesV2` both exist and SPOTIO describes such pairs as interchangeable;
  prefer the `/api/v2/...` form for new work.
- `POST /api/v2/appointments` - schedule an appointment against a record and a rep.
  `POST /api/v2/appointments/bulk/create` and `/api/v2/appointments/multiple` handle
  volume.
- `GET /api/DataObjects/{dataObjectId}/appointments/upcoming` reads a record's forward
  schedule.

Each of these emits a webhook (`activity.*`, `appointment.*`) if a subscription exists -
see **spotio-subscribe-to-webhooks**.

## Routes, trips and tracking

- `RoutesV2` (8 ops) plans a rep's stops; `TripsV2` (11) and `Trips` (7) record what was
  actually visited. SPOTIO's own description: *"Trips are created from routes and record
  places that user visited during the trip."*
- `UserTracking` (5 ops) exposes rep location.
- `GET /api/Trips/{id}/export/pdf` and `/csv` export a trip directly, without the
  submit-then-poll export lifecycle.

## Cautions

- Territory geometry and rep location are **personal and operational data**. SPOTIO is
  SOC 2 Type II certified and offers EU data residency; whatever you build inherits the
  handling obligations, not the certification.
- No rate limits are published. When importing many territories or users, batch and
  pace rather than waiting for a `429` that SPOTIO never sends.
