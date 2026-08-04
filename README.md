# Genability (genability)

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

Genability is a United States energy-data platform, based in San Francisco and now part of Arcadia, that sells programmatic access to North American electricity tariff data and a bill-calculation engine. Its Signal API — served from api.genability.com and documented as "Arcadia Platform - Signal" — covers electricity utilities, tariffs, territories, seasons, time-of-use definitions, calendars, utility taxes and typical-usage baselines across the USA, Canada and Mexico, plus on-demand and mass cost calculations used for solar savings analysis, storage dispatch, EV charging economics, procurement and bill auditing. Genability sits in the private, commercial layer of the energy value chain: it is not a utility, not a retailer and not a designated data holder under any consumer-energy-data mandate, so no Green Button, ESPI, CDR or other energy data standard is referenced anywhere in its documentation. Its API posture is honestly "self-serve but entirely closed data": a developer can sign up at dash.genability.com in minutes, but every endpoint — including the ones pathed /rest/public/ — returns 401 without an appId/appKey, so none of this tariff or market reference data is openly published, and Genability exposes no individual customer's usage or billing data at all (that consumer-data surface lives in Arcadia's separate Plug/Arc API).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/genability/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/genability/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Utilities
- Electricity
- Tariffs
- Energy Rates
- Rate Calculation
- Energy Data Platform
- Solar
- Grid

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Genability Signal Tariff API

Search and retrieve North American electricity tariffs, including rate structures, applicability properties, documents and the effective-dated history of a master tariff. The list endpoint exposes 33 documented query parameters for filtering by utility, territory, customer class, service type, tariff type and effective date.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/tariff](https://docs.arcadia.com/v2022-12-21-Signal/reference/tariff)
- **Base URL:** `https://api.genability.com`

#### Tags

- Tariffs
- Energy Rates
- Electricity

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/docs/find-utilities-and-tariffs)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-tariff)
- [Authentication](https://docs.arcadia.com/v2022-12-21-Signal/reference/authentication)

### Genability Signal Load Serving Entity API

List and retrieve Load Serving Entities (LSEs) — the investor-owned utilities, municipal utilities and cooperatives that serve electricity across the USA, Canada and Mexico — searchable by postal code, name or utility code.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/load-serving-entities-lses](https://docs.arcadia.com/v2022-12-21-Signal/reference/load-serving-entities-lses)
- **Base URL:** `https://api.genability.com`

#### Tags

- Utilities
- Electricity

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/docs/find-customer-utility)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-lses)

### Genability Signal Territory API

List and retrieve territories — the service, baseline, climate and tariff applicability geographies that a utility uses to scope which rates apply to a given premise.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/territory](https://docs.arcadia.com/v2022-12-21-Signal/reference/territory)
- **Base URL:** `https://api.genability.com`

#### Tags

- Territories
- Utilities

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-territories)

### Genability Signal Cost Calculation API

On-demand bill calculation against any North American tariff. Post a usage scenario and receive a modeled cost breakdown, or use the mass calculation endpoint to price many scenarios in one request for savings analysis, bill auditing and rate comparison.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/calculation-apis](https://docs.arcadia.com/v2022-12-21-Signal/reference/calculation-apis)
- **Base URL:** `https://api.genability.com`

#### Tags

- Cost Modeling
- Energy Rates
- Billing

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/calculate)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/reference/on-demand-mass-calculation)

### Genability Signal Smart Price API

Returns a single blended price signal ($/kWh) for a utility, tariff and time window, for use in dispatch logic, EV charging schedules and consumer-facing price displays.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/smart-price](https://docs.arcadia.com/v2022-12-21-Signal/reference/smart-price)
- **Base URL:** `https://api.genability.com`

#### Tags

- Energy Rates
- Pricing

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/smart-price-api)

### Genability Signal Time of Use API

Retrieve time-of-use (TOU) groups, TOU definitions and their interval schedules for a utility, and create private TOU definitions scoped to your own organization.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/time-of-use-tou](https://docs.arcadia.com/v2022-12-21-Signal/reference/time-of-use-tou)
- **Base URL:** `https://api.genability.com`

#### Tags

- Time of Use
- Energy Rates

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-tou-group)

### Genability Signal Calendar API

