# Interactive playground — normative proposal

**Feature:** F-PLAYGROUND-001 | **Status:** proposed for requester approval | **Requirements:** R-39, R-39a, R-39b, R-39c, R-39d | **Acceptance:** A-39 through A-39d

## Goal and boundaries

Provide a **fully static, browser-executed playground** capable of exercising every approved client-side search feature, including positive, negative and boundary behavior. It uses the same public API and the same release artifacts as real integrators; mock-only demonstrations do not qualify as implemented feature coverage. It is a diagnostic and educational consumer, **not** a substitute for executable contract tests.

The playground is shipped with public, independently authored fixtures. No login, backend search API or required remote service is permitted. Editing fixture content must never mutate deployed production datasets. The default deployment uses a React/TypeScript shell, but the underlying engine remains framework independent. Build-only behavior must be exercised through prebuilt fixtures plus a local sandbox builder, with unsupported build options clearly marked; do not pretend a browser-only control validates the entire offline publisher.

## User workflows

1. **Explore:** open a feature catalogue grouped by indexing, query, ranking, filters/facets, language, navigation, lifecycle, security and performance. See description, linked R/A IDs, implementation status, preconditions and sample data.
2. **Choose data:** load a small controlled example, a multilingual corpus, a structured catalog or an approved benchmark fixture. See dataset version, document count, language partitions and active field definitions.
3. **Edit data safely:** edit, duplicate, remove or add public sample records, field/facet configuration, synonym sets and pins. Validate edits and rebuild in an isolated in-memory dataset or select a generated static fixture. No production index writes.
4. **Issue query:** enter text, choose locale, operator, fields/boosts, prefix/phrase, fuzzy tolerance, synonyms, filters (terms/exact/range/hierarchy/geo), pins, sorting, page/offset and result size. Expose only options supported by the chosen dataset.
5. **Inspect:** view ranked hits, excerpts/highlight spans, scores or relevance signals, applied settings, selected facets and counts, distance, suggestions, timing, active dataset ID, raw JSON request/response and typed errors.
6. **Test difficult cases:** replay no-match, typo, escaped/malicious text, unknown filter, invalid geo/range, malformed dataset, cancellation, disposal, concurrent queries and truncated/incompatible publication in a safe sandbox.
7. **Reproduce:** reset to deterministic defaults; copy a minimal sanitized reproduction containing fixture ID/version, configuration and request. Optional URL state is permitted only when it contains non-sensitive public fixture references, never arbitrary raw queries or pasted content.
8. **Verify coverage:** inspect a feature-to-requirement matrix showing each adopted R-ID, linked runnable scenario and automated acceptance test. Mark planned/deferred or impossible-to-demo aspects explicitly. Interactive success must not mark a requirement verified.

## Required views and controls

| Panel | Inputs / actions | Observable output | Requirement coverage |
| --- | --- | --- | --- |
| Corpus & publisher | structured records, rendered-HTML examples, noindex, canonical URL, sections, field definitions, local rebuild, fixture selection | normalized public records, version, warnings, generated descriptor | R-01–R-07, R-21, R-30, R-37 |
| Text search | text, phrase, prefix, AND/OR, locale and field selection | matched hits, total, ordered IDs, empty/parse errors | R-08, R-09, R-23, R-24 |
| Relevance | field/term/document boosts, fuzzy tolerance, equivalent/directional/multiword synonyms, pins, exclusive mode | scores, rank ordering, pinned flags, did-you-mean, diff view vs baseline settings | R-03, R-10–R-13, R-16 |
| Facets & filtering | terms, multiple filters, numeric interval, hierarchy, geo center/radius, distance sort | contextual counts, chips, selected values, distance, excluded documents | R-18–R-20 |
| Result presentation | paging, scalar sorting, highlight on/off, section anchors, snippet length | stable page, raw result JSON, highlighted text spans, navigation targets | R-14, R-15, R-21 |
| Discovery | input prefix, suggestion bounds, spelling | suggestions grounded in dataset; empty explanation | R-11, R-16 |
| Lifecycle & errors | load/reload/dispose, cancel, concurrent requests, defective fixture selection, network failure simulation | ready/loading/error state, operation timings, typed error, no stale results | R-04–R-06, R-25–R-29, R-37 |
| Security & privacy | untrusted string fixture, blocked URL, unknown field, public field review, network inspector summary | escaped text, denied unsafe operations, public-field declaration, no query upload | R-30–R-32 |
| Diagnostics & accessibility | active fixture manifest, request/response, browser timings, viewport and keyboard flows | transfer/parse/query timings, typed errors, status announcements, focus | R-33–R-36, R-38 |
| Coverage | feature list, R-ID and A-ID links, state, preset cases, reset/replay | all approved capabilities discoverable and reproducible; missing cases flagged | R-39–R-39d |

