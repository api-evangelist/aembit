# Aembit

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

Aembit is a Workload Identity and Access Management (Workload IAM) platform for non-human identities — AI agents, applications, microservices, CI/CD pipelines, scripts and service accounts. Instead of long-lived, hard-coded secrets, Aembit cryptographically attests a workload against a Trust Provider (AWS, Azure, GCP, GitHub Actions, GitLab, Kubernetes, Terraform Cloud, OIDC, SPIFFE, Kerberos), evaluates an Access Policy with optional conditional-access signals from CrowdStrike and Wiz, and injects a short-lived credential just-in-time so the application never stores one. The platform is delivered as a SaaS control plane (Aembit Cloud) plus a distributed enforcement layer (Aembit Edge — Agent Proxy, Agent Injector, AWS Lambda extension, CLI and Edge SDKs). Aembit publishes two OpenAPI 3.1.1 contracts — the Aembit Cloud API for managing every platform resource and the Aembit Edge API for workload authentication and credential retrieval — alongside a hosted, read-only MCP Server for querying audit, authorization and workload events, an MCP Identity Gateway and an MCP Authorization Server for governing AI-agent access to MCP servers.

**Areas:** Security · Identity · Identity and Access Management · Workload Identity · Non-Human Identity · Secrets Management · Zero Trust · AI Agents · MCP · Authentication · Authorization · DevSecOps

## Aembit on APIs.io

