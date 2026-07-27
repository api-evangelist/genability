---
name: Validate credentials and debug a Signal integration
description: >-
  Use the Echo API family to confirm appId/appKey work, check input formats, and
  exercise your error handling against real Signal error envelopes before
  calling priced endpoints.
api: openapi/genability-signal-openapi.json
operations: [echo-api-authenticate, echo-api-hello, echo-api-validate, echo-api-errors, echo]
generated: '2026-07-27'
method: generated
source: >-
  openapi/genability-signal-openapi.json +
  https://docs.arcadia.com/v2022-12-21-Signal/reference/echo-summary
---

# Validate credentials and debug a Signal integration

Signal has no sandbox host and no test-key prefix — there is one environment,
`https://api.genability.com`. What it does have is the Echo family: five live
endpoints that cost you nothing conceptually and let you get authentication,
formatting and error handling right before touching tariff or calculation
endpoints. All Echo calls still require valid credentials.

## Steps

1. **Confirm the credential pair** — `echo-api-authenticate`
   `GET /rest/echo/authenticate`. A success envelope means `appId` (username)
   and `appKey` (password) are valid Basic credentials. A `401` with
   `{"code":"Unauthorized","message":"The credentials were not supplied or are
   invalid","propertyName":"appId"}` means they are not.

2. **Confirm the transport** — `echo-api-hello`
   `GET /rest/echo/hello` returns a Hello World payload when credentials are
   valid, so you can prove TLS, Basic header construction and JSON parsing end
   to end.

3. **Check an input before you send it** — `echo-api-validate`
   `GET /rest/echo/validate` tells you whether a value is in a recognized
   format: dates, times, integers and arrays. Use it when a `400` names a
   `propertyName` you thought was well-formed.

4. **Exercise your error handling** — `echo-api-errors`
   `GET /rest/echo/errors?errorCode={code}` where `errorCode` is one of the
   published enum values `200`, `301`, `400`, `403`, `404`, `500`. Each returns
   the real Signal error envelope for that status, so your retry, logging and
   user-messaging paths can be tested against genuine payloads.

5. **Inspect a whole request** — `echo`
   `GET /rest/echo/{errorCode}` echoes back how you are calling the API, for
   debugging request formatting, authentication and input values. (The harvested
   contract templates this path as `{error_code}` while naming the parameter
   `errorCode`, and declares no responses — an upstream defect, recorded in
   `overlays/genability-signal-overlay.yaml`.)

## Rules

- Credentials: HTTP Basic, `appId:appKey`, Base64 in an `Authorization: Basic`
  header if your client will not build it for you. Mint both at
  `https://dash.genability.com/org/applications`; a credit card is required to
  create an Application on the 14-day trial.
- Every response — success or error — uses the same
  `{status, count, type, results[]}` wrapper.
- Only `200`, `301`, `400`, `403`, `404` and `500` are simulable. `401`, `429`
  and `503` are documented in prose but are not in the simulator or in the
  machine-readable contract.
- When you graduate to real endpoints, keep concurrency around 4 and ramp up
  over 8-10 minutes; the spike limiter answers `429` with `Retry-After`.
