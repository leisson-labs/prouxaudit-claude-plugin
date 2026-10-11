---
description: Run a ProUXAudit UX audit of a public website URL
argument-hint: <public-url> [en|et]
---

Audit the website given in `$ARGUMENTS` using the `prouxaudit` MCP server and the `ux-audit-website` skill.

1. Check that the first argument is an explicitly supplied public HTTP(S) URL. If it is missing, localhost, a private or link-local address, a file path or contains credentials, ask for a public URL and call no tool.
2. If the second argument is `en` or `et`, pass it as `locale` to `start_ux_audit`.
3. Read the result with `get_ux_audit` until the status is `completed` or `failed`.
4. Summarize at most three findings, state whether the audit was reused from cache and its age, and list the limitations the result reports.
5. Offer `get_public_report` and the `fix-plan-from-audit` skill as follow-up steps; do not run them unless the user asks.
