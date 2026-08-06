---
name: Sync 7pace Timetracker worklogs
description: >-
  Read, create, update and incrementally sync time entries in 7pace Timetracker for Jira (an Appfire
  product) — the correct pattern for keeping a payroll, billing or BI system in step.
api: openapi/appfire-7pace-timetracker-v2-openapi-original.yml
generated: '2026-08-06'
method: generated
source: openapi/appfire-7pace-timetracker-v2-openapi-original.yml
operations:
  - "GET /api/v2/worklogs"
  - "GET /api/v2/worklogs/views/incrementalChanges"
  - "POST /api/v2/worklogs"
  - "PUT /api/v2/worklogs/{worklogId}"
  - "DELETE /api/v2/worklogs/{worklogId}"
  - "GET /api/v2/settings/customFields"
---

# Sync 7pace Timetracker worklogs

> **Note on operation references.** The 7pace OpenAPI documents declare **no `operationId` on any
> operation**, so every step below names the real `METHOD path` from the spec instead. Do not invent
> operationIds for this API.

## Before you start

- **Base URL:** `https://timehubjra.7pace.com`. The spec declares `servers: [{url: "/"}]`, which is
  relative and unusable on its own.
- **Auth:** `Authorization: Bearer <token>` — a JWT created in Timetracker under Settings → API
  Tokens, with a mandatory expiration date. Note this is the opposite convention to Appfire's OKR API,
  which forbids the `Authorization` header. Do not share a token or a client between the two.
- **Version:** use `v2`. `v1` is still served but has no published sunset date, and the change feed was
  renamed between them (`/api/v1/worklogs/changes` → `/api/v2/worklogs/views/incrementalChanges`).

## Steps — first full load

1. `GET /api/v2/worklogs` with the filters you need: `externalItemId` (the Jira work item),
   `assigneeId`, `authorId`, and the range filters `startedAt.start` / `startedAt.end`,
   `editedAt.start` / `editedAt.end`, `createdAt.start` / `createdAt.end`.
2. Page with the cursor pair: read `pageInfo.endCursor` and `pageInfo.hasNextPage` from the response,
   then pass the cursor back as `after`. Walk backwards with `before` if you need to.
3. Store `id`, `externalItemId`, `assigneeId`, `authorId`, `startedAt`, `duration` and `customFields`
   per worklog. `externalItemId` is the join key back to Jira — Jira, not 7pace, is the system of
   record for what the time was spent on.

## Steps — incremental sync (do it this way, not by re-listing)

1. `GET /api/v2/worklogs/views/incrementalChanges` with the same filter and cursor parameters.
2. This projection returns `ChangedWorklog`, which carries **`isDeleted`**. The plain `/worklogs` list
   does not, so a delete is invisible to a re-list and your copy will silently drift. Always drive
   incremental sync from this endpoint.
3. Apply upserts for `isDeleted: false` and tombstones for `isDeleted: true`, then persist the last
   `endCursor` as your watermark.

## Steps — writing time

1. `POST /api/v2/worklogs` with `comment`, `startedAt`, `assigneeId`, `duration`, `externalItemId` and
   any `customFields`. Returns `200` with the created worklog.
2. `PUT /api/v2/worklogs/{worklogId}` to amend one. `DELETE /api/v2/worklogs/{worklogId}` returns
   `204`.
3. Read the account's custom-field definitions with `GET /api/v2/settings/customFields` before writing
   `customFields`; mandatory fields will otherwise fail validation with `400`.

## Rules

- **No idempotency key exists on any write.** A retried `POST` after a timeout double-logs time — a
  billing defect, not a cosmetic one. On a timeout, do not retry: query the incremental-changes feed
  for the window you just wrote and only re-post if your entry is absent.
- **Migrated worklogs are a separate lane.** `POST /api/v2/worklogs/migrated` and
  `DELETE /api/v2/worklogs/migrated/{worklogId}` exist for imported history; deleting a non-migrated
  worklog through that path returns `400 The worklog is not migrated`.
- **Error bodies are unstructured.** The spec declares a `ProblemDetails` schema but references it from
  no response, and errors come back as plain `application/json`. Branch on status: `400` validation,
  `401` bad token, `403` insufficient permission for the token's user, `404` missing worklog or
  assignee, `500` server error. See `errors/appfire-problem-types.yml`.
- **No rate-limit contract is published** for this API. Be conservative and serialise bulk writes.
