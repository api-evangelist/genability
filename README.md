# Genability

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

Genability is a United States energy-data platform, based in San Francisco and now part of Arcadia, that sells programmatic access to North American electricity tariff data and a bill-calculation engine. Its Signal API — served from api.genability.com and documented as "Arcadia Platform - Signal" — covers electricity utilities, tariffs, territories, seasons, time-of-use definitions, calendars, utility taxes and typical-usage baselines across the USA, Canada and Mexico, plus on-demand and mass cost calculations used for solar savings analysis, storage dispatch, EV charging economics, procurement and bill auditing. Genability sits in the private, commercial layer of the energy value chain: it is not a utility, not a retailer and not a designated data holder under any consumer-energy-data mandate, so no Green Button, ESPI, CDR or other energy data standard is referenced anywhere in its documentation. Its API posture is honestly "self-serve but entirely closed data": a developer can sign up at dash.genability.com in minutes, but every endpoint — including the ones pathed /rest/public/ — returns 401 without an appId/appKey, so none of this tariff or market reference data is openly published, and Genability exposes no individual customer's usage or billing data at all (that consumer-data surface lives in Arcadia's separate Plug/Arc API).

**Areas:** Energy · United States · Utilities · Electricity · Tariffs · Energy Rates · Rate Calculation · Energy Data Platform · Solar · Grid

## Genability on APIs.io

Everything profiled for Genability is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/genability/](https://apis.io/providers/genability/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Genability GET API](https://apis.io/apis/genability/genability-get-api/) — The GET API from Genability — 1 operation(s) for get.
- [Genability Rest API](https://apis.io/apis/genability/genability-rest-api/) — The Rest API from Genability — 32 operation(s) for rest.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [genability-mcp.yml](https://apis.io/servers/genability/genability-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Genability Agentic Access](https://apis.io/agentic-access/genability/genability-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [signal](https://apis.io/collections/genability/open-genability-signal/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Genability Signal Overlay](https://apis.io/overlays/genability/genability-signal-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Genability Authentication](https://apis.io/security/genability/genability-authentication/)
- [Genability Domain Security](https://apis.io/security/genability/genability-domain-security/)
- [Genability Vulnerability Disclosure](https://apis.io/security/genability/genability-vulnerability-disclosure/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://genability.com/)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/docs/welcome-to-signal)
- [Getting started](https://docs.arcadia.com/v2022-12-21-Signal/docs/quick-start)
- [API reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/api-basics)
- [Sign up](https://dash.genability.com/signup)
- [Support](https://www.arcadia.com/contact)
- [Changelog](https://docs.arcadia.com/v2022-12-21-Signal/changelog)
- [Blog](https://www.arcadia.com/blog)
- [Security](https://www.arcadia.com/security)
- [Terms of service](https://platform-legal.arcadia.com/#platform-terms-of-service)
- [Privacy policy](https://platform-legal.arcadia.com/#arcadia-privacy-policy)
- [GitHub](https://github.com/Genability)
- [Status](https://status.arcadia.com)

## API Evangelist rating

**Kin Score 44.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 49.9 |
| Contract governance | 4.5 |
| Operational transparency | 36.8 |
| Developer ergonomics | 66.1 |
| Access clarity | 23.7 |

**Agent readiness 29.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
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
| Operation Distinctiveness | distinct |

**Regulatory alignment 28.7** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/genability/](https://apis.io/providers/genability/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Genability: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/genability/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
