# QA Agent — Copilot Architecture Starter

This feature branch contains the **Amica AI quote-testing architecture handoff** for GitHub Copilot. It is a planning/configuration package, not a functioning quote runner.

**Start here:** [README_START_HERE.md](README_START_HERE.md)

- [Architecture](docs/AI_QUOTE_ARCHITECTURE.md)
- [Phased build instructions](docs/BUILD_PHASES.md)
- [Decisions and environment prerequisites](docs/DECISIONS_REQUIRED.md)
- [Builder agent](.github/agents/amica-quote-builder.agent.md)
- [Reviewer agent](.github/agents/amica-quote-reviewer.agent.md)
- [Operator agent](.github/agents/amica-quote-operator.agent.md)
- [Initial knowledge store](automation/quote-knowledge.json)

## Using this branch

1. Open the repository in VS Code on this branch.
2. Verify Copilot detects the Builder, Reviewer, and Operator custom agents.
3. Review [README_START_HERE.md](README_START_HERE.md), including Playwright CLI prerequisites.
4. With the **Amica Quote Builder** agent, ask: `Execute Phase 0 only, following docs/BUILD_PHASES.md.`
5. Keep QA credentials and runtime artifacts out of Git.

**Security:** This public repository must not contain proprietary React source, live customer records, authentication state, passwords, tokens, or internal QA URLs without explicit authorization.
