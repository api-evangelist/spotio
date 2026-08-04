# SPOTIO (spotio)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

SPOTIO is a field sales engagement and territory management platform for outside sales teams - lead and prospect tracking, activity logging, territory mapping and assignment, route optimization, appointment setting, and pipeline visibility - delivered through a mobile-first field app and a web console.

For custom integrations beyond its native Salesforce, HubSpot, Microsoft Dynamics 365, Pipedrive, and Zapier connectors, SPOTIO publishes a documented **Open REST API** and **outbound webhooks**.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/spotio/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/spotio/refs/heads/main/apis.yml)

## Access Model (read this first)

SPOTIO's API is **real and documented, but not fully self-serve**:

- The developer portal at [developer.spotio2.com](https://developer.spotio2.com/) (hosted on Stoplight) documents a REST Open API with a curl quickstart and token authentication.
- The full endpoint reference is oriented toward enterprise customers with an API key; the exact REST path surface is **not publicly extractable** from unauthenticated pages.
- API and webhook access is an entitlement of the SPOTIO SaaS subscription (most associated with the higher Pro / Enterprise tiers for custom integrations), **not** a separately metered, sign-up-and-go API product.
- SPOTIO also documents [outbound webhooks](https://support.spotio.com/hc/en-us/articles/360057063834-Webhooks) that POST signed (HMAC-SHA256, `X-Signature`) event payloads to a customer endpoint.

Because of this, the APIs listed below are **honestly modeled** from SPOTIO's documented product surface and its public webhook event catalog rather than from a published OpenAPI definition. Leads, Activities, and Appointments are directly evidenced by webhook events; Territories, Users/Reps, and Pipelines/Data Objects are core documented product features inferred to have API coverage. No `openapi/` artifact was created and no exact endpoint paths were fabricated. See `review.yml` for details (`endpointsModeled: true`).

## Tags

- Field Sales
- Sales Engagement
- Territory Management
- CRM
- Lead Tracking
- Outside Sales
- Sales Enablement

## Timestamps

- **Created:** 2026-07-04
- **Modified:** 2026-07-04

## APIs (modeled)

### SPOTIO Leads API

Create, read, update, and delete leads and prospects, including custom data-object fields, stages, and location. Confirmed by webhook events `lead.added`, `lead.updated`, `lead.deleted`.

### SPOTIO Activities API

Log and retrieve rep activities - visits, calls, notes, and stage changes. Confirmed by webhook events `activity.created`, `activity.updated`, `activity.deleted`, `activity.done`.

### SPOTIO Appointments API

Schedule and manage field appointments tied to leads and reps. Confirmed by webhook events `appointment.created`, `appointment.updated`, `appointment.deleted`.

### SPOTIO Territories API

Define and manage sales territories - geographic boundaries, coverage, and rep assignment. Modeled from the documented product surface.

### SPOTIO Users & Reps API

Manage users and field reps - roles, team membership, and territory assignment. Modeled from the documented product surface.

### SPOTIO Pipelines & Data Objects API

Read and configure pipelines, stages, and custom [data objects](https://support.spotio.com/hc/en-us/articles/11712242070807-Configuring-Data-Objects) that structure how leads move through a sales process. Modeled from the documented product surface.

## Webhook Events (documented)

`lead.added`, `lead.updated`, `lead.deleted`, `activity.created`, `activity.updated`, `activity.deleted`, `activity.done`, `appointment.created`, `appointment.updated`, `appointment.deleted`

Payloads are signed with an HMAC-SHA256 `X-Signature` header, retried up to three times, time out after 10 seconds, and expect an HTTP 200 response.

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/spotio)
- [Website](https://spotio.com)
- [Documentation](https://developer.spotio2.com/)
- [Webhooks](https://support.spotio.com/hc/en-us/articles/360057063834-Webhooks)
- [Integrations](https://spotio.com/integrations/)
- [Plans](plans/spotio-plans-pricing.yml)

## Pricing

Per-user SaaS subscription with a five-user minimum and annual/quarterly billing (custom quote typical). Publicly reported approximate tiers: Team ~$39/user/mo, Business ~$69/user/mo, Pro ~$129/user/mo, and a custom Enterprise tier. See `plans/spotio-plans-pricing.yml`. Figures come from third-party pricing directories and should be reconciled against a current SPOTIO quote.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
