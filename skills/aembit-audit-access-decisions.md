---
name: Audit access decisions and workload activity
description: Query Aembit's three event streams — audit logs, authorization events and workload events — through the Cloud API or the read-only MCP Server.
api: openapi/aembit-cloud-api-openapi.yml
operations:
  - get-audit-logs
  - get-audit-log
  - get-access-authorization-events
  - get-access-authorization-event
  - get-workload-events
  - get-workload-event
---

# Audit access decisions and workload activity

Three separate event families answer three different questions. Pick the right one before you
start paginating.

| Question | Stream | Cloud API | MCP tool |
|---|---|---|---|
| Who changed the configuration? | Audit Log | `get-audit-logs` | `get_audit_logs` |
| Was this access allowed, and why? | Access Authorization Event | `get-access-authorization-events` | `get_auth_events` |
| What did the workload actually connect to? | Workload Event | `get-workload-events` | `get_workload_events` |

## Two ways in, and the MCP one is better specified

**Via the Cloud API** — `GET /api/v1/audit-logs`, `/api/v1/authorization-events`,
`/api/v1/workload-events`, each with a `GET .../{id}` sibling for a single record
(`get-audit-log`, `get-access-authorization-event`, `get-workload-event`). Paginate with `page`
and `per-page`. The `filter`, `order` and `group-by` parameters are bare strings with **no
published grammar** — treat them as unusable.

**Via the MCP Server** — `https://{tenantId}.mcp.useast2.aembit.io/mcp`, read-only, three tools.
Same data, but with **closed enums the REST contract does not publish**:

- `get_audit_logs`: `orderBy` ∈ {CreatedAt, Category, ActorDisplayName, Activity, Target,
  OutcomeResult, Severity}; `severity` ∈ {Info, Warn, Alert}; `category` ∈ {Tenant, Users,
  Authentication, Workloads, AccessPolicies, Agents, CredentialProvider, TrustProvider, …};
  `spanLastDays` (default 30), `spanLastMinutes`, `startDate`/`endDate`.
- `get_auth_events`: `eventType` ∈ {Request, Authorization, Credential}; `severity` ∈ {Error,
  Alert, Warn, Info}; `spanLastHours` (default 24).
- `get_workload_events`: `appProtocol` ∈ {Redshift, HTTP, MySQL, Postgres, Redis, Snowflake, TCP,
  OracleDatabase, **MCP**}; `sourceWorkload`/`targetWorkload` as UUID arrays.

If you are building an agent, use the MCP Server: the filters are typed, and it cannot mutate
anything.

## Rules

- **Retention will silently truncate your query.** Event log retention is **24 hours** on the
  Starter tiers and Workloads Teams, 7 days on Agentic AI Teams, custom on Enterprise. The
  `spanLastDays` parameter defaults to 30 and will happily accept it — you will just get back
  whatever the tier retained. Check the tier before concluding a period was quiet.
- **`perPage` hard-caps at 100** on the MCP Server; larger values are silently reduced. Loop on
  `page` until you have seen `recordsTotal`.
- **The MCP Server is read-only** and must be enabled per tenant by an administrator. It cannot
  create, update or delete, and it exposes none of the 98 mutating Cloud API operations.
- **Correlate with the right field.** Authorization events carry `ContextId`; workload events
  carry `ConnectionId`. Neither is returned to you as a response header on your own API call, so
  you cannot join your request to the resulting event except by timestamp and workload.
- **For anything longer than the retention window**, configure a Log Stream instead of polling —
  see the streaming skill.
