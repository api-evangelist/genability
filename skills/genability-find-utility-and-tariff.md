---
name: Find a customer's utility and tariff
description: >-
  Given a US, Canadian or Mexican postal code (or address), identify the Load
  Serving Entity that serves it, list the tariffs that customer is eligible for,
  and pull the full rate detail for the chosen master tariff.
api: openapi/genability-signal-openapi.json
operations: [get-lses, get-tariff, get-tariff-1, get-tariff-history, zip-code-api]
generated: '2026-07-27'
method: generated
source: >-
  openapi/genability-signal-openapi.json +
  https://docs.arcadia.com/v2022-12-21-Signal/docs/tariff-identification-workflow
---

# Find a customer's utility and tariff

Signal is reference data: you start from a location, narrow to a utility, then
to a tariff. Every request is HTTP Basic — `appId` as username, `appKey` as
password — over TLS against `https://api.genability.com`. Paths under
`/rest/public/` are non-org-scoped reference data, **not** anonymous: they
return `401` without credentials.

## Steps

1. **Validate credentials once** — `echo-api-authenticate`
   `GET /rest/echo/authenticate`. A success envelope means the `appId`/`appKey`
   pair is good. Do this before burning priced calls.

2. **Identify the utility** — `get-lses`
   `GET /rest/public/lses?postCode=94104&country=USA`. Use `zipCode` or
   `postCode` for location, or `search` + `searchOn=name,code` to look a utility
   up by name. Filter with `ownerships` and `serviceTypes` when a location is
   served by more than one LSE. Read `lseId` from `results[]`.
   Optionally enrich the location first with `zip-code-api`
   (`GET /rest/public/zipcodes/{zipCode}`) for city, county, coordinates and
   time zone.

3. **List candidate tariffs** — `get-tariff`
   `GET /rest/public/tariffs?lseId={lseId}&customerClasses=RESIDENTIAL&tariffTypes=DEFAULT&effectiveOn=2026-07-01`.
   This operation exposes 33 documented query parameters; the ones that do most
   of the work are `lseId`, `customerClasses`, `tariffTypes`, `serviceTypes`,
   `effectiveOn`/`openOn`, `isActive`, `zipCode`/`postCode`/`addressString`,
   and the capability filters `hasNetMetering`, `hasTimeOfUseRates`,
   `hasTieredRates`. Add `populateProperties=true` to see what inputs each
   tariff needs before you price it.

4. **Narrow a long list** — add `consumption` and `demand` to filter by size,
   `applicableRatesOnly=true` and `filterByApplicability=true` to drop rates the
   customer cannot get, and `sortOn`/`sortOrder` to rank. Use `fields=ext` only
   when you actually need every field — the default view is smaller and faster.

5. **Pull the chosen tariff in full** — `get-tariff-1`
   `GET /rest/public/tariffs/{masterTariffId}?populateRates=true&populateProperties=true&populateDocuments=true`.
   `masterTariffId` is stable across effective-dated versions; keep it as your
   customer's tariff key.

6. **Check history when modelling the past** — `get-tariff-history`
   `GET /rest/public/tariffs/{masterTariffId}/history` returns the effective-dated
   versions, so a bill from last year is priced against the rates in force then.

## Rules

- **Pagination**: `pageStart` (default `0`) and `pageCount` (default `25`).
  `count` in the envelope is the total match count, capped at `100000` — treat
  `100000` as "100,000 or more".
- **Envelope**: every response is `{status, count, type, results[]}` and
  `results` is always an array, even for a single object.
- **Errors**: `status: "error"`, `type: "Error"`, each item carrying
  `code`, `message`, `objectName`, `propertyName`. See
  `errors/genability-problem-types.yml`.
- **Throttling**: a dynamic spike limiter returns `429` with `Retry-After`.
  Keep concurrency around 4 and ramp up over 8-10 minutes
  (`conventions/genability-conventions.yml`).
- **No idempotency contract exists.** These are all reads, so retry freely; do
  not assume replay protection on writes.
- Arrays go as `a,b` or repeated `k=a&k=b`. Dates are ISO 8601 with an explicit
  offset.
