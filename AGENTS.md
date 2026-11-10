# AGENTS.md — Amica AI Quote Automation

## Repository objective

Build and maintain the AI-generated quote automation foundation described in `docs/AI_QUOTE_ARCHITECTURE.md`.

## Mandatory architecture

- GitHub Copilot interprets natural-language quote requests.
- Copilot generates a fresh self-contained Playwright function for each request.
- Playwright CLI is the primary executor.
- The quote flow runs inside one `run-code` function after controlled browser/session setup.
- Playwright MCP is a targeted recovery tool only.
- CLI and MCP must be able to attach to the same bound browser session.
- Automatic MCP snapshots must remain disabled.
- `quote-knowledge.json` is the only persistent learned application-behavior data file.
- Per-run plans/results/candidates are ignored artifacts.
- There is no permanent `quote-request.json`.
- There is no static `quote-flow.json`.

## Existing test-code exclusion

Do not use, import, extend, modify, copy selectors from, or derive quote-flow knowledge from existing:

- Playwright tests;
- Cypress tests;
- Selenium tests;
- page objects;
- fixtures;
- test helpers;
- manual test scripts.

You may identify their locations only to avoid modifying them.

## Allowed knowledge sources

Use this order:

1. User prompt.
2. Amica QA Skill.
3. Approved `quote-knowledge.json`.
4. Relevant React source.
5. Optional generated source index.
6. Targeted live-browser discovery.

## Security

- Non-production only unless explicit written authorization changes the policy.
- Bind, payment, policy issuance, and destructive Guidewire mutations are disabled by default.
- Do not place credentials or authentication state in source control.
- Generated code must pass deterministic AST/policy validation.
- Generated code is untrusted input.
- URL allowlists and AST checks are defense in depth, not a complete sandbox.
- Preserve least privilege and use an isolated execution environment.
- Never silently heal an application defect.

## Failure handling

Classify before recovery:

- SUCCESS
- AUTOMATION_DRIFT
- APPLICATION_DEFECT
- TEST_DATA_FAILURE
- AUTHENTICATION_FAILURE
- ENVIRONMENT_FAILURE
- POLICY_VIOLATION
- NEEDS_REVIEW

Only `AUTOMATION_DRIFT` may enter automated recovery.

## Learning

A recovery creates a candidate. It does not directly modify approved knowledge.

Promotion requires validation, evidence, scope/build compatibility, and the configured review policy.

## Engineering standards

- Adapt to the repository’s package manager and established conventions.
- Prefer TypeScript for trusted orchestration.
- Keep generated browser functions self-contained.
- Add unit tests for policy and classification logic.
- Add a safe local integration fixture when organization environments are unavailable.
- Run formatter, lint, typecheck, tests, and build before completing a change.
- Document exact commands and observed results.
- Be honest about unsupported or unverified behavior.
