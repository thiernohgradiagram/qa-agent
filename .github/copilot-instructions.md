# Amica AI quote automation

For quote-flow requests, use the `amica-fast-quote` skill.

- Generate a fresh Playwright workflow for the current prompt.
- Use Playwright CLI as the primary executor and run the quote interactions in one self-contained `run-code` function.
- Do not use or depend on existing automated tests, page objects, fixtures, or test helpers.
- Use approved `quote-knowledge.json`, then relevant React source, before live-browser discovery.
- Create and validate an ephemeral execution plan before generating executable code.
- Pass generated code through the deterministic policy gate.
- Add semantic checkpoints after logical page transitions.
- Classify failures before recovery.
- Use MCP only for targeted automation-drift investigation; automatic MCP snapshots remain disabled.
- Never update approved knowledge directly from a recovery run.
- Use synthetic test data and approved non-production environments only.
- Bind, payment, policy issuance, and destructive operations are disabled unless explicitly authorized.
