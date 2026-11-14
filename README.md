# Orama Client Search

Specification-first implementation of a **static, browser-local lexical search engine**. The production implementation is intended to use [OramaJS](https://github.com/oramasearch/orama); the **product contracts remain implementation independent**.

**Current status:** proposed system specification and plan. No implementation or passing verification evidence exists yet. The specification is awaiting requester approval.

## System specification

| Artifact | Purpose |
| --- | --- |
| [spec/SYSTEM.md](spec/SYSTEM.md) | Standalone product scope, invariants, 11 capabilities, 48 requirements (including analyzer, geo, pin, boost and playground refinements), risks and boundaries |
| [spec/system.yaml](spec/system.yaml) | Machine-readable model aligned with [System Specification](https://github.com/ktjn/system-specification), requirements `R-01`–`R-39d`, including 5 explicit feature refinements |
| [spec/ACCEPTANCE.md](spec/ACCEPTANCE.md) | Independent requirement-linked verification scenarios; not a passing test report |
| [spec/PLAYGROUND.md](spec/PLAYGROUND.md) | Required interactive playground for **all approved features** and negative/boundary behavior |
| [spec/APPROVAL.md](spec/APPROVAL.md) | Decision log, remaining approvals, quality budgets and gate definitions |
| [PLAN.md](PLAN.md) | Proposed Orama implementation architecture, feasibility spike, implementation and release phases |
| [AGENTS.md](AGENTS.md) | Agent input boundaries and contract-first workflow |

## Core constraints

- Search requests are evaluated locally in the browser with configurable per-language stemming/stopwords, geospatial search, pinning and boosts. Static artifacts are public; there is no query-time API or required search server.
- The public dataset contains no secrets, personal content or permission-protected information.
- No default query telemetry or remote embedding/vector service.
- The browser client is headless/framework neutral. The playground is a static React/TypeScript consumer of its public API.
- Results are required to satisfy **behavioral** contracts and independent acceptance tests, not implementation-specific index bytes or floating-point scores.
- Orama is an implementation choice. Version and adapter constraints are in the plan, not in the product specification.
- A fully isolated two-team legal clean room is not claimed. Implementation code and verification evidence must be independently produced.

## Development flow

1. Review the specification and playground scenarios. Resolve [approval decisions](spec/APPROVAL.md).
2. Validate the machine-readable model against the selected system-specification reference implementation (the model is at **verification**, not release, lifecycle stage).
3. Approve the complete requirement and verification baseline before implementation.
4. Execute the Orama feasibility spike, then implement independently from the approved specification.
5. Test each logical component in isolation with programmed substitutes, run integration/acceptance tests, and exercise features in the playground.
6. Gather evidence, review relevance/performance/security and approve release.

The playground is a required part of the initial deliverable, **not** optional documentation.
