---
name: Govern AI agent access to MCP servers
description: Use Access Policies, Access Conditions and Content Security to control which AI agents may reach which MCP servers, and observe the result in workload events.
api: openapi/aembit-cloud-api-openapi.yml
operations:
  - post-client-workload
  - post-server-workload
  - post-access-condition2
  - post-content-security
  - get-content-security-list
  - post-access-policy-v2
  - get-workload-events
---

# Govern AI agent access to MCP servers

Aembit treats an AI agent as a Client Workload and an MCP server as a Server Workload, so agent
governance uses the same policy graph as everything else. The MCP Identity Gateway sits in the
data path and enforces it.

## Steps

1. **Register the agent as a Client Workload** — `post-client-workload`
   (`POST /api/v1/client-workloads`). MCP clients have their own identifier types: **CIMD Client
   ID** and **Redirect URI**, alongside the standard cloud and Kubernetes identifiers. Call
   `get-client-identifiers` to see what is available before choosing.

2. **Register the MCP server as a Server Workload** — `post-server-workload`
   (`POST /api/v1/server-workloads`). Aembit documents configurations for Atlassian, BigQuery,
   Databricks, FactSet, GitHub, Google Workspace, Kensho, Microsoft Enterprise and Notion MCP
   servers under `docs.aembit.io/ai-guide/mcp/identity-gateway/supported-servers/`.

3. **Add conditional access** — `post-access-condition2` (`POST /api/v2/access-conditions`).
   This is where posture from CrowdStrike or Wiz, geography and time windows narrow the grant.
   Conditional access is an **Enterprise-tier** capability on both pricing lines.

4. **Add Content Security if you need traffic inspection** — `post-content-security`
   (`POST /api/v1/content-security`), listed with `get-content-security-list`. This inspects MCP
   traffic in the Gateway request path and, with the CrowdStrike AIDR integration, returns
   allow / block / transform verdicts. Each decision is recorded as an event.

5. **Bind it together** — `post-access-policy-v2` (`POST /api/v2/access-policies`), attaching the
   client workload, the server workload, the credential provider, the access conditions and the
   content security configuration.

6. **Watch it work** — `get-workload-events` (`GET /api/v1/workload-events`), or the
   `get_workload_events` MCP tool. Filter `appProtocol` to **`MCP`** to see only agent-to-MCP
   traffic. Authorization decisions are in `get-access-authorization-events`.

## Know which MCP thing you are touching

Aembit ships three distinct MCP components. Do not conflate them:

- **Aembit MCP Server** (`https://{tenantId}.mcp.useast2.aembit.io/mcp`) — Aembit's *own*
  read-only server exposing three event-query tools. This is what you point Claude, Copilot or
  Visual Studio at to ask questions about your tenant.
- **MCP Identity Gateway** — the data plane that brokers *your agents'* access to *third-party*
  MCP servers. Managed or self-hosted.
- **MCP Authorization Server** — OAuth 2.1 authorization for MCP clients and servers, driven by
  Access Policies.

Only the first is an Aembit API surface; the other two are enforcement products.

## Rules

- **Blended Identity means two subjects.** Aembit combines the human user identity and the agent
  workload identity into one decision, so authorization events distinguish human-initiated from
  agent-initiated access. Do not assume a single actor when reading them.
- **Agentic AI tiers cap what you can build.** Starter allows 3 AI agents, 1 MCP Identity Gateway
  and 5 MCP authorization policies; Teams raises it to 10–500 agents with unlimited policies.
- **No idempotency, no undo.** Same as everywhere else on this API: a retried POST duplicates,
  and a DELETE is permanent. Use `isActive: false` to disable a policy you might want back.
