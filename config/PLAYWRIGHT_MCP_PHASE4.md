# Playwright MCP — configure only in Phase 4

Do not copy an unverified MCP command into production configuration.

When Phase 4 begins, the builder agent must inspect the installed Playwright MCP help and VS Code's current MCP configuration format, then create a reviewed workspace configuration that:

- attaches to the same bound browser session used by Playwright CLI;
- disables automatic snapshots;
- omits image responses unless explicitly required;
- restricts origins and capabilities;
- writes artifacts only to an ignored directory;
- exposes MCP only to the operator/recovery role;
- remains absent from the successful fast path.
