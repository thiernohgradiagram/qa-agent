# Give the Amica AI Quote Architecture to GitHub Copilot

This folder is a repository overlay. Copy its contents into the **root of the React repository** that GitHub Copilot will work in.

## What Copilot loads

- `.github/copilot-instructions.md` — concise always-on repository rules.
- `.github/agents/*.agent.md` — selectable Builder, Reviewer, and Operator roles.
- `.github/skills/*/SKILL.md` — detailed reusable build/runtime workflows loaded when relevant or explicitly named by a custom agent.
- `AGENTS.md` — repository agent guidance, especially useful to Copilot cloud agent and Copilot CLI.
- `docs/*.md` — full architecture, decisions, and build phases; custom agents/skills explicitly instruct Copilot to read them.
- `schemas/*.json` and `automation/quote-knowledge.json` — initial contracts and empty persistent knowledge seed.

Do not rely on one giant chat message. The repository files are the durable context.

## 1. Copy the overlay into your repository

From PowerShell, while located in the React repository root:

```powershell
Copy-Item -Path "<downloaded-pack>\*" -Destination "." -Recurse -Force
```

Review the changes before committing. If the repository already contains `AGENTS.md` or `.github/copilot-instructions.md`, merge the contents rather than overwriting team instructions.

## 2. Install Playwright CLI and its agent skill

Use the project-local Playwright version when the repository already has Playwright. Otherwise follow your organization’s dependency process.

Typical commands:

```powershell
npx --no-install playwright --version
npx playwright cli --help
npx playwright cli install --skills=agents
```

If the project does not have a compatible local Playwright CLI, the builder agent should inspect the repository and propose the minimum approved installation instead of silently changing versions.

The installed skill should appear under:

```text
.agents/skills/playwright-cli/
```

## 3. Open the repository in VS Code

1. Open the repository folder, not an individual file.
2. Open GitHub Copilot Chat.
3. Select the **Copilot** session target/harness.
4. Run **Chat: Open Customizations** from the Command Palette.
5. Verify these workspace agents appear without validation errors:
   - Amica Quote Builder
   - Amica Quote Reviewer
   - Amica Quote Operator
6. Verify these skills are discovered:
   - `amica-quote-builder`
   - `amica-fast-quote`
   - `playwright-cli`

## 4. Start with the Builder agent

Create a feature branch, then select **Amica Quote Builder** from the agent dropdown.

Send only:

```text
Execute Phase 0 only, following docs/BUILD_PHASES.md. Do not implement the later phases.
```

The custom agent and skill tell Copilot which architecture documents to read. Do not paste the entire architecture into the chat.

## 5. Review before implementation

Review `docs/AI_QUOTE_DISCOVERY.md` and the proposed Phase 1 plan. Correct repository-specific assumptions before sending:

```text
Execute Phase 1 only, following docs/BUILD_PHASES.md and the approved discovery.
```

Use a new chat session for every phase to avoid carrying stale implementation context.

## 6. Run independent review

After each phase, start a fresh session and select **Amica Quote Reviewer**. Send:

```text
Review the completed phase against the architecture. Do not edit files.
```

Resolve findings before committing the phase.

## 7. Do not configure MCP at the beginning

Playwright CLI is the primary path. Add Playwright MCP only in Phase 4, after fast execution, classification, and CLI-first recovery work. The builder must verify the exact installed CLI/MCP commands and options before adding configuration.

## 8. Verify Copilot received the context

In Copilot Chat, inspect the response references/tool activity. Confirm it read:

- `.github/copilot-instructions.md`
- `AGENTS.md` where supported
- the selected custom agent
- the named skills
- `docs/AI_QUOTE_ARCHITECTURE.md`
- `docs/BUILD_PHASES.md`

If an architecture document is missing, explicitly tell Copilot to read it before continuing.

## First milestone

The first working vertical slice is complete when a natural-language scenario is converted into a validated ephemeral plan and fresh Playwright function, then run against a synthetic local quote fixture through one Playwright CLI `run-code` execution, with checkpoints, a Driver Info screenshot, a stop at Coverage, a structured result, no MCP, and no dependency on existing tests.
