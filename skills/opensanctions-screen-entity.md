---
name: Screen a person or company against sanctions and PEP lists
description: >-
  Use the OpenSanctions matching API to check one or many entities against sanctions,
  watchlist and politically-exposed-person data, with scored, explainable results.
api: openapi/opensanctions-api-openapi.yml
operations:
  - match_match__dataset__post
  - algorithms_algorithms_get
  - catalog_catalog_get
generated: '2026-08-27'
method: generated
source: >-
  openapi/opensanctions-api-openapi.yml plus
  https://www.opensanctions.org/docs/api/matching/ and
  https://www.opensanctions.org/docs/api/faq/
---

# Screen an entity against sanctions and PEP data

## Before you start

- Base URL is `https://api.opensanctions.org`. Authenticate with
  `Authorization: ApiKey <key>` — the literal word `ApiKey`, **not** `Bearer`.
  A missing key returns `401 {"detail":"No API key provided."}`.
- Use `match_match__dataset__post`, never the website's search page. The provider
  states plainly that automated queries against the website risk IP bans and legal
  liability; the matching API is the supported path.
- **Use `match`, not `search`.** Even with partial input — a name alone, a name plus a
  country — `match` returns scored, ranked candidates. `search_search__dataset__get`
  is for a human typing into a search box and returns unscored entities. Reaching for
  `search` because the input is sparse is the most common mistake against this API.

## Steps

1. **Choose the dataset scope.** The `dataset` path parameter is a collection or
   source name. `sanctions` for sanctions-only screening, `default` for the combined
   sanctions + PEP + watchlist collection. Call `catalog_catalog_get`
   (`GET /catalog`, no key needed) if you need to confirm what exists or how fresh it
   is — it returns every dataset with `updated_at`, `entity_count` and `coverage`.

2. **Build the query-by-example batch.** `POST /match/{dataset}` takes a `queries`
   map. Each key is a name **you** choose so you can correlate the response; each
   value is an entity example with an FtM `schema` and a `properties` map whose
   values are always arrays:

   ```json
   {"queries": {
     "customer-1": {"schema": "Person",
                    "properties": {"name": ["John Doe"],
                                   "birthDate": ["1975-04-21"],
                                   "nationality": ["us"]}},
     "vendor-1":   {"schema": "Company",
                    "properties": {"name": ["Brilliant Amazing Limited"],
                                   "jurisdiction": ["hk"],
                                   "registrationNumber": ["84BA99810"]}}
   }}
   ```

   Precision follows detail. The provider names the properties that carry the most
   weight: **Person** — `name`, `birthDate`, `nationality`, `idNumber`, `address`;
   **Organization** — `name`, `country`, `registrationNumber`, `address`;
   **Company** — `name`, `jurisdiction`, `registrationNumber`, `address`,
   `incorporationDate`.

3. **Set the algorithm and the threshold.** Pass `?algorithm=best` — it selects the
   highest-quality algorithm available. Pin an explicit algorithm only when you need
   stable scores for a regulatory reason; avoid `logic-v1`. `threshold` (default
   `0.7`) is the score above which a result counts as a match. The `cutoff` parameter
   is deprecated in the spec — use `threshold`.

4. **Read the response by your own query keys.** `responses` is keyed by the names you
   sent. Each entry carries `results` (scored entities), `total` and the echoed
   `query`. Every result has `score`, a boolean `match`, and `explanations` — a list
   of per-feature results with `detail`, `score`, `query` and `candidate`. **Keep the
   explanations.** They are the audit trail that tells a reviewer why the system said
   yes, and a screening decision without one is not defensible.

5. **Enrich a hit before deciding.** A score is not an adjudication. Fetch the full
   record with `fetch_entity_entities__entity_id__get` and walk its relationships —
   see the `opensanctions-investigate-entity` skill.

## Cost and limits

- A batch may carry up to **100 queries**, and **each query is billed individually**
  at EUR 0.10 — a 100-entity batch costs EUR 10, not EUR 0.10. Size batches
  deliberately.
- Non-2xx responses are never billed. `/entities` and `/statements` are free.
- Quota is **monthly**, not per-second. There are no `RateLimit-*` or `Retry-After`
  headers to read: a `429` means the month's quota is gone and it will not clear
  until the first of the next month. Do not write a retry loop around a 429 — it
  cannot succeed. Alert a human instead.
- Above ~2M queries/month or 200k requests/hour, contact OpenSanctions first.

## Errors

`400` invalid query · `401` no/bad key · `422` parameter validation, with a
`detail[]` array of `{loc, msg, type}` naming the bad field · `429` monthly quota
exhausted · `500` server error (check https://status.opensanctions.org/).
The envelope is `{"detail": ...}` — plain JSON, not RFC 9457 problem+json.

## Reversibility

Nothing to undo. This API creates and mutates nothing; a screening call is a read.
The only lasting effect is the metered charge on a successful call, which is why
batch sizing — not rollback — is the thing to get right before you send.