The table covers **the complete adopted feature surface**, not just the original implementation's current state. R-17, R-22, R-29 and R-38 are extension features; display their pending status without fabricating working controls until approved and implemented. A feature is playable only if its own implementation/fixture supports it.

## UX requirements

- Usable on small-screen mobile, touch and keyboard; responsive panes rather than horizontal-only tables.
- Accessible input labels, focus indication, button semantics and status/error announcements; test rendered UI against WCAG 2.2 AA.
- Every search run exposes *both* human-readable hits and raw structured output; preview is safely text-rendered and never executes content.
- Show non-blocking progress on costly dataset construction and explicit cancellations; no indefinite loading indicators.
- Expose actual data/implementation behavior, never a UI-only simulation labeled as a passing search result.
- No default telemetry, external scripts uploading queries, or network writes. Static asset GETs may be observable by the host; document this.

## Sample scenarios

| Scenario ID | Primary behavior | Sample interaction |
| --- | --- | --- |
| PG-01 | Exact vs approximate | Query an exact label, toggle fuzzy and compare rankings |
| PG-02 | Phrase and prefix | Search a quoted contiguous phrase versus non-contiguous words; then prefix |
| PG-03 | Synonyms | Toggle directional/multiword expansion and inspect matching IDs |
| PG-04 | Pinning | Toggle pin/exclusive flag, activate a filter and confirm no forbidden result |
| PG-05 | Faceting | Select category, price range and hierarchy; observe contextual counts |
| PG-06 | Geosearch | Change radius and sort by distance; inspect boundary points |
| PG-07 | Pagination | Change offset/sort and ensure stable nonoverlapping pages |
| PG-08 | Languages | Compare inflections across en/de/sv/nl/nb/nn; select unsupported locale |
| PG-09 | Snippet safety | Query HTML-shaped content; inspect literal highlights/escaped rendering |
| PG-10 | Editable dataset | Add a public record, rebuild locally, search it, reset to baseline |
| PG-11 | Invalid data | Select malformed descriptor, invalid origin and duplicate ID; inspect errors |
| PG-12 | Lifecycle | Cancel in-flight request, retry another, dispose and verify failure |
| PG-13 | Performance | Compare cold/warm timing and displayed count; capture browser/env |
| PG-14 | Publication | Switch release A/B and verify generation isolation |
| PG-15 | Coverage | Navigate all requirement links; find missing or deferred demos without false claims |
| PG-16 | Security | Prove unknown filters, unsafe URLs, injection strings and no query upload |

These are representative presets. The coverage matrix must additionally enumerate every adopted R-ID and criterion; an ID not represented by a playable scenario must be listed as a documented non-interactive verification obligation rather than silently omitted.

## Verification

- **A-39** Every supported feature has an interactive entry with visible R/A identifiers, preconditions, expected result and at least one runnable scenario; deferred features have status labels.
- **A-39a** Editing sample records changes subsequent local results; reset reproduces original results; no publish/network-write side effects.
- **A-39b** Controls exist and work for all adopted functional features; rendered output agrees with raw response data; impossible browser-only cases link to publisher-specific fixtures.
- **A-39c** Scenario reset/replay is deterministic; copied reproduction is sufficient to repeat behavior without private data or leaked queries.
- **A-39d** Responsive keyboard/screen-reader flows pass the adopted WCAG 2.2 AA checks; untrusted content is inert and browser network inspection shows no query-upload path.

Release gate: **100% of adopted product R-IDs** have a traceable playground entry or an explicit, reviewed rationale for non-interactivity. Every directly interactive feature has at least one passing browser-level scenario and one negative/boundary scenario where applicable. All automated tests must still run independently of the playground.

## Technical guidance (not product requirements)

Build the playground as a React/TypeScript static SPA. Keep its dataset adapters and visible state thin; consume the public headless package rather than importing Orama internal APIs. Playwright can automate reference scenarios. Generated fixtures may be bundled as static assets; local editing/rebuild uses only user-controlled in-memory data. The engine may use Orama, but no playground requirement depends on a particular library.
