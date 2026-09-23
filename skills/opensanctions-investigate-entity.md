---
name: Investigate an entity and audit where each claim came from
description: >-
  Fetch a full OpenSanctions entity, walk its ownership, sanctions and family edges,
  and trace every asserted property back to the source dataset that asserted it.
api: openapi/opensanctions-api-openapi.yml
operations:
  - fetch_entity_entities__entity_id__get
  - Fetch_Adjacent_Entities__entities__entity_id__adjacent_get
  - Fetch_Adjacent_by_Property__entities__entity_id__adjacent__property_name__get
  - statements_statements_get
generated: '2026-08-27'
method: generated
source: >-
  openapi/opensanctions-api-openapi.yml plus
  https://www.opensanctions.org/docs/api/entities/ ,
  https://www.opensanctions.org/docs/nested-entities/ ,
  https://www.opensanctions.org/docs/identifiers/ and
  https://www.opensanctions.org/docs/statements/
---

# Investigate an entity, and prove where its data came from

These two operations are **free** — `/entities` and `/statements` are not metered —
so investigate as deeply as the case needs without watching the meter.

## Steps

1. **Fetch the entity.** `GET /entities/{entity_id}`
   (`fetch_entity_entities__entity_id__get`). IDs look like
   `NK-aU5ybkbRFJucf8YMwsJvDw`, and come from a `match` or `search` result.

   **Follow 308 redirects.** The spec declares a `308` on this operation meaning
   "the entity was merged into another ID". OpenSanctions de-duplicates continuously,
   so an ID you stored last quarter may now redirect to a canonical record. An HTTP
   client configured not to follow redirects will silently lose the entity — this is
   the single most likely way to break a stored-ID integration against this API.

2. **Decide how much to inline.** `nested` defaults to `true` and inlines adjacent
   entities — addresses, family members, sanctions — into `properties`. Set
   `nested=false` when you want the flat record and will walk edges yourself.

3. **Walk the graph.** `GET /entities/{entity_id}/adjacent`
   (`Fetch_Adjacent_Entities__entities__entity_id__adjacent_get`) returns adjacent
   entities grouped by the FtM property that links them. Note the departure from the
   usual meaning of `limit` here: it is **per property**, not per response. To page
   one edge type deeply — every subsidiary, say — use
   `GET /entities/{entity_id}/adjacent/{property_name}`
   (`Fetch_Adjacent_by_Property__entities__entity_id__adjacent__property_name__get`)
   with `limit`/`offset`.

4. **Read `referents` and `target`.** `referents` lists the source IDs merged into
   this canonical entity — the merge history. `target` says whether the entity is
   itself a screening target or context pulled in around one. Do not report an entity
   as sanctioned because it is adjacent to one; check its own `topics`.

5. **Audit the provenance.** `GET /statements`
   (`statements_statements_get`) returns the atoms behind the record: one row per
   asserted property value, with `dataset` and `origin` naming who asserted it,
   `original_value` alongside the cleaned `value`, `lang`, and
   `first_seen`/`last_seen`. Filter with `canonical_id=<entity id>`, and narrow with
   `prop`, `prop_type` or `dataset`. Paginate with `limit` (default 50) / `offset`.

   This is the step that turns a hit into evidence. When a reviewer asks "which list
   says this person is sanctioned, and since when", `/statements` is the answer, and
   the `entity_id` versus `canonical_id` pair shows exactly which source record was
   merged into the one you are looking at.

   Note the endpoint is **hosted-API only** — it is not available on a self-hosted
   yente instance.

## Understanding what you read

`properties` keys are FollowTheMoney property names for the schema in `schema`, and
that vocabulary lives **outside** the OpenAPI. Resolve names, types and enums against
https://www.opensanctions.org/reference/ or https://followthemoney.tech/ — or, if you
are running the MCP server, with `describe_schema`, `describe_topics` and
`describe_countries`, which answer offline from the bundled model.

## Reversibility

Read-only. Nothing here writes, so there is nothing to reverse.