List calendars and calendar dates — the holiday and special-day schedules that determine which rate periods apply on a given date under a tariff.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/calendar](https://docs.arcadia.com/v2022-12-21-Signal/reference/calendar)
- **Base URL:** `https://api.genability.com`

#### Tags

- Calendars
- Energy Rates

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-calendars)

### Genability Signal Season API

List season groups, the seasonal definitions a utility applies when a tariff prices summer and winter usage differently.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/season](https://docs.arcadia.com/v2022-12-21-Signal/reference/season)
- **Base URL:** `https://api.genability.com`

#### Tags

- Seasons
- Energy Rates

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/get-season)

### Genability Signal Property and Lookup API

List and retrieve property keys — the typed inputs a tariff calculation accepts — along with their permitted lookup values and usage statistics, so a client can discover exactly what a given rate needs before pricing it.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/properties](https://docs.arcadia.com/v2022-12-21-Signal/reference/properties)
- **Base URL:** `https://api.genability.com`

#### Tags

- Metadata
- Energy Rates

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/properties-api)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/reference/lookups)

### Genability Signal Typical Baseline API

Returns a best-fit typical usage baseline — a modeled hourly or monthly load profile — for a location and building type, used when real interval data for a customer is not available.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/typical-baseline](https://docs.arcadia.com/v2022-12-21-Signal/reference/typical-baseline)
- **Base URL:** `https://api.genability.com`

#### Tags

- Load Profiles
- Usage Modeling

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/typical-baseline-api)

### Genability Signal ZIP Code API

Retrieve details for a ZIP code, including the utilities and territories that serve it, as the entry point for identifying a customer's tariff from an address.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/zip-code](https://docs.arcadia.com/v2022-12-21-Signal/reference/zip-code)
- **Base URL:** `https://api.genability.com`

#### Tags

- Geography
- Utilities

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/zip-code-api)

### Genability Signal Utility Tax API

List and retrieve the utility taxes that apply to an electricity bill by jurisdiction, so a modeled bill reflects the taxes a customer actually pays.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/tariff-rate-components-overview](https://docs.arcadia.com/v2022-12-21-Signal/reference/tariff-rate-components-overview)
- **Base URL:** `https://api.genability.com`

#### Tags

- Taxes
- Billing

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Genability Signal Organization Usage API

Reports your own organization's Signal API consumption, the metering surface behind Genability's subscription billing.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/organization-usage](https://docs.arcadia.com/v2022-12-21-Signal/reference/organization-usage)
- **Base URL:** `https://api.genability.com`

#### Tags

- Usage Metering
- Account

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/organization-usage-api)

### Genability Signal Echo API

Testing and debugging endpoints that validate credentials, echo a hello response, simulate error codes and validate input formats before a client calls the priced endpoints.

- **Human URL:** [https://docs.arcadia.com/v2022-12-21-Signal/reference/echo-summary](https://docs.arcadia.com/v2022-12-21-Signal/reference/echo-summary)
- **Base URL:** `https://api.genability.com`

#### Tags

- Testing
- Sandbox

#### Properties

- [OpenAPI](openapi/genability-signal-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/echo)

## Common Properties

- [Website](https://genability.com/)
- [Developer Portal](https://docs.arcadia.com/v2022-12-21-Signal/)
- [Documentation](https://docs.arcadia.com/v2022-12-21-Signal/docs/welcome-to-signal)
- [API Reference](https://docs.arcadia.com/v2022-12-21-Signal/reference/api-basics)
- [Getting Started](https://docs.arcadia.com/v2022-12-21-Signal/docs/quick-start)
- [Authentication](https://docs.arcadia.com/v2022-12-21-Signal/reference/authentication)
- [Rate Limits](https://docs.arcadia.com/v2022-12-21-Signal/docs/rate-limit-best-practices)
- [LLMs.txt](https://docs.arcadia.com/v2022-12-21-Signal/llms.txt)
- [Sign Up](https://dash.genability.com/signup)
- [Login](https://dash.genability.com/login)
- [GitHub Organization](https://github.com/Genability)
- [SDKs](https://github.com/Genability/genability-js)
- [SDKs](https://github.com/Genability/genability-java)
- [SDKs](https://github.com/Genability/Genability-PHP-Library)
- [LinkedIn](https://www.linkedin.com/company/genability)

## Maintainers

**FN:** Kin Lane  
**Email:** kin@apievangelist.com
