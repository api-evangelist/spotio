# SPOTIO

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

SPOTIO is a field sales engagement and territory management platform for outside sales teams - lead and prospect tracking, activity logging, territory mapping and assignment, route optimization, appointment setting, and pipeline visibility, delivered through a mobile-first field app and a web console. Behind that product is a substantial and genuinely public API: SPOTIO 2.0 is an OpenAPI 3.0.1 contract of 238 paths and 295 operations across 39 capabilities, published from SPOTIO's own Stoplight project at developer.spotio2.com and exportable without authentication. Authentication is a bearer JWT minted from a clientId/secret pair; collections page on a scrollId cursor; and SPOTIO's data model is polymorphic - there is no fixed Lead entity, only a tenant-defined DataObject whose types, stages and fields are read from a Workflow before anything can be written. SPOTIO also operates a first-party remote MCP server at app.spotio2.com/mcp, authenticated with a SPOTIO-MCP-KEY that the API itself mints, plus a signed outbound webhook system covering ten lead, activity and appointment events. It publishes no SDK in any language, no idempotency contract, no rate limits and no security.txt.

**Areas:** Field Sales · Sales Engagement · Territory Management · CRM · Lead Tracking · Outside Sales · Sales Enablement · Route Optimization · Geospatial · Webhook · MCP · Door to Door

## SPOTIO on APIs.io

