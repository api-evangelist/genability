---
name: Price a usage scenario against a tariff
description: >-
  Run an on-demand bill calculation for a master tariff and a usage scenario,
  compare many scenarios in one mass calculation, and fall back to a modeled
  typical baseline when the customer has no interval data.
api: openapi/genability-signal-openapi.json
operations: [calculate, mass-calculate, typical-baseline-api, properties-api, get-one-property, get-utility-taxes, smart-price-api]
generated: '2026-07-27'
method: generated
source: >-
  openapi/genability-signal-openapi.json +
  https://docs.arcadia.com/v2022-12-21-Signal/docs/run-calculations
---

# Price a usage scenario against a tariff

The calculation engine is the reason to use Signal: you supply a
`masterTariffId`, a date range and usage inputs, and it returns a modeled cost
breakdown. Nothing is stored — these are stateless pricing calls.

## Steps

1. **Discover what the tariff needs** — `properties-api`
   `GET /rest/public/properties?entityId={masterTariffId}&entityType=TARIFF`, or
   `get-one-property` (`GET /rest/public/properties/{keyName}`) for one key.
   Property keys are the typed inputs a calculation accepts (`consumption`,
   `demand`, `buildingType`, ...). Calling `get-tariff-1` with
   `populateProperties=true` gives the same picture from the tariff side.

2. **Run the calculation** — `calculate`
   `POST /rest/v1/ondemand/calculate`. The request body requires
   `masterTariffId`, `fromDateTime`, `toDateTime` and `propertyInputs`. Usage
   goes in as a `propertyInputs` entry with `keyName` (e.g. `consumption`),
   `unit` (e.g. `kWh`), and either a `dataValue` or a `dataSeries` +
   `fromDateTime` + `duration` (milliseconds per interval — `3600000` is
   hourly).

3. **Compare many scenarios at once** — `mass-calculate`
   `POST /rest/v1/ondemand/calculate/mass`, body requires `fromDateTime`,
   `toDateTime` and `scenarios`. Use it for savings analysis, rate comparison
   and bill auditing instead of looping `calculate`; it is one request against
   the spike limiter instead of N.

4. **Model usage you do not have** — `typical-baseline-api`
   `GET /rest/v1/typicals/baselines/best?zipCode=94104&country=USA&customerClass=RESIDENTIAL&buildingType=...`
   returns a best-fit hourly or monthly load profile. Feed its series back into
   `calculate` as `propertyInputs.dataSeries`.

5. **Add taxes when the rate book does not model them** — `get-utility-taxes`
   `GET /rest/v1/utilitytaxes?territoryId={territoryId}&customerClasses=RESIDENTIAL`.
   (Note the harvested contract carries this path with a malformed key,
   `"/GET /rest/v1/utilitytaxes"`; the real request is
   `GET https://api.genability.com/rest/v1/utilitytaxes`.)

6. **Need one number, not a bill?** — `smart-price-api`
   `GET /rest/v1/prices/smart?masterTariffId=...&fromDateTime=...&toDateTime=...`
   returns a single blended $/kWh signal for dispatch logic, EV charging
   schedules or a consumer-facing price display.

7. **Watch your own consumption** — `product-usage-data`
   `GET /rest/v1/orgs/usage?startYearMonth=2026-01&endYearMonth=2026-07` reports
   month-to-date Signal usage for the organization, which is what Genability
   bills on.

## Rules

- Dates are ISO 8601 **with an explicit offset**
  (`2016-07-13T00:00:00-07:00`); a missing offset is a common `400`.
- Control output shape with `detailLevel` (cost granularity) and `groupBy` (time
  granularity) as documented in the calculation guides.
- There is **no idempotency key**. `calculate` and `mass-calculate` create no
  resource, so a retry after a timeout is safe, but Genability makes no
  idempotency guarantee — never assume replay protection on
  `tou-api-copy-3` (`POST /rest/timeofuses`), the one write in the contract.
- Errors come back as `{status:"error", type:"Error", results:[{code, message,
  objectName, propertyName}]}`. `400` almost always names the offending
  `propertyName`.
- Back off on `429` using `Retry-After`; batch with `mass-calculate` rather than
  raising concurrency.
