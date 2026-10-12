# ProUXAudit plugin for Claude

This plugin connects Claude Code to the [ProUXAudit](https://prouxaudit.com) MCP connector. It lets Claude run a UX audit of a public website, read the structured result, and plan fixes from the findings. It bundles a remote MCP server entry, two skills and one slash command. Audit state and measurements are produced by the ProUXAudit server, not by the plugin.

## Contents

| Path | Purpose |
| --- | --- |
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.mcp.json` | Remote MCP server `prouxaudit` at `https://prouxaudit.com/api/mcp` |
| `skills/ux-audit-website/SKILL.md` | Run and summarize an audit of a public URL |
| `skills/fix-plan-from-audit/SKILL.md` | Plan up to three fixes and re-check them |
| `commands/ux-audit.md` | `/prouxaudit:ux-audit <public-url> [en\|et]` |

## Tools

The connector exposes four tools:

| Tool | Input | Purpose |
| --- | --- | --- |
| `start_ux_audit` | `url`, optional `locale` (`en` or `et`) | Start an audit of a public URL, or reuse a recent one and disclose the cache age |
| `get_ux_audit` | `auditHandle` | Read the state and, when completed, the structured result of one audit |
| `verify_ux_changes` | `auditHandle` | Start a fresh audit of the same URL after a change and return a new handle; never reuses the cache |
| `get_public_report` | `auditHandle` | Return the public evidence report link of a completed audit |

## Install

Load the plugin from a local checkout with `claude --plugin-dir <path-to-this-repository>`. Validate the bundle with `claude plugin validate .`.

## Limits

- Only explicitly supplied public HTTP(S) URLs are audited. Localhost, private-network, link-local and cloud-metadata addresses, file paths and credential-bearing URLs are refused.
- `url` is limited to 2048 characters.
- An `auditHandle` is an opaque handle that can expire or be revoked; the connector then returns `audit_handle_expired` or `audit_handle_revoked`.
- Requests are rate limited and audits are subject to a budget; the connector returns `rate_limited` or `budget_exceeded`.
- A fresh verification compares measurements of the same URL. When capture failed or coverage is insufficient the comparison is `inconclusive`, which is not evidence that a finding was fixed.
- The plugin has no tool for plan changes or payments and stores no data of its own.
- The connector can be unavailable (`service_unavailable`); the skills report this rather than inventing a result.

## Evals

`evals/` holds an eval suite for `claude plugin eval`: five cases (audit from a public URL, read an existing result, fix plan from a result, verify changes with a fresh re-audit, refuse a private-network URL). The ProUXAudit connector is replaced by mocks under `evals/mocks/prouxaudit/`, so a run makes no request to prouxaudit.com. Cases use `https://prouxaudit.com` as the audited URL; the refusal case uses a private-network address on purpose, to check that nothing is sent to the connector.

```
claude plugin eval . --trust-plugin --no-publish
```

A run makes real model calls (30 agent runs plus judge calls: five cases, three runs per arm, two arms). The latest passing report is committed under `evals/results/`; `aggregate-result.json` there has local paths redacted.
## Support

Questions and problem reports: prouxaudit@leisson.eu. Include the tool name and the returned error code, but not an `auditHandle` you want to keep private.
