---
name: Stream Aembit events to a SIEM or bucket
description: Configure and manage Log Streams so audit, authorization and workload events are delivered to S3, GCS, Splunk or CrowdStrike instead of being lost to tier retention.
api: openapi/aembit-cloud-api-openapi.yml
operations:
  - get-log-streams
  - post-log-stream
  - get-log-stream
  - put-log-stream
  - patch-log-stream
  - delete-log-stream
---

# Stream Aembit events to a SIEM or bucket

Aembit publishes **no webhooks and no AsyncAPI**. Outbound event delivery is Log Streams, and it
is managed entirely through the Cloud API. This is the only durable path off the platform — on
most tiers the in-platform event store holds 24 hours.

## Destination types

`LogStreamDestinationType` is a closed enum of four. You cannot register an arbitrary callback URL.

| Type | Transport | Required fields |
|---|---|---|
| `AwsS3Bucket` | object store | `s3BucketName`, `s3BucketRegion` (optional `s3PathPrefix`) |
| `GcsBucket` | object store | `gcsBucketName`, `gcsPathPrefix`, `audience`, `serviceAccountEmail`, `tokenLifetime` (15–3600s) |
| `SplunkHttpEventCollector` | HTTP push | `hecHostPort`, `authenticationToken`, `hecSourceName` (optional `tls`, `tlsVerification`) |
| `CrowdstrikeHttpEventCollector` | HTTP push | `hecHostPort`, `apiKey`, `hecSourceName` (optional `tls`, `tlsVerification`) |

## Steps

1. **List what already exists** — `get-log-streams` (`GET /api/v1/log-streams`). Streams are
   scoped by Resource Set, so set `X-Aembit-ResourceSet` if you are not using the default.

2. **Create the stream** — `post-log-stream` (`POST /api/v1/log-streams`). Set `type` to one of
   the four destination types, `dataType` to the event family you want (e.g. `AuditLogs`),
   `name` (1–128 chars) and `isActive`. Supply the destination fields from the table above.

3. **Verify it is running** — `get-log-stream` (`GET /api/v1/log-streams/{id}`). The
   `LogStreamDTO` carries `inProgTransactionCount`, which tells you delivery is moving.

4. **Change it safely** — `patch-log-stream` (`PATCH /api/v1/log-streams/{id}`) for partial
   updates (`name`, `description`, `isActive`, `tags`). `put-log-stream` replaces the whole
   object; use PATCH unless you intend a full replacement.

## Rules

- **Turn it off, do not delete it.** `PATCH` with `isActive: false` is reversible.
  `delete-log-stream` is not — there is no restore endpoint for any Aembit entity, and deleting
  a stream loses its configuration including the destination credentials you supplied.
- **No idempotency key exists.** A retried `post-log-stream` after an ambiguous timeout creates a
  second stream shipping duplicate events to the same destination. List and match on `name`
  before retrying.
- **You are writing a secret into the request body.** `authenticationToken` (Splunk, UUID format)
  and `apiKey` (CrowdStrike, 32–40 chars) are credentials for the destination system. Source them
  from your own secret store; never commit them, and rotate at the destination if a request is
  logged.
- **The HEC destinations are an HTTP push, not a webhook.** The payload is the SIEM vendor's HEC
  envelope and the destination type is fixed. Do not plan an integration around receiving these
  at a generic endpoint.
- Vendor-specific setup: the Splunk and CrowdStrike Next-Gen SIEM guides under
  `docs.aembit.io/user-guide/administration/log-streams/`.
