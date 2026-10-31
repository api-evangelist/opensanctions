# OpenSanctions

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

OpenSanctions is an open database of international sanctions, watchlists, criminal designations and politically exposed persons (PEPs), published as a screening API, bulk data downloads and MIT-licensed open-source software from Berlin. It consolidates hundreds of primary government sources — OFAC, the EU consolidated list, UN Security Council, UK FCDO, procurement debarment registers, regulatory enforcements and national PEP registers — into a single de-duplicated entity graph expressed in the FollowTheMoney ontology it stewards. The hosted Screening API at api.opensanctions.org offers query-by-example entity matching with scored, per-feature explanations, free-text search, entity fetch with relationship traversal, statement-level provenance for every asserted value, and an OpenRefine reconciliation manifest. It is used for customer due diligence, transaction monitoring, supply-chain and vessel screening, KYB, and investigative journalism. The dataset is free for non-commercial use under CC BY-NC 4.0; commercial use is licensed, and the API is metered at EUR 0.10 per query.

**Areas:** Sanctions Screening · AML · Politically Exposed Persons · Compliance · Financial Crime · KYC · Entity Resolution · Open Data · Risk Data · Due Diligence · Public APIs · Agent-Native

## OpenSanctions on APIs.io

Everything profiled for OpenSanctions is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/opensanctions/](https://apis.io/providers/opensanctions/)** — or go straight to one of the APIs or properties below.

### APIs (4)

- [OpenSanctions Data access API](https://apis.io/apis/opensanctions/opensanctions-data-access-api/) — Endpoints for fetching data from the API, either related to individual entities, or for bulk data access in various forms.
- [OpenSanctions Matching API](https://apis.io/apis/opensanctions/opensanctions-matching-api/) — Endpoints for conducting a user-facing entity search or matching a local data store against the given dataset.
- [OpenSanctions Reconciliation API](https://apis.io/apis/opensanctions/opensanctions-reconciliation-api/) — The Reconciliation Service provides four separate endpoints that work in concert to implement the data matching API used by OpenRefine, Wikidata and several…
- [OpenSanctions System information API](https://apis.io/apis/opensanctions/opensanctions-system-information-api/) — Service metadata endpoints for health checking and getting the application metadata to be used in client applications.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [yente](https://apis.io/servers/opensanctions/yente/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Opensanctions Agentic Access](https://apis.io/agentic-access/opensanctions/opensanctions-agentic-access/)

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Opensanctions Api Overlay](https://apis.io/overlays/opensanctions/opensanctions-api-overlay/)
- [Opensanctions Data Access Api Phrasing Overlay](https://apis.io/overlays/opensanctions/opensanctions-data-access-api-phrasing-overlay/)
- [Opensanctions Matching Api Phrasing Overlay](https://apis.io/overlays/opensanctions/opensanctions-matching-api-phrasing-overlay/)
- [Opensanctions Reconciliation Api Phrasing Overlay](https://apis.io/overlays/opensanctions/opensanctions-reconciliation-api-phrasing-overlay/)
- [Opensanctions System Information Api Phrasing Overlay](https://apis.io/overlays/opensanctions/opensanctions-system-information-api-phrasing-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Opensanctions Authentication](https://apis.io/security/opensanctions/opensanctions-authentication/)
- [Opensanctions Domain Security](https://apis.io/security/opensanctions/opensanctions-domain-security/)
- [Opensanctions Trust Center](https://apis.io/security/opensanctions/opensanctions-trust-center/)
- [Opensanctions Vulnerability Disclosure](https://apis.io/security/opensanctions/opensanctions-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Opensanctions Plans Pricing](https://apis.io/plans/opensanctions/opensanctions-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Opensanctions Rate Limits](https://apis.io/rate-limits/opensanctions/opensanctions-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.opensanctions.org/)
- [Documentation](https://www.opensanctions.org/docs/)
- [Getting started](https://www.opensanctions.org/docs/api/quickstart/)
- [API reference](https://www.opensanctions.org/reference/)
- [Pricing](https://www.opensanctions.org/api/)
- [Sign up](https://www.opensanctions.org/api/)
- [Support](https://www.opensanctions.org/support/)
- [Blog](https://www.opensanctions.org/articles/rss/)
- [Security](https://www.opensanctions.org/docs/security/)
- [Compliance](https://www.opensanctions.org/docs/security/)
- [Terms of service](https://www.opensanctions.org/docs/terms/)
- [Privacy policy](https://www.opensanctions.org/docs/privacy/)
- [GitHub](https://github.com/opensanctions)
- [Status](https://status.opensanctions.org/)

## API Evangelist rating

**Kin Score 67.9** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.3 |
| Contract quality | 43.5 |
| Contract governance | 18.2 |
| Operational transparency | 76.3 |
| Developer ergonomics | 80.4 |
| Access clarity | 92.1 |

**Agent readiness 33.7** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 35.3** — Government & Public Sector

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/opensanctions/](https://apis.io/providers/opensanctions/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for OpenSanctions: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/opensanctions/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
