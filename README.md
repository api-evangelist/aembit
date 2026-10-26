# AEMBIT

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

Aembit is a Workload Identity and Access Management (Workload IAM) platform for non-human
identities — AI agents, applications, microservices, CI/CD pipelines and service accounts.
Rather than storing long-lived secrets, Aembit cryptographically attests a workload against a
Trust Provider, evaluates an Access Policy, and injects a short-lived credential just in time.

## What Aembit publishes

| Surface | Where |
|---|---|
| Aembit Cloud API — OpenAPI 3.1.1, 165 operations | <https://docs.aembit.io/cloud.yaml> |
| Aembit Edge API — OpenAPI 3.1.1, 2 operations | <https://docs.aembit.io/edge.yaml> |
| Aembit MCP Server (hosted, read-only, 3 tools) | <https://docs.aembit.io/ai-guide/mcp/mcp-server/> |
| Developer guide | <https://docs.aembit.io/dev-guide/> |
| llms.txt (developer + company) | <https://docs.aembit.io/llms.txt>, <https://aembit.io/llms.txt> |
| TypeScript Edge SDK | <https://www.npmjs.com/package/@aembit/edge-sdk> |
| Terraform provider | <https://registry.terraform.io/providers/Aembit/aembit/latest> |
| CLI | <https://docs.aembit.io/dev-guide/cli/> |
| Changelog | <https://docs.aembit.io/changelog/> |
| Status page | <https://status.aembit.io/> |
| Trust center (SOC 2 Type II, ISO/IEC 27001:2022) | <https://trust.aembit.io/> |
| Pricing | <https://aembit.io/pricing/> |

## Notes from this profile

- Both OpenAPI contracts are served from the documentation host at `/cloud.yaml` and `/edge.yaml`,
  discovered from the Scalar reference page rather than from any conventional `/openapi.json` path.
- Servers are tenant-templated (`https://{tenant}.aembit.io`); there is no shared multi-tenant host.
- **No idempotency mechanism** exists on any of the 96 mutating operations, and **no reversal or
  restore endpoint** exists for the 22 DELETE operations.
- **No published rate limit.** The Edge API declares `429` on both operations with no `Retry-After`
  header and no documented number.
- Deprecation is signalled by tag naming (`Access Policy (Deprecated)`, `Credential Provider
  (Deprecated)` — 16 operations) but `deprecated: true` is set on **zero** operations, so no code
  generator or linter surfaces it.
- **No A2A agent card** on any of seven probed hosts, and **no first-party `/.well-known/` document**.
  The three `.well-known` 200s found belong to Atlassian Statuspage and SafeBase, not to Aembit.
- The Python Edge SDK exists in the first-party repository but is **not published to PyPI**.

Company surfaced through the API Evangelist harvest backlog (secondary-market source) and
profiled from Aembit's own public developer surface.
