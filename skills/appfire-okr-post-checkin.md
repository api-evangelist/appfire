---
name: Post an OKR check-in to Appfire OKR for Jira
description: >-
  Write a progress update (check-in) against an Appfire OKR objective or key result — the only two
  write operations the public OKR API exposes.
api: openapi/appfire-okr-openapi-original.json
generated: '2026-08-06'
method: generated
source: openapi/appfire-okr-openapi-original.json
operations:
  - updateObjective
  - updateKeyResult
  - fetchObjectivesByIds
  - fetchKeyResultsByIds
  - fetchUpdatesByEntityId
---

# Post an OKR check-in to Appfire OKR for Jira

## What this API lets you write

Exactly two things: a progress update on an **objective** (`updateObjective`) and a progress update on
a **key result** (`updateKeyResult`). You cannot create objectives, key results, teams, labels or
periods over the public API — those are UI-only. Do not attempt to synthesise them.

Both operations are named "update" but they **create a new update record**; they return `201`, and the
new check-in appears in the entity's update history. They do not patch a field in place.

## Before you start

- Send the token in the `API-Token` header (never `Authorization`). Base URL must match the tenant's
  data-residency region — see the export skill.
- Confirm the target exists first with `fetchObjectivesByIds` or `fetchKeyResultsByIds`. A bad id
  returns `404` from the write call and you will have no way to tell it apart from a permission
  problem otherwise.

## Steps

### Objective check-in
1. Call `updateObjective` with `objectiveId`, the `status` you are moving it to, and a `description`
   carrying the narrative of the check-in.
2. A `201` means the update was recorded. Read it back with `fetchUpdatesByEntityId` (`entityId` =
   the objective id) if you need the generated `updateId`.

### Key result check-in
1. Call `updateKeyResult` with `keyResultId`, `status`, the measured `newValue`, and a `description`.
2. `newValue` is interpreted against the key result's own `unit` and `currentProgressDefinition`
   (`startValue` → `desiredValue`, or a `jql`-driven definition). Read the key result first if you
   need to know which, and never convert units yourself.
3. `201` on success.

## Rules

- **There is no idempotency key.** If a call times out, you cannot safely retry it — a retry posts a
  second check-in. Instead, re-read the update history with `fetchUpdatesByEntityId` and only re-post
  if your update is genuinely absent. This is the most important rule in this skill.
- **Status meanings:** `400` = malformed body or a missing `API-Token` header; `401` = invalid token;
  `403` = the token's user lacks permission on that objective or key result; `404` = no such id.
- **Back off on 429.** Throttling is documented in prose with no quota and no `Retry-After`.
- **Never batch blindly.** There is no bulk check-in endpoint; a loop over objectives is N separate
  non-idempotent writes. Log each id you have already posted so a resumed run does not double-post.
