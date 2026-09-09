---
name: Retrieve a credential from the Edge API
description: Exchange environment-native attestation evidence for a short-lived Aembit token, then use it to fetch a credential for a Server Workload — the secretless bootstrap.
api: openapi/aembit-edge-api-openapi.yml
operations:
  - edge-api-auth
  - edge-api-get-credentials
---

# Retrieve a credential from the Edge API

Two operations, in strict order. This is the runtime path an application takes when it cannot
run Agent Proxy — the same path the Edge SDKs, the Aembit CLI and the GitHub Action wrap.

## Steps

1. **Authenticate** — `edge-api-auth` (`POST /edge/v1/auth`).
   Send an `AuthRequest` body carrying the identity and attestation evidence for a configured
   Trust Provider. **This call is deliberately unauthenticated** — the whole point is that your
   workload holds no credential yet. Aembit verifies the evidence against a Trust Provider that
   must already exist in the tenant and match the environment you are running in.

   Optionally set `X-Aembit-ResourceSet: <uuid>` to select which Resource Set's Trust Provider to
   authenticate against; omitted, the default Resource Set is used.

   A `200` returns a `TokenDTO`: an OAuth2-style access token with expiry details. It is a JWT
   (`bearerFormat: JWT`), unlike the Cloud API's opaque reference token.

2. **Get the credential** — `edge-api-get-credentials` (`POST /edge/v1/credentials`).
   Send `Authorization: Bearer <token from step 1>` and identify the Server Workload you want to
   reach. Aembit evaluates the Access Policy and returns the credential for that target.

## Rules

- **Cache the token, not the credential.** The step-1 token has a stated expiry; re-authenticate
  when it lapses rather than calling `/edge/v1/auth` on every request.
- **Handle 429 with your own backoff.** Both operations declare `429` — `POST /edge/v1/auth` as
  "Too many authentication requests", body
  `{"success": false, "message": "Too many requests. Please try again later.", "id": 0}`.
  **No `Retry-After` header is declared and no rate limit is published**, so you must supply your
  own exponential backoff with jitter. There is no signal telling you when to resume.
- **Nothing here is reversible and nothing needs to be.** These operations create no persistent
  state; the credential is short-lived and expiry is the rollback.
- **Do not reuse the Cloud API token here.** The Cloud API's `bearerAuth` reference token and the
  Edge API's `EdgeApiAuth` JWT are different credentials with different issuers and lifetimes.

## Prefer a wrapper where one exists

- TypeScript: `npm install @aembit/edge-sdk` (1.34.1, Apache-2.0)
- Python: source-only from `github.com/Aembit/edge-sdks` (`py/`) — **not published to PyPI**
- Shell / CI: `aembit credentials get --client-id <id> --server-workload-host <host> --server-workload-port <port>`
- GitHub Actions: the `Aembit/get-credentials` action
