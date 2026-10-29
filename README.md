# Appfire

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

Appfire is a global software company that builds, acquires, and operates a large portfolio of apps that enhance, extend, and connect the platforms enterprise teams already run on — principally Atlassian Jira, Confluence and Jira Service Management (Cloud and Data Center), plus Microsoft Azure DevOps, monday.com and Salesforce. Its product families cover portfolio and project management (BigPicture, BigGantt, BigTemplate), goal setting (OKR for Jira), time tracking (7pace Timetracker for Jira and for Azure DevOps), document workflow and approvals (Comala Document Management), workflow automation and scripting (Jira Misc Workflow Extensions, Power Scripts), and administration tooling (the Appfire/Atlassian Command Line Interface). Public, machine-readable API surface is per-product rather than company-wide: 7pace Timetracker for Jira publishes OpenAPI 3.0 for its v1 and v2 REST APIs, the OKR app serves an OpenAPI 3.1 document for its public export/update API, and BigPicture publishes a hosted API reference for its Cloud and Data Center REST APIs.

**Areas:** Atlassian · Jira · Confluence · Project Portfolio Management · Work Management · Time Tracking · OKRs · Workflow Automation · Azure DevOps · marketplace-apps · Document Workflow · Enterprise Software

## Appfire on APIs.io

Everything profiled for Appfire is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/appfire/](https://apis.io/providers/appfire/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [BigPicture Cloud Public API](https://apis.io/apis/appfire/bigpicture-cloud-public-api/) — Public REST API for BigPicture, BigGantt and BigTemplate on Atlassian Cloud (Appfire's portfolio and project-management suite). Exposes boxes, box types,…
- [Appfire API query methods API](https://apis.io/apis/appfire/appfire-api-query-methods-api/) — Retrieve objectives, key results, updates, and comments. Use **expand** to include related entities (teams, periods, labels, etc.) instead of IDs only.…
- [Appfire API update methods API](https://apis.io/apis/appfire/appfire-api-update-methods-api/) — **POST** with a JSON body. Send **Content-Type: application/json** and the **API-Token** header. Creates update records that set current status (and…
- [Appfire Settings API](https://apis.io/apis/appfire/appfire-settings-api/) — The Settings API from Appfire — 16 operation(s) for settings.
- [Appfire Worklogs API](https://apis.io/apis/appfire/appfire-worklogs-api/) — The Worklogs API from Appfire — 10 operation(s) for worklogs.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [appfire](https://apis.io/servers/appfire/appfire/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Appfire Agentic Access](https://apis.io/agentic-access/appfire/appfire-agentic-access/)

#### Collections (4)

Postman and Open Collection request collections.

- [OKR API query methods API](https://apis.io/collections/appfire/open-appfire-api-query-methods-api/)
- [OKR API update methods API](https://apis.io/collections/appfire/open-appfire-api-update-methods-api/)
- [Appfire Settings API](https://apis.io/collections/appfire/open-appfire-settings-api/)
- [Appfire Worklogs API](https://apis.io/collections/appfire/open-appfire-worklogs-api/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Appfire 7Pace Timetracker V1 Overlay](https://apis.io/overlays/appfire/appfire-7pace-timetracker-v1-overlay/)
- [Appfire 7Pace Timetracker V2 Overlay](https://apis.io/overlays/appfire/appfire-7pace-timetracker-v2-overlay/)
- [Appfire Okr Overlay](https://apis.io/overlays/appfire/appfire-okr-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Appfire Authentication](https://apis.io/security/appfire/appfire-authentication/)
- [Appfire Domain Security](https://apis.io/security/appfire/appfire-domain-security/)
- [Appfire Trust Center](https://apis.io/security/appfire/appfire-trust-center/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://appfire.com)
- [Documentation](https://appfire.atlassian.net/wiki/spaces/APPFIRE/overview)
- [API reference](https://developer.bigpicture.one/reference/whatisbigpicture)
- [Support](https://support.appfire.com/)
- [Blog](https://appfire.com/resources/blog)
- [Compliance](https://trust.appfire.com/)
- [Terms of service](https://appfire.com/eula)
- [Privacy policy](https://appfire.com/privacy-policy)
- [Status](https://status.appfire.com/)

## API Evangelist rating

**Kin Score 39.3** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 44.5 |
| Contract governance | 4.5 |
| Operational transparency | 31.6 |
| Developer ergonomics | 49.4 |
| Access clarity | 26.3 |

**Agent readiness 25.0** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | — |
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

**Regulatory alignment 25.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/appfire/](https://apis.io/providers/appfire/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Appfire: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/appfire/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
