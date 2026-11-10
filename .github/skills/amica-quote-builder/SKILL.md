---
name: amica-quote-builder
description: Build and review the secure adaptive Amica quote-testing platform in controlled phases without depending on existing test automation.
---

# Amica Quote Builder Skill

## Use this skill when

The user asks to design, implement, review, secure, test, or extend the Amica AI quote-testing platform.

## Authoritative context

Read these files before implementation:

- `AGENTS.md`
- `docs/AI_QUOTE_ARCHITECTURE.md`
- `docs/DECISIONS_REQUIRED.md`
- `docs/BUILD_PHASES.md`
- the JSON Schemas under `schemas/`

## Core architecture

- Natural-language prompt defines the scenario.
- Copilot creates an ephemeral execution plan.
- A deterministic policy gate validates the plan.
- Copilot generates a fresh self-contained Playwright function.
- A deterministic AST/policy gate validates generated code.
- A trusted TypeScript runner owns the browser, evidence, guards, cleanup, and result parsing.
- Playwright CLI executes the full flow in one `run-code` invocation.
- Semantic checkpoints detect divergence at logical transitions.
- An outcome classifier distinguishes success, automation drift, product defects, data problems, authentication failures, environment failures, policy violations, and needs-review cases.
- Only automation drift enters targeted recovery.
- Recovery escalates from compact evidence to React source to targeted CLI discovery and only then to targeted MCP.
- Successful recovery creates a learning candidate. Replay/review/promotion updates approved `quote-knowledge.json`.

## Existing test-code exclusion

Do not read existing test content for selectors, flow order, branch logic, fixtures, or business knowledge. You may identify excluded directories by path so the implementation avoids them.

## Required build sequence

Implement only the phase requested by the user. Follow `docs/BUILD_PHASES.md`.

1. Phase 0 — repository discovery and implementation plan.
2. Phase 1 — contracts, schemas, policy gates, run directories, synthetic fixture, and unit tests.
3. Phase 2 — trusted browser host, Playwright CLI one-shot execution, checkpoints, evidence, and structured result.
4. Phase 3 — outcome classification and CLI-first recovery.
5. Phase 4 — targeted MCP fallback attached to the same browser session.
6. Phase 5 — controlled learning, replay, review, promotion, supersession, and deprecation.

Do not silently continue into the next phase.

## Security requirements

Generated code is untrusted. Instructions are not enforcement. Use deterministic validation and an isolated execution environment.

Reject or prevent:

- production and non-allowlisted origins;
- shell and child-process execution;
- arbitrary filesystem access;
- `process`, `eval`, `Function`, dynamic loading, and environment enumeration;
- disabling runner guards;
- unexpected external network access;
- unapproved upload/download;
- bind, payment, issuance, cancellation, and destructive operations;
- credentials or auth state in source control.

## Completion report

At the end of a phase, report:

- files added/changed;
- architecture decisions implemented;
- commands executed and outcomes;
- acceptance criteria passed/failed;
- assumptions and placeholders;
- unresolved security or integration risks;
- recommended next phase, without implementing it.
