# Organization Decisions and Inputs Required

The GitHub Copilot builder agent should not block Phase 1 when these are unknown. It should create safe placeholders, local fixture validation, and explicit TODOs. It must never guess production or credential values.

## Required before connecting to an Amica environment

| Decision | Required value | Safe default while unknown |
|---|---|---|
| Initial environment | QA/UAT environment name | `local-fixture` |
| Base URL | Approved non-production quote URL | Local fixture URL |
| Allowed origins | Exact semicolon-separated origins | Localhost only |
| Production deny patterns | Production domains/host suffixes | Deny any non-allowlisted origin |
| Authentication | SSO, storage state, extension, or manual | No remote auth |
| Storage-state path | Secure ignored path | `playwright/.auth/user.json` placeholder |
| Test account role | Least-privilege approved account | None |
| Synthetic identity source | Approved fake data rules/service | Deterministic local synthetic generator |
| Initial product/state | Example: Auto / RI | Auto / RI fixture only |
| Maximum mutation | Read-only, quote-create, bind | `quote_create`, bind disabled |
| Screenshot rules | Pages and redaction requirements | Requested pages only |
| Trace retention | Duration and storage location | Retain failures locally, ignored by Git |
| Run artifact retention | Duration and cleanup policy | 7 days local placeholder |
| Build identifier | Header, endpoint, HTML meta, deployment manifest | `unknown` with knowledge promotion disabled |
| Feature flags | Source of active flags | Unknown/empty |
| Headed/headless | Local and CI preference | Headed locally, headless CI |
| Browser | Chrome/Chromium/Edge | Installed Chromium/Chrome supported by CLI |
| React source root | Application packages/directories | The builder agent discovers; otherwise TODO |
| Test ID attribute | `data-testid` or organization custom | `data-testid` |
| CI integration | Pipeline and secret provider | Not enabled in Phase 1 |
| Jira integration | Project/API/evidence rules | Deferred |
| PolicyCenter/BillingCenter | URLs, auth, permitted operations | Deferred |
| Bind/payment permission | Explicit authorization | Disabled |

## Governance decisions before controlled learning

- Who reviews new business-flow knowledge?
- How many repeat validations permit locator-only auto-promotion?
- What application-build compatibility rule is required?
- How are feature flags represented?
- What evidence must accompany a candidate?
- Who may promote knowledge?
- Is promotion a pull request, signed artifact, or controlled service operation?
- How are stale/deprecated facts retired?
- How long is provenance retained?

## Security decisions before enterprise deployment

- Container/sandbox platform.
- Network egress policy.
- Secret manager.
- Test-account lifecycle.
- Audit-log destination.
- Artifact encryption.
- PII redaction rules.
- Retention and deletion requirements.
- Incident response for unintended mutations.
- Approval model for bind/payment/policy issuance.
