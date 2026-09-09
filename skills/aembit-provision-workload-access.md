---
name: Provision secretless workload access
description: Create the Trust Provider, workloads, Credential Provider and Access Policy that let one workload reach one protected resource without a stored secret.
api: openapi/aembit-cloud-api-openapi.yml
operations:
  - post-trust-provider
  - post-client-workload
  - post-server-workload
  - post-credential-provider2
  - get-credential-provider-verification-v2
  - post-access-policy-v2
  - get-access-policy-by-workloads-v2
---

# Provision secretless workload access

Aembit's model is a policy graph. Nothing works until five objects exist and one of them
(the Access Policy) joins the other four. Create them in this order.

## Before you start

- Base URL is tenant-templated: `https://{tenant}.aembit.io`. Get `{tenant}` from the Admin UI
  Profile screen — there is no shared host.
- Authenticate with `Authorization: Bearer <Aembit API Token>`, generated on the same Profile
  screen. It is an opaque reference token; do not try to parse it.
- Set `X-Aembit-ResourceSet: <uuid>` on every call. It is optional and falls back to the default
  Resource Set, but for automation you want the boundary explicit. List them with
  `get-resource-sets`.
- Use the **v2** operations. The v1 Access Policy and Credential Provider families are tagged
  "(Deprecated)" in the contract even though `deprecated: true` is not set on the operations.

## Steps

1. **Create the Trust Provider** — `post-trust-provider` (`POST /api/v1/trust-providers`).
   This is how Aembit will verify the requester's identity from environment-native evidence
   (AWS Metadata Service, AWS Role, GCP Identity Token, GitHub Action ID Token, GitLab Job ID
   Token, Kubernetes Service Account, OIDC ID Token, Terraform Cloud Identity Token, AWS ALB JWT,
   GCP IAP JWT). Keep the returned `externalId`.

2. **Create the Client Workload** — `post-client-workload` (`POST /api/v1/client-workloads`).
   This is the requester. Bind it to the Trust Provider from step 1 and give it identifiers that
   match the runtime. Call `get-client-identifiers`
   (`GET /api/v1/client-workloads/identifiers`) first to see the identifier types available.

3. **Create the Server Workload** — `post-server-workload` (`POST /api/v1/server-workloads`).
   This is the target: an API, database, LLM endpoint or MCP server, addressed by host and port.

4. **Create the Credential Provider** — `post-credential-provider2`
   (`POST /api/v2/credential-providers`). This mints or brokers the credential that will be
   injected. Then call `get-credential-provider-verification-v2`
   (`GET /api/v2/credential-providers/{id}/verification`) and confirm it before going further —
   this is the only rehearsal affordance the API offers, and a policy built on an unverified
   credential provider fails at runtime rather than at creation.

5. **Create the Access Policy** — `post-access-policy-v2` (`POST /api/v2/access-policies`).
   Bind `clientWorkload`, `serverWorkload`, the Trust Provider and the Credential Provider. Add
   Access Conditions here if you need posture, geography or time-window constraints
   (`post-access-condition2`).

6. **Confirm the binding resolves** — `get-access-policy-by-workloads-v2`
   (`GET /api/v2/access-policies/getByWorkloadIds/{clientWorkloadId}/{serverWorkloadId}`).
   If this returns your policy, the graph is wired correctly.

## Rules that will bite you

- **There is no idempotency.** No `Idempotency-Key` header exists on any of the 96 mutating
  operations. If step 1-5 times out ambiguously, **do not blind-retry the POST** — you will
  create a duplicate. List the collection and match on `name` first, then retry only if absent.
- **DELETE is permanent.** No restore, undelete or trash endpoint exists for any entity. Prefer
  `PATCH` with `isActive: false` to take something out of service; you can turn it back on.
  If you must delete, `GET` the entity and keep the body first.
- **Errors are not RFC 9457.** Every failure returns `{success: false, message: "...", id: n}` as
  `application/json`. Branch on the HTTP status; `message` is free text and `id` is not a stable
  error code. `400`, `401` and `500` are declared on effectively every operation; `404` is
  declared on only 11 of 165, so a missing resource may not surface the way you expect.
- **Pagination is offset.** `page` (default 1) and `per-page` (default 100), with `recordsTotal`
  in the list envelope. There is no cursor and no next link. The `filter`, `order` and `group-by`
  query parameters are untyped strings with no published grammar — do not rely on them.
