# Specification authority and approval record

**Feature:** independent client-side search engine with a full-feature playground

**Baseline revision:** proposed 0.1.0, 2026-11-14
**Status:** not approved
**Approver:** repository requester or explicitly delegated maintainer
**Implementation:** not started

## Authority and interpretation

- [SYSTEM.md](SYSTEM.md) is the standalone narrative product contract.
- [system.yaml](system.yaml) is its machine-readable representation under the [System Specification metamodel](https://github.com/ktjn/system-specification/blob/main/MODEL-SCOPE.md).
- [ACCEPTANCE.md](ACCEPTANCE.md) specifies independent verification, including negative and boundary cases.
- [PLAYGROUND.md](PLAYGROUND.md) specifies the required interactive test experience.
- [../PLAN.md](../PLAN.md) is **non-normative implementation guidance**; Orama is an implementation choice.
- Any discrepancy between documents is a **review blocker**, not permission to pick the easiest interpretation.
- A reference validator result is informative and does not signify requester approval.

## Decisions required before implementation

| Decision | Proposed baseline | Status |
| --- | --- | --- |
| D-01 Product boundary | Public data, static HTTP deployment, local/browser lexical search, no hosted query API | Pending |
| D-02 Compatibility | Independent headless API and dataset format; no predecessor API/manifest compatibility | Pending |
| D-03 Search semantics | R-08–R-24 plus R-10a/R-13a/R-19a/R-23a/R-23b: explicit boosts, pin modes, geo distance, language-specific stemming and configurable stopwords | Pending |
| D-04 Feature scope | R-01–R-06, R-08–R-16, R-18–R-21, R-23–R-28, R-30–R-37 and R-39–R-39d are MVP; R-07, R-17, R-22, R-29, R-38 are extensions | Pending |
| D-05 Playground | Static, interactive, editable public fixtures; **all adopted requirements** traceable to scenarios; React/TypeScript implementation candidate | Pending |
| D-06 Performance | 2k/10k/50k corpus benchmarks, representative devices/browsers; agree p95/bytes/heap/long-task budgets using measured spike | Pending |
| D-07 Relevance | Independent judged domains/locales, nDCG@5/MRR/recall/precision/zero-result rate, approved thresholds | Pending |
| D-08 Packaging and dependency | Pin stable Orama 3.x only after public API/serializer feasibility spike; ensure license review and SBOM | Pending |
| D-09 Security and privacy | Public-only content, query-local behavior, safe rendering/URLs, no default analytics | Pending |

## Review workflow

1. **Discovery:** review actors, capabilities, invariant and failure-mode completeness.
2. **Architecture:** review logical components, dependency/capability graph, data ownership/classification, independent static publisher/runtime boundary.
3. **Verification:** review complete R-ID and A-ID mapping, playable PG scenarios, negative/boundary cases, risks and numeric budget plan.
4. **Specification approval:** record approver, spec revision/commit, accepted R/A IDs, exceptions and dependency/risk assumptions. Only then initiate implementation.
5. **Implementation acceptance:** evidence must bind to Orama implementation source and tests. A passing draft model or playground is not release proof.

A change to accepted behavior or tests returns to its affected specification gate for reapproval. A defect against approved behavior is corrected in implementation, not by weakening the approved test.

## Unresolved questions

- Distinguish genuine phrase matching from concatenated full-text term matching; keep implementation free to use an adapter if necessary.
- Determine whether serialized Orama snapshots or client-built indexes meet the resource envelope; pick after benchmarks.
- Define performance budgets and acceptable relevance regressions before declaring a release candidate.
- Decide whether dataset editing in the playground supports HTML parsing in-browser or only structured records with separate HTML fixtures; both ingestion behaviors must still be independently verified.
- Define the small-screen and screen-reader test matrix for the playground and reference integration.

## Approval record (to be completed by requester)

- Decision: **pending**
- Approver: **pending**
- Approved revision/commit: **pending**
- Approved requirements/acceptance suite: **pending**
- Accepted exceptions and residual risks: **none recorded**
- Evidence threshold agreement: **pending**

Do not infer approval from PR creation, a green reference-tool check, or the presence of this file.
