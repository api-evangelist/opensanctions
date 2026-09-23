---
name: Keep a screening integration fresh and monitor for changes
description: >-
  Poll the OpenSanctions catalog for dataset freshness, re-screen only what changed
  using changed_since, and stay ahead of announced breaking changes.
api: openapi/opensanctions-api-openapi.yml
operations:
  - catalog_catalog_get
  - search_search__dataset__get
  - healthz_healthz_get
  - readyz_readyz_get
generated: '2026-08-27'
method: generated
source: >-
  openapi/opensanctions-api-openapi.yml plus
  https://www.opensanctions.org/docs/monitoring/ ,
  https://www.opensanctions.org/docs/data/changes/ and
  https://www.opensanctions.org/changelog/rss/
---

# Keep a screening integration fresh

Sanctions data is only useful if it is current, and a screening decision made against
last month's lists is a compliance finding waiting to happen. This skill is the
maintenance loop around the screening loop.

## Steps

1. **Poll the catalog conditionally.** `GET /catalog` (`catalog_catalog_get`) needs no
   API key and returns every dataset with `updated_at`, `last_export`, `version`,
   `entity_count` and `coverage.frequency`. It is large — roughly 1.7 MB across 477
   datasets — so **send `If-None-Match` with the ETag from your last call**. The
   operation declares a `304` "The catalog has not changed" and the live response
   carries `cache-control: public, max-age=300`. Polling it unconditionally every
   minute wastes bandwidth on both ends for no new information.

2. **Watch the fields that matter.** `current` / `outdated` / `index_stale` at the top
   of the response tell you whether the served index is behind the published data. Per
   dataset, `deprecated` and `deprecation` carry the change policy into the data
   itself — a dataset you depend on will be flagged there before it disappears.

3. **Re-screen incrementally.** `GET /search/{dataset}` accepts `changed_since` (an
   ISO date or datetime) so you can pull only entities updated since your last run,
   rather than re-screening the whole book. Combine with `topics`, `countries` and
   `filter` to narrow further. The provider's continuous-monitoring pattern is
   documented at https://www.opensanctions.org/docs/monitoring/ .

4. **Page correctly.** `limit`/`offset`, and read `total` as `{value, relation}` — not
   an integer. `relation` distinguishes an exact count from a lower bound, so a client
   that reads `total` as a number will mis-page deep result sets.

5. **Check readiness, not just liveness.** `GET /healthz` returns 200 whenever the
   service is up; `GET /readyz` returns `503` while the search index is still loading.
   Gate a batch run on `readyz`, not `healthz`.

6. **Subscribe to change notices.** Breaking changes are announced ahead of time with
   real windows — 3 months for hosted-API deprecations, data-model renames and export
   format changes, 2 months for dataset removals. They land at
   https://www.opensanctions.org/changelog/ with an RSS feed at
   https://www.opensanctions.org/changelog/rss/ , and each notice carries a forward
   effective date. **There is no `Sunset` or `Deprecation` response header**, so
   nothing in the HTTP response will ever warn you — the feed is the only signal.
   Poll it, or subscribe a human to the monthly newsletter.

7. **Subscribe to status per component.** https://status.opensanctions.org/ exposes
   RSS, Atom, JSON, webhook and Slack, with separate components for the Matching API,
   Search API, Fetch entity API, Statement-based data API and the dataset publication
   pipeline. Subscribe to the components you actually call.

## Cost

`/catalog`, `/healthz` and `/readyz` are unauthenticated and free. `/search` is billed
at EUR 0.10 per request, so an incremental `changed_since` sweep costs one query per
page — page size, not page count, is where the savings are.

## Reversibility

Read-only. Nothing in this loop writes.
