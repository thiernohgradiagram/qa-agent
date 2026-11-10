# GitHub Copilot Build Phases

Use the **Amica Quote Builder** custom agent in a fresh Copilot session for each phase. Do not ask it to build the entire platform in one turn.

## Phase 0 — Repository discovery only

Send:

> Execute Phase 0 only. Read the repository instructions, architecture, decisions, and builder skill. Inspect package management, Node/TypeScript versions, React source roots, routing, component conventions, `data-testid` conventions, environment configuration, lint/typecheck/test/build commands, and CI expectations. Identify existing test-related directories only so they can be excluded; do not read their contents for selectors, flow logic, or business behavior. Create `docs/AI_QUOTE_DISCOVERY.md` and refine the implementation plan. Do not implement runtime code, connect to a real environment, or configure MCP. Stop after reporting findings, excluded paths, exact validation commands, Phase 1 file plan, assumptions, and required organization decisions.

## Phase 1 — Contracts and safety foundation

Send:

> Execute Phase 1 only, using the approved discovery and architecture. Implement TypeScript contracts and JSON Schema validation for execution plans, run results, checkpoints, evidence, drift reports, classifications, learning candidates, and quote knowledge. Implement deterministic plan validation, generated-code AST/policy validation, origin and production-deny rules, mutation-level policy, run-directory management, structured serialization, and a local synthetic React quote fixture. Add unit tests for allowed and denied cases. Do not implement real Amica access, authentication, MCP, automatic learning promotion, or static quote tests. Run formatting, lint, typecheck, tests, and build; stop when Phase 1 criteria pass.

## Phase 2 — Playwright CLI fast path

Send:

> Execute Phase 2 only. Build the trusted browser-session host, isolated context, allowed-origin network enforcement, console and failed-request collection, trace-on-failure, Playwright CLI adapter, ephemeral generated-function execution, semantic checkpoints, screenshot evidence, structured result parsing, cleanup, and timeout handling. Demonstrate against the synthetic fixture with: “Run a Rhode Island Auto quote for a 35-year-old driver with a 2025 Honda Accord, screenshot Driver Info, and stop at Coverage.” The demonstration must create and validate an ephemeral plan, generate a fresh Playwright function, pass the code policy gate, execute the full quote in one CLI `run-code` call, record checkpoints, capture the screenshot, stop at Coverage, return a structured result, use no MCP, and use no existing test automation. Stop after Phase 2.

## Phase 3 — Classification and CLI-first recovery

Send:

> Execute Phase 3 only. Implement the deterministic outcome classifier with `SUCCESS`, `AUTOMATION_DRIFT`, `APPLICATION_DEFECT`, `TEST_DATA_FAILURE`, `AUTHENTICATION_FAILURE`, `ENVIRONMENT_FAILURE`, `POLICY_VIOLATION`, and `NEEDS_REVIEW`. Add compact drift reports, relevant React-source lookup, targeted Playwright CLI discovery, same-session preservation, recovery-code validation, and one-shot recovery execution. Add synthetic scenarios for a renamed locator, inserted legitimate page, HTTP 500 defect, invalid test data, login redirect, and unavailable environment. Verify only the first two enter recovery. Do not configure MCP yet.

## Phase 4 — Targeted MCP fallback

Send:

> Execute Phase 4 only. Add Playwright MCP as the final targeted investigation level after compact evidence, React-source investigation, and CLI discovery are insufficient. Attach MCP to the same browser session, disable automatic snapshots, restrict origins/capabilities, and prove MCP is absent from the happy path. After MCP discovers the unfamiliar state, generate one recovery program rather than using one MCP action per field. Verify the installed Playwright/MCP options rather than assuming command syntax.

## Phase 5 — Controlled learning

Send:

> Execute Phase 5 only. Implement scoped and versioned `quote-knowledge.json`, provenance, confidence, build and feature-flag compatibility, learning-candidate generation, evidence references, replay validation, human-review status, duplicate/conflict detection, atomic promotion, supersession, and deprecation. Runtime recovery may create a candidate but must never directly modify approved knowledge. New branches and business-flow changes require human approval. Defects, data failures, auth failures, and environment failures must never become learned behavior.

## Independent review after each phase

Start a fresh session with **Amica Quote Reviewer** and send:

> Review the completed phase against the architecture and security requirements. Run only non-mutating validation commands. Report actionable findings with severity, file/line, impact, and remediation. Do not edit files.
