---
name: Export Appfire OKR objectives, key results and check-ins
description: >-
  Pull the current OKR tree (objectives, key results, and their check-in updates and comments) out of
  Appfire's OKR app for Jira Cloud into a reporting system, warehouse or agent context.
api: openapi/appfire-okr-openapi-original.json
generated: '2026-08-06'
method: generated
source: openapi/appfire-okr-openapi-original.json
operations:
  - fetchObjectives
  - fetchObjectivesByIds
  - fetchKeyResults
  - fetchKeyResultsByIds
  - fetchUpdatesByEntityId
  - fetchCommentsByUpdateIds
---

# Export Appfire OKR objectives, key results and check-ins

## Before you start

- **Base URL.** Use the regional host that matches the customer's Jira Cloud data residency:
  `https://okr-ppm-prod.appfire.com` (default), `https://eu.okr-ppm-prod.appfire.com`,
  `https://au.okr-ppm-prod.appfire.com`, or `https://ca.okr-ppm-prod.appfire.com`. Getting this wrong
  returns someone else's empty tenant, not an error.
- **Auth.** Send the token in an `API-Token` header. Do **not** send `Authorization` or
  `Authentication` — the API rejects those. A completely missing header returns `400`, not `401`;
  an invalid token returns `401`.
- **Token source.** Generated in Jira under Apps → OKR for Jira → Settings → API. It cannot be
  retrieved after creation.

## Steps

1. **Pull the objective set for the period.** Call `fetchObjectives` with `startDateEpochMilli` and
   `deadlineEpochMilli` bounding the period you care about (epoch milliseconds, not ISO dates). This
   endpoint is **not paginated** — it returns the whole `ApiExportData` bundle for the window, which
   includes the `teams`, `periods`, `labels`, `okrTypes` and `customFields` lookup tables alongside
   `okrs`. Keep those lookups; the objects reference them by id only.
2. **Pull the key results the same way** with `fetchKeyResults` over the same window, or resolve them
   from each objective's `krIds` using `fetchKeyResultsByIds`.
3. **Ask for only the expansions you need.** Both `byDate` and `byIds` calls accept `expand`. An
   unrecognised expand value returns `400 Invalid expand options provided` — do not guess values,
   read them off the operation in the spec.
4. **Read progress from `percentDone`.** The provider states plainly: rely on `percentDone` on the
   objective or key result rather than recomputing it from update history.
5. **Walk the check-ins** with `fetchUpdatesByEntityId`, passing the objective or key result id as
   `entityId`. This one **is** paginated: pass `pageSize` and follow `nextCursor` into `cursor` until
   it comes back empty. `laterThan` / `earlierThan` narrow the window for incremental pulls.
6. **Fetch comment threads** with `fetchCommentsByUpdateIds` for the update ids you kept. Same cursor
   paging. Replies are threaded via `replyToCommentId`.
7. **Resolve people outside this API.** `ownerAccountId`, `collaboratorAccountIds` and
   `authorAccountId` are Jira Cloud account ids. Names and emails come from the Jira API, not from
   OKR.

## Rules

- **Back off on 429.** The API documents throttling but publishes no quota, no `Retry-After` and no
  `X-RateLimit-*` headers. Use exponential backoff with jitter and do not parallelise the export.
- **Do not assume an error body.** Every 4xx in this spec is typed as a bare object with no
  properties. Branch on the HTTP status, not on a parsed error code. See
  `errors/appfire-problem-types.yml`.
- **Read-only skill.** Nothing here mutates OKR data. Use the check-in skill for writes.
