# Example Runtime Prompts for GitHub Copilot

These prompts are examples after Phase 1 is installed. They are not static tests.

## Basic happy path

Run a Rhode Island Auto quote for a 35-year-old driver with a 2025 Honda Accord. Take a screenshot of Driver Info and stop at Coverage. Use the approved QA environment and synthetic test data.

## Different evidence request

Run a Rhode Island Auto quote for a married 40-year-old homeowner with a 2026 BMW X5. Capture screenshots at Applicant, Vehicle Info, and Coverage. Stop at Coverage and return the checkpoints and branches taken.

## Drift investigation

Re-run the previous quote using the fast path. If the outcome classifier reports automation drift, preserve the browser session, inspect only the unfamiliar state using the documented recovery hierarchy, continue the quote, and create a learning candidate. Do not directly update approved knowledge.

## Failure protection

Run the quote and stop if the application returns a server error, authentication redirect, or test-data validation error. Do not attempt to heal any of those outcomes and do not create a learning candidate.