Everything profiled for Aembit is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aembit/](https://apis.io/providers/aembit/)** — or go straight to one of the APIs or properties below.

### APIs (38)

- [Aembit MCP Server](https://apis.io/apis/aembit/aembit-mcp-server/) — A first-party hosted Model Context Protocol server that gives AI agents and MCP clients read-only access to a tenant's Aembit event logs. Three tools —…
- [Aembit Access Authorization Event API](https://apis.io/apis/aembit/aembit-access-authorization-event-api/) — The Access Authorization Event API from Aembit — 2 operation(s) for access authorization event.
- [Aembit Access Condition API](https://apis.io/apis/aembit/aembit-access-condition-api/) — The Access Condition API from Aembit — 2 operation(s) for access condition.
- [Aembit Access Condition v2 API](https://apis.io/apis/aembit/aembit-access-condition-v2-api/) — The Access Condition v2 API from Aembit — 2 operation(s) for access condition v2.
- [Aembit Access Policy (Deprecated) API](https://apis.io/apis/aembit/aembit-access-policy-deprecated-api/) — The Access Policy (Deprecated) API from Aembit — 4 operation(s) for access policy (deprecated).
- [Aembit Access Policy v2 API](https://apis.io/apis/aembit/aembit-access-policy-v2-api/) — The Access Policy v2 API from Aembit — 5 operation(s) for access policy v2.
- [Aembit Agent Controller API](https://apis.io/apis/aembit/aembit-agent-controller-api/) — The Agent Controller API from Aembit — 3 operation(s) for agent controller.
- [Aembit Audit Log API](https://apis.io/apis/aembit/aembit-audit-log-api/) — The Audit Log API from Aembit — 2 operation(s) for audit log.
- [Aembit Auth API](https://apis.io/apis/aembit/aembit-auth-api/) — The Auth API from Aembit — 1 operation(s) for auth.
- [Aembit Client Workload API](https://apis.io/apis/aembit/aembit-client-workload-api/) — The Client Workload API from Aembit — 3 operation(s) for client workload.
- [Aembit Compliance API](https://apis.io/apis/aembit/aembit-compliance-api/) — The Compliance API from Aembit — 1 operation(s) for compliance.
- [Aembit Content Security API](https://apis.io/apis/aembit/aembit-content-security-api/) — The Content Security API from Aembit — 2 operation(s) for content security.
- [Aembit Credential Provider (Deprecated) API](https://apis.io/apis/aembit/aembit-credential-provider-deprecated-api/) — The Credential Provider (Deprecated) API from Aembit — 4 operation(s) for credential provider (deprecated).
- [Aembit Credential Provider Integration API](https://apis.io/apis/aembit/aembit-credential-provider-integration-api/) — The Credential Provider Integration API from Aembit — 3 operation(s) for credential provider integration.
- [Aembit Credential Provider v2 API](https://apis.io/apis/aembit/aembit-credential-provider-v2-api/) — The Credential Provider v2 API from Aembit — 4 operation(s) for credential provider v2.
- [Aembit Credentials API](https://apis.io/apis/aembit/aembit-credentials-api/) — The Credentials API from Aembit — 1 operation(s) for credentials.
- [Aembit Discovery Integration API](https://apis.io/apis/aembit/aembit-discoveryintegration-api/) — The DiscoveryIntegration API from Aembit — 2 operation(s) for discoveryintegration.
- [Aembit Discovery Server Workload Draft API](https://apis.io/apis/aembit/aembit-discoveryserverworkloaddraft-api/) — The DiscoveryServerWorkloadDraft API from Aembit — 1 operation(s) for discoveryserverworkloaddraft.
- [Aembit Health API](https://apis.io/apis/aembit/aembit-health-api/) — The Health API from Aembit — 1 operation(s) for health.
- [Aembit Integration API](https://apis.io/apis/aembit/aembit-integration-api/) — The Integration API from Aembit — 2 operation(s) for integration.
- [Aembit Integration v2 API](https://apis.io/apis/aembit/aembit-integration-v2-api/) — The Integration v2 API from Aembit — 2 operation(s) for integration v2.
- [Aembit Log Stream API](https://apis.io/apis/aembit/aembit-log-stream-api/) — The Log Stream API from Aembit — 2 operation(s) for log stream.
- [Aembit MFA SignOn Policy API](https://apis.io/apis/aembit/aembit-mfa-signon-policy-api/) — The MFA SignOn Policy API from Aembit — 1 operation(s) for mfa signon policy.
- [Aembit Policy API](https://apis.io/apis/aembit/aembit-policy-api/) — The Policy API from Aembit — 1 operation(s) for policy.
- [Aembit Resource Set API](https://apis.io/apis/aembit/aembit-resource-set-api/) — The Resource Set API from Aembit — 2 operation(s) for resource set.
- [Aembit Role API](https://apis.io/apis/aembit/aembit-role-api/) — The Role API from Aembit — 2 operation(s) for role.
- [Aembit Routing API](https://apis.io/apis/aembit/aembit-routing-api/) — The Routing API from Aembit — 2 operation(s) for routing.
- [Aembit Server Workload API](https://apis.io/apis/aembit/aembit-server-workload-api/) — The Server Workload API from Aembit — 2 operation(s) for server workload.
- [Aembit SignOn Policy API](https://apis.io/apis/aembit/aembit-signon-policy-api/) — The SignOn Policy API from Aembit — 1 operation(s) for signon policy.
- [Aembit SSO Identity Provider API](https://apis.io/apis/aembit/aembit-sso-identity-provider-api/) — The SSO Identity Provider API from Aembit — 3 operation(s) for sso identity provider.
- [Aembit SSO SignOn Policy API](https://apis.io/apis/aembit/aembit-sso-signon-policy-api/) — The SSO SignOn Policy API from Aembit — 1 operation(s) for sso signon policy.
- [Aembit Standalone Certificate Authority API](https://apis.io/apis/aembit/aembit-standalone-certificate-authority-api/) — The Standalone Certificate Authority API from Aembit — 2 operation(s) for standalone certificate authority.
- [Aembit Standalone TLS Decrypt API](https://apis.io/apis/aembit/aembit-standalone-tls-decrypt-api/) — The Standalone TLS Decrypt API from Aembit — 1 operation(s) for standalone tls decrypt.
- [Aembit TLS Decrypt API](https://apis.io/apis/aembit/aembit-tls-decrypt-api/) — The TLS Decrypt API from Aembit — 1 operation(s) for tls decrypt.
- [Aembit Trust Provider API](https://apis.io/apis/aembit/aembit-trust-provider-api/) — The Trust Provider API from Aembit — 2 operation(s) for trust provider.
- [Aembit Trust Provider Secret API](https://apis.io/apis/aembit/aembit-trust-provider-secret-api/) — The Trust Provider Secret API from Aembit — 2 operation(s) for trust provider secret.
- [Aembit User API](https://apis.io/apis/aembit/aembit-user-api/) — The User API from Aembit — 3 operation(s) for user.
- [Aembit Workload Event API](https://apis.io/apis/aembit/aembit-workload-event-api/) — The Workload Event API from Aembit — 2 operation(s) for workload event.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Aembit Event Surface](https://apis.io/asyncapis/aembit/aembit-event-surface/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Aembit MCP Server](https://apis.io/servers/aembit/aembit-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Aembit Agentic Access](https://apis.io/agentic-access/aembit/aembit-agentic-access/)

#### Overlays (39)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aembit Access Authorization Event Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-access-authorization-event-api-phrasing-overlay/)
- [Aembit Access Condition Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-access-condition-api-phrasing-overlay/)
- [Aembit Access Condition V2 Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-access-condition-v2-api-phrasing-overlay/)
- [Aembit Access Policy Deprecated Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-access-policy-deprecated-api-phrasing-overlay/)
- [Aembit Access Policy V2 Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-access-policy-v2-api-phrasing-overlay/)
- [Aembit Agent Controller Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-agent-controller-api-phrasing-overlay/)
- [Aembit Audit Log Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-audit-log-api-phrasing-overlay/)
- [Aembit Auth Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-auth-api-phrasing-overlay/)
- [Aembit Client Workload Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-client-workload-api-phrasing-overlay/)
- [Aembit Cloud Overlay](https://apis.io/overlays/aembit/aembit-cloud-overlay/)
- [Aembit Compliance Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-compliance-api-phrasing-overlay/)
- [Aembit Content Security Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-content-security-api-phrasing-overlay/)
- [Aembit Credential Provider Deprecated Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-credential-provider-deprecated-api-phrasing-overlay/)
- [Aembit Credential Provider Integration Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-credential-provider-integration-api-phrasing-overlay/)
- [Aembit Credential Provider V2 Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-credential-provider-v2-api-phrasing-overlay/)
- [Aembit Credentials Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-credentials-api-phrasing-overlay/)
- [Aembit Discoveryintegration Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-discoveryintegration-api-phrasing-overlay/)
- [Aembit Discoveryserverworkloaddraft Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-discoveryserverworkloaddraft-api-phrasing-overlay/)
- [Aembit Edge Overlay](https://apis.io/overlays/aembit/aembit-edge-overlay/)
- [Aembit Health Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-health-api-phrasing-overlay/)
- [Aembit Integration Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-integration-api-phrasing-overlay/)
- [Aembit Integration V2 Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-integration-v2-api-phrasing-overlay/)
- [Aembit Log Stream Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-log-stream-api-phrasing-overlay/)
- [Aembit Mfa Signon Policy Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-mfa-signon-policy-api-phrasing-overlay/)
- [Aembit Policy Api Phrasing Overlay](https://apis.io/overlays/aembit/aembit-policy-api-phrasing-overlay/)
- …and 14 more published on APIs.io

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Aembit Authentication](https://apis.io/security/aembit/aembit-authentication/)
- [Aembit Domain Security](https://apis.io/security/aembit/aembit-domain-security/)
- [Aembit Trust Center](https://apis.io/security/aembit/aembit-trust-center/)
- [Aembit Vulnerability Disclosure](https://apis.io/security/aembit/aembit-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Aembit Plans Pricing](https://apis.io/plans/aembit/aembit-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Aembit Rate Limits](https://apis.io/rate-limits/aembit/aembit-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://aembit.io/)
- [Documentation](https://docs.aembit.io/)
- [Getting started](https://docs.aembit.io/get-started/quickstart/)
- [API reference](https://docs.aembit.io/dev-guide/api/)
- [Pricing](https://aembit.io/pricing/)
- [Sign up](https://useast2.aembit.io/signup)
- [Support](https://support.aembit.io/hc/en-us)
- [Changelog](https://docs.aembit.io/changelog/)
- [Blog](https://aembit.io/blog/)
- [Security](https://docs.aembit.io/get-started/security-posture/security-compliance/)
- [Compliance](https://docs.aembit.io/get-started/security-posture/security-compliance/)
- [Trust centre](https://trust.aembit.io/)
- [Terms of service](https://aembit.io/terms-of-service/)
- [Privacy policy](https://aembit.io/privacy-policy/)
- [GitHub](https://github.com/Aembit)
- [Status](https://status.aembit.io/)

## API Evangelist rating

**Kin Score 72.6** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 68.3 |
| Contract quality | 60.5 |
| Contract governance | 18.2 |
| Operational transparency | 84.2 |
| Developer ergonomics | 76.8 |
| Access clarity | 85.5 |

**Agent readiness 52.7** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | templated |
| Auth Clarity | served (partial credit) |
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
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aembit/](https://apis.io/providers/aembit/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Aembit: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aembit/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
