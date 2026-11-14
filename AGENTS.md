# Contract-first agent workflow

This is a greenfield, independent implementation governed by the **proposed** contract artifacts in `spec/` and the gated plan in `PLAN.md`. The methodology follows https://github.com/ktjn/system-specification, in particular `MODEL-SCOPE.md`, `GREENFIELD.md`, `FEATURE.md`, `REPLACEMENT.md` and `COMPONENT-ISOLATION.md`. The upstream reference implementation is helpful tooling, not the authority for product correctness.

## Before implementation

- Do not implement or mark requirements verified before the requester approves the complete scope and acceptance baseline in `spec/APPROVAL.md`.
- Read `spec/SYSTEM.md`, `spec/ACCEPTANCE.md`, `spec/PLAYGROUND.md`, `spec/system.yaml` and the relevant bounded capability/component slice.
- Preserve requirement IDs and corresponding acceptance IDs. Resolve contradictory or incomplete behavior with requester review; never derive missing product requirements from Orama defaults.
- Do not copy a predecessor search engine's source, algorithms, tests, artifacts or ranking constants. Public Orama documentation and independent authored fixtures are permitted.
- Do not assume exact Searchable index v2 or published TypeScript/Python API compatibility.
- Evaluate Orama APIs at a pinned version. If an approved behavior cannot be supported without complex engine emulation, document the feasibility result and reopen approval.

## Component verification

- Components must be invocable with programmable substitutes of required dependencies and publish a programmable mock of their own provided capabilities; test the mock against the provider contract and test consumer integration separately.
- Bind every acceptance/test case to one requirement version. Record negative/boundary paths, failures and trust assumptions, not only happy paths.
- Store actual test results and evidence only after executing against the candidate revision, with environment, dependency lock, dataset revision and provenance.
- Do not convert a failed test into a pass by narrowing a requirement or editing expected behavior without requester approval.
- A passing reference-tool check is neither an approved specification nor proof of correctness.

## Required playground

- Treat `C-11` and `R-39` through `R-39d` as release obligations.
- Provide interactive scenarios and full adopted requirement coverage, including editing/rebuilding public sample datasets, typed errors, performance diagnostics, mobile and keyboard accessibility.
- Test the playground itself; a clickable demo is not verification evidence.
- No query upload, telemetry by default, executable rendering of stored text, or private data in public fixtures.

## Validation

```bash
system-spec spec/system.yaml --stage discovery
system-spec spec/system.yaml --stage architecture
system-spec spec/system.yaml --stage verification
```

Do **not** use `--stage release` until implementation-backed evidence exists. Do not invent evidence or remove a failing gate.