Everything profiled for SPOTIO is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/spotio/](https://apis.io/providers/spotio/)** — or go straight to one of the APIs or properties below.

### APIs (39)

- [SPOTIO Activities V2 API](https://apis.io/apis/spotio/spotio-activitiesv2-api/) — The controller is responsible for handling the creation, updating, and retrieval of activities. Mainly the controller allow to manage activities (current…
- [SPOTIO Appointments V2 API](https://apis.io/apis/spotio/spotio-appointmentsv2-api/) — The controller is responsible for handling the creation, updating, deleting and retrieval of appointment. Mainly the controller allow to manage appointment…
- [SPOTIO Autoplays API](https://apis.io/apis/spotio/spotio-autoplays-api/) — The controller provides various endpoints for managing autoplays, which are automated workflows that can be triggered for dataObject in application. Allowed…
- [SPOTIO Business Cards API](https://apis.io/apis/spotio/spotio-businesscards-api/) — The Business Cards API allows managing business card and their related operations, such as fetching details, listing, creating, updating, cloning, sharing,…
- [SPOTIO Calendar Settings API](https://apis.io/apis/spotio/spotio-calendarsettings-api/) — The controller is responsible for managing calendar settings. Setup for company users calendar.
- [SPOTIO Communication API](https://apis.io/apis/spotio/spotio-communication-api/) — API for communication activities. You can retrieve data about communication activities. You can also marks calls, emails, texts as seen/read.
- [SPOTIO Connectors API](https://apis.io/apis/spotio/spotio-connectors-api/) — The controller is responsible for managing company links (connectors). The controller allows creating new connectors which user can use them on web or…
- [SPOTIO Contracts API](https://apis.io/apis/spotio/spotio-contracts-api/) — The controller is responsible for gets information about contracts templates and signed documents / files.
- [SPOTIO Data Objects API](https://apis.io/apis/spotio/spotio-dataobjects-api/) — The controller is responsible for manages the data objects and their related operations like creating, retrieving, updating, and deleting data objects, as…
- [SPOTIO Data Objects Bulk Jobs API](https://apis.io/apis/spotio/spotio-dataobjectsbulkjobs-api/) — Bulk operations on data objects. Flow: Create job -> Upload NDJSON data -> Start processing -> Poll progress -> Download results -> Cleanup.
- [SPOTIO Data Objects Search API](https://apis.io/apis/spotio/spotio-dataobjectssearch-api/) — This controller is responsible for searching data objects. There are available endpoints for: * simple global searches - return only basic information about…
- [SPOTIO Documents API](https://apis.io/apis/spotio/spotio-documents-api/) — The controller is responsible for handling the upload and retrieval of documents. Documents can be attached to data object, activity or be available company…
- [SPOTIO Exports API](https://apis.io/apis/spotio/spotio-exports-api/) — The controller is responsible for exporting data from the application, such as exporting dataObjects (leads) and activities. The result of the export is a…
- [SPOTIO Filters API](https://apis.io/apis/spotio/spotio-filters-api/) — The controller is responsible for handling operations on filter objects. Filter can be used throughout the system to filter data. It can be passed wherever…
- [SPOTIO Generate Content API](https://apis.io/apis/spotio/spotio-generatecontent-api/) — The controller is responsible for content generating for text messages and emails.
- [SPOTIO Layouts API](https://apis.io/apis/spotio/spotio-layouts-api/) — The Layouts API from SPOTIO — 8 operation(s) for layouts.
- [SPOTIO Leaderboards API](https://apis.io/apis/spotio/spotio-leaderboards-api/) — The controller is responsible for leaderboards.
- [SPOTIO MCP API](https://apis.io/apis/spotio/spotio-mcp-api/) — The controller is responsible for handling operations related to MCP. It provides endpoints for generating, retrieving, deactivating, and regenerating MCP…
- [SPOTIO Multi Channel Communication API](https://apis.io/apis/spotio/spotio-multichannelcommunication-api/) — The controller is responsible for text messages management. Sending messages to customers
- [SPOTIO My Reports API](https://apis.io/apis/spotio/spotio-myreports-api/) — The controller is responsible for managing MyReports in a web application, creation, updating and rendering MyReports.
- [SPOTIO Notifications V2 API](https://apis.io/apis/spotio/spotio-notificationsv2-api/) — The controller is responsible for handling operations on notification objects. Notifications are created automatically when creating appointments with…
- [SPOTIO Pins V2 API](https://apis.io/apis/spotio/spotio-pinsv2-api/) — Pins API handles searching and retrieving pins with details. It provides operations including fetching pins by viewport, getting pin details with data…
- [SPOTIO Reports API](https://apis.io/apis/spotio/spotio-reports-api/) — The controller is responsible exporting data by selected report type.
- [SPOTIO Routes V2 API](https://apis.io/apis/spotio/spotio-routesv2-api/) — API for routes. You can manage routes and calculate route based on stops list. You can also start a new trip based on the route.
- [SPOTIO Teams API](https://apis.io/apis/spotio/spotio-teams-api/) — The controller is responsible for handling operations on teams creating, updating, deleting, and retrieving team data. The controller also handles adding…
- [SPOTIO Territories API](https://apis.io/apis/spotio/spotio-territories-api/) — The controller is responsible for getting all territories for a company.
- [SPOTIO Trips API](https://apis.io/apis/spotio/spotio-trips-api/) — The controller is responsible for handling operations on trip objects. Trips are created from routes and record places that user visited during the trip.…
- [SPOTIO Trips V2 API](https://apis.io/apis/spotio/spotio-tripsv2-api/) — The controller is responsible for handling operations on trip objects. Trips are created from routes and record places that user visited during the trip.…
- [SPOTIO Upload Care API](https://apis.io/apis/spotio/spotio-uploadcare-api/) — Handles file upload operations
- [SPOTIO Users API](https://apis.io/apis/spotio/spotio-users-api/) — The controller is responsible for handling the creation, updating, deleting Spotio Users. This controller allow users to exchange of credentials for a token.
- [SPOTIO Webhooks API](https://apis.io/apis/spotio/spotio-webhooks-api/) — The controller is responsible for handling webhooks related operations. It provides methods for retrieving available webhook scopes, getting all webhooks…
- [SPOTIO Workflow Activity Templates API](https://apis.io/apis/spotio/spotio-workflowactivitytemplates-api/) — Activity templates are used to define type of activities in the system. To create activity from the activity template refer to the ActivitiesController.…
- [SPOTIO Workflow Data Objects API](https://apis.io/apis/spotio/spotio-workflowdataobjects-api/) — This controller is responsible for managing data object definitions. Data object definition consists of field and stages definitions. To create records from…
- [SPOTIO Workflow Fields API](https://apis.io/apis/spotio/spotio-workflowfields-api/) — Api is responsible for the comprehensive management of fields associated with data objects within a workflow. This includes functionality for retrieving…
- [SPOTIO Workflow Settings API](https://apis.io/apis/spotio/spotio-workflowsettings-api/) — Workflow Settings API provides operations including fetching full workflow settings for company as well as retrieving and updating workflow company properties.
- [SPOTIO Communication Templates API](https://apis.io/apis/spotio/spotio-communication-templates-api/) — The controller is responsible for managing company templates. Templates for text messages and emails. The controller allows creating new templates which can…
- [SPOTIO Filters V2 API](https://apis.io/apis/spotio/spotio-filters-v2-api/) — The controller is responsible for handling operations on filter objects. Filter can be used throughout the system to filter data. It can be passed wherever…
- [SPOTIO User Tracking API](https://apis.io/apis/spotio/spotio-user-tracking-api/) — User tracking API. You can configure Spotio to track users which using the app. Using the following methods you can retrieve tracking data.
- [SPOTIO Workflow Stages API](https://apis.io/apis/spotio/spotio-workflow-stages-api/) — This controller is responsible for managing stages definitions. You can split stages in 3 groups, each group can have different set of stages. The available…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Spotio Webhooks](https://apis.io/asyncapis/spotio/spotio-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [spotio](https://apis.io/servers/spotio/spotio/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Spotio Agentic Access](https://apis.io/agentic-access/spotio/spotio-agentic-access/)

#### Collections (39)

Postman and Open Collection request collections.

- [Spotio 2.0 Activities V2 API](https://apis.io/collections/spotio/open-spotio-activitiesv2-api/)
- [Spotio 2.0 Appointments V2 API](https://apis.io/collections/spotio/open-spotio-appointmentsv2-api/)
- [Spotio 2.0 Autoplays API](https://apis.io/collections/spotio/open-spotio-autoplays-api/)
- [Spotio 2.0 Business Cards API](https://apis.io/collections/spotio/open-spotio-businesscards-api/)
- [Spotio 2.0 Calendar Settings API](https://apis.io/collections/spotio/open-spotio-calendarsettings-api/)
- [Spotio 2.0 Communication API](https://apis.io/collections/spotio/open-spotio-communication-api/)
- [Spotio 2.0 Communication Templates API](https://apis.io/collections/spotio/open-spotio-communicationtemplates-api/)
- [Spotio 2.0 Connectors API](https://apis.io/collections/spotio/open-spotio-connectors-api/)
- [Spotio 2.0 Contracts API](https://apis.io/collections/spotio/open-spotio-contracts-api/)
- [Spotio 2.0 Data Objects API](https://apis.io/collections/spotio/open-spotio-dataobjects-api/)
- [Spotio 2.0 Data Objects Bulk Jobs API](https://apis.io/collections/spotio/open-spotio-dataobjectsbulkjobs-api/)
- [Spotio 2.0 Data Objects Search API](https://apis.io/collections/spotio/open-spotio-dataobjectssearch-api/)
- [Spotio 2.0 Documents API](https://apis.io/collections/spotio/open-spotio-documents-api/)
- [Spotio 2.0 Exports API](https://apis.io/collections/spotio/open-spotio-exports-api/)
- [Spotio 2.0 Filters API](https://apis.io/collections/spotio/open-spotio-filters-api/)
- [Spotio 2.0 Filters V2 API](https://apis.io/collections/spotio/open-spotio-filtersv2-api/)
- [Spotio 2.0 Generate Content API](https://apis.io/collections/spotio/open-spotio-generatecontent-api/)
- [Spotio 2.0 Layouts API](https://apis.io/collections/spotio/open-spotio-layouts-api/)
- [Spotio 2.0 Leaderboards API](https://apis.io/collections/spotio/open-spotio-leaderboards-api/)
- [Spotio 2.0 MCP API](https://apis.io/collections/spotio/open-spotio-mcp-api/)
- [Spotio 2.0 Multi Channel Communication API](https://apis.io/collections/spotio/open-spotio-multichannelcommunication-api/)
- [Spotio 2.0 My Reports API](https://apis.io/collections/spotio/open-spotio-myreports-api/)
- [Spotio 2.0 Notifications V2 API](https://apis.io/collections/spotio/open-spotio-notificationsv2-api/)
- [Spotio 2.0 Pins V2 API](https://apis.io/collections/spotio/open-spotio-pinsv2-api/)
- [Spotio 2.0 Reports API](https://apis.io/collections/spotio/open-spotio-reports-api/)
- …and 14 more published on APIs.io

#### Overlays (39)

OpenAPI overlays, including conversational phrasing for each operation.

- [Spotio Activitiesv2 Overlay](https://apis.io/overlays/spotio/spotio-activitiesv2-overlay/)
- [Spotio Appointmentsv2 Overlay](https://apis.io/overlays/spotio/spotio-appointmentsv2-overlay/)
- [Spotio Autoplays Overlay](https://apis.io/overlays/spotio/spotio-autoplays-overlay/)
- [Spotio Businesscards Overlay](https://apis.io/overlays/spotio/spotio-businesscards-overlay/)
- [Spotio Calendarsettings Overlay](https://apis.io/overlays/spotio/spotio-calendarsettings-overlay/)
- [Spotio Communication Overlay](https://apis.io/overlays/spotio/spotio-communication-overlay/)
- [Spotio Communicationtemplates Overlay](https://apis.io/overlays/spotio/spotio-communicationtemplates-overlay/)
- [Spotio Connectors Overlay](https://apis.io/overlays/spotio/spotio-connectors-overlay/)
- [Spotio Contracts Overlay](https://apis.io/overlays/spotio/spotio-contracts-overlay/)
- [Spotio Dataobjects Overlay](https://apis.io/overlays/spotio/spotio-dataobjects-overlay/)
- [Spotio Dataobjectsbulkjobs Overlay](https://apis.io/overlays/spotio/spotio-dataobjectsbulkjobs-overlay/)
- [Spotio Dataobjectssearch Overlay](https://apis.io/overlays/spotio/spotio-dataobjectssearch-overlay/)
- [Spotio Documents Overlay](https://apis.io/overlays/spotio/spotio-documents-overlay/)
- [Spotio Exports Overlay](https://apis.io/overlays/spotio/spotio-exports-overlay/)
- [Spotio Filters Overlay](https://apis.io/overlays/spotio/spotio-filters-overlay/)
- [Spotio Filtersv2 Overlay](https://apis.io/overlays/spotio/spotio-filtersv2-overlay/)
- [Spotio Generatecontent Overlay](https://apis.io/overlays/spotio/spotio-generatecontent-overlay/)
- [Spotio Layouts Overlay](https://apis.io/overlays/spotio/spotio-layouts-overlay/)
- [Spotio Leaderboards Overlay](https://apis.io/overlays/spotio/spotio-leaderboards-overlay/)
- [Spotio Mcp Overlay](https://apis.io/overlays/spotio/spotio-mcp-overlay/)
- [Spotio Multichannelcommunication Overlay](https://apis.io/overlays/spotio/spotio-multichannelcommunication-overlay/)
- [Spotio Myreports Overlay](https://apis.io/overlays/spotio/spotio-myreports-overlay/)
- [Spotio Notificationsv2 Overlay](https://apis.io/overlays/spotio/spotio-notificationsv2-overlay/)
- [Spotio Pinsv2 Overlay](https://apis.io/overlays/spotio/spotio-pinsv2-overlay/)
- [Spotio Reports Overlay](https://apis.io/overlays/spotio/spotio-reports-overlay/)
- …and 14 more published on APIs.io

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Spotio Authentication](https://apis.io/security/spotio/spotio-authentication/)
- [Spotio Domain Security](https://apis.io/security/spotio/spotio-domain-security/)
- [Spotio Trust Center](https://apis.io/security/spotio/spotio-trust-center/)
- [Spotio Vulnerability Disclosure](https://apis.io/security/spotio/spotio-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Spotio Plans Pricing](https://apis.io/plans/spotio/spotio-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Spotio Rate Limits](https://apis.io/rate-limits/spotio/spotio-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://spotio.com)
- [Documentation](https://developer.spotio2.com/)
- [Getting started](https://developer.spotio2.com/docs/spotio2/a4cpj8d1knctg-quickstart-for-the-spotio-api)
- [API reference](https://developer.spotio2.com/docs/spotio2/c977e70019695-spotio-2-0)
- [Pricing](https://spotio.com/plans/)
- [Sign up](https://spotio.com/request-a-demo/)
- [Support](https://support.spotio.com/)
- [Changelog](https://support.spotio.com/release-notes)
- [Blog](https://spotio.com/resources/)
- [Compliance](https://spotio.com/features/security-compliance/)
- [Terms of service](https://spotio.com/terms-of-service/)
- [Privacy policy](https://spotio.com/privacy-policy/)
- [GitHub](https://github.com/Spotio)
- [Status](https://status.spotio2.com/)

## API Evangelist rating

**Kin Score 68.7** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 68.3 |
| Contract quality | 57.7 |
| Contract governance | 18.2 |
| Operational transparency | 42.1 |
| Developer ergonomics | 66.1 |
| Access clarity | 92.1 |

**Agent readiness 36.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | — |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/spotio/](https://apis.io/providers/spotio/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for SPOTIO: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/spotio/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
