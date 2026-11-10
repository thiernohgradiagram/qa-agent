---
name: amica-fast-quote
description: Dynamically plan, generate, execute, recover, validate, and learn Amica quote flows using Playwright CLI first and targeted MCP only for automation drift.
---

# Amica Fast Quote Skill

## Trigger

Use this skill when the user asks to run, create, reproduce, investigate, validate, screenshot, pause, stop, quote, or bind an Amica insurance flow.

Phase 1 supports quote creation through approved non-consequential stop points. Bind/payment/policy issuance remain disabled unless the repository policy explicitly authorizes them.

## Core operating model

1. Interpret the user’s natural-language request.
2. Create an ephemeral execution plan.
3. Load relevant approved `quote-knowledge.json`.
4. Inspect relevant React source only when knowledge is insufficient.
5. Do not use existing test automation as application knowledge.
6. Generate one fresh self-contained Playwright function.
7. Submit the plan and function to the trusted runner.
8. Let Playwright CLI execute the full browser flow through one `run-code` invocation.
9. Review the structured result.
10. Enter recovery only when the outcome classifier returns `AUTOMATION_DRIFT`.

## Forbidden test dependencies

Do not read for flow knowledge, import, call, extend, modify, or copy from:

- Playwright tests;
- Cypress tests;
- Selenium tests;
- page objects;
- fixtures;
- helper libraries created for existing automated tests;
- manual-test scripts.

Application source is allowed. Trusted quote-agent runtime helpers are allowed.

## Knowledge priority

Use context in this order:

1. User prompt.
2. This skill.
3. Approved facts in `quote-knowledge.json` that match environment, product, jurisdiction, build, and feature flags.
4. Relevant React components/routes/schemas.
5. Generated React UI index, when available.
6. Compact runtime evidence.
7. Targeted Playwright CLI discovery.
8. Targeted Playwright MCP.

Never begin a known quote by requesting a full accessibility tree or scraping the whole DOM.

## Plan requirements

The ephemeral plan must include:

- run ID;
- environment;
- product;
- jurisdiction;
- scenario data;
- requested stop/completion point;
- screenshots/evidence;
- assertions;
- mutation level;
- allowed origins;
- authentication profile reference;
- required checkpoints.

Do not persist a canonical `quote-request.json`. The trusted runner may store a redacted plan in the ignored run directory.

## Locator priority

Prefer:

1. `getByTestId`;
2. `getByRole` with accessible name;
3. `getByLabel`;
4. `getByPlaceholder`;
5. stable exact text;
6. stable CSS only as a last resort.

Do not generate long CSS chains or XPath based on transient DOM structure.

Use ordered fallback locators only when all candidates refer to the same semantic control.

## Generated-function rules

The output must be one self-contained function expression compatible with Playwright CLI `run-code`.

- No import or require.
- No process, filesystem, shell, or environment enumeration.
- No dynamic code execution.
- No arbitrary external origins.
- No disabling the runner’s guards.
- No fixed sleeps unless explicitly justified.
- Use Playwright auto-waiting and semantic checkpoint waits.
- Return a JSON string matching the run-result contract.
- Include the last successful checkpoint in failures.
- Capture only requested evidence plus failure evidence required by policy.

## Checkpoints

After every logical transition, verify a semantic page fingerprint:

- URL pattern;
- page heading;
- unique controls;
- optional relevant network response.

Do not assume a click succeeded merely because it did not throw immediately.

## Outcome handling

Do not call every failure drift.

- `SUCCESS`: requested goal reached and validated.
- `AUTOMATION_DRIFT`: healthy application, stale locator/page/branch understanding.
- `APPLICATION_DEFECT`: product error or broken behavior.
- `TEST_DATA_FAILURE`: scenario rejected or invalid.
- `AUTHENTICATION_FAILURE`: login/session/authorization problem.
- `ENVIRONMENT_FAILURE`: infrastructure or dependency issue.
- `POLICY_VIOLATION`: prohibited plan or code.
- `NEEDS_REVIEW`: insufficient/conflicting evidence.

Only `AUTOMATION_DRIFT` enters recovery.

## Recovery hierarchy

1. Read compact drift report.
2. Inspect relevant React source.
3. Use targeted Playwright CLI discovery.
4. Attach MCP to the same bound browser only if still unclear.
5. Keep MCP snapshot mode `none`.
6. Request only matching text, a subtree, or shallow snapshot.
7. Generate one recovery function and continue the quote.
8. Do not revert to one action per agent turn.

## Learning

After successful recovery:

1. independently validate the observed behavior;
2. create a learning candidate;
3. attach evidence and scope;
4. replay or repeat as policy requires;
5. request review/promotion;
6. update approved `quote-knowledge.json` only through the promotion mechanism.

Business-flow changes require human review initially.

## Result presentation

Report:

- classification;
- pages/checkpoints reached;
- requested evidence paths;
- branches taken;
- final URL;
- quote identifier/premium only if requested and safe;
- drift/failure evidence;
- whether a learning candidate was created.

Never claim success without validated checkpoints.
