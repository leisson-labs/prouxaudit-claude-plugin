# Claude directory submission: ProUXAudit

Two listings from the LEISSON OÜ claude.ai organization, as the directory docs recommend for a product that runs its own remote MCP server:

1. **MCP connector**: `https://prouxaudit.com/api/mcp`
2. **Plugin bundle**: this repository (root folder), whose `.mcp.json` points at the same URL so people with both see one set of tools

Checked on 2026-10-12 against [Connector pre-submission checklist](https://claude.com/docs/connectors/building/review-criteria) and [Plugin pre-submission checklist](https://claude.com/docs/plugins/pre-submission-checklist). Evidence is linked per row; a row without evidence names its gap.

## Connector checklist

| Requirement | Status | Evidence |
|---|---|---|
| Separate read and write tools; no catch-all request tool | Pass | Four purpose-built tools: `start_ux_audit`, `get_ux_audit`, `get_public_report`, `verify_ux_changes` (see `evals/mocks/prouxaudit/_tools.json`) |
| Custom query tools reference API docs | Not applicable | No tool accepts freeform endpoints, queries or bodies |
| Every tool has `title` and the applicable hint | Pass | `get_ux_audit`, `get_public_report`: `readOnlyHint: true`. `start_ux_audit`, `verify_ux_changes`: `readOnlyHint: false`, `destructiveHint: false` (they create an audit, they modify or delete nothing). claude.ai groups them as read-only and write tools (`assets/screenshot-1-connector.png`) |
| Tool names ≤ 64 characters | Pass | Longest is `verify_ux_changes` (17) |
| Narrow, accurate descriptions; no prompt-injection patterns, no promotion | Pass | Descriptions state what each tool does; none instructs Claude to call other tools, fetch instructions or promote a product |
| Valid calls succeed; errors are actionable | Pass | Live claude.ai run on 2026-10-12: audit of `https://prouxaudit.com` completed (93/100, 20/20 dimensions). Typed error codes: `invalid_target`, `target_not_allowed`, `audit_handle_expired`, `audit_handle_revoked`, `budget_exceeded`, `service_unavailable`; HTTP 429 on network rate limit |
| Input validation | Pass | Public HTTP(S) URLs only; localhost, private, link-local, metadata and credential-bearing URLs are refused server-side (SSRF tests in PROUXAUDIT) |
| Reasonably sized responses | Pass | One structured audit result per handle; queued/running states are compact |
| No collection of conversation data; no reading of memory, history or files | Pass | Tools receive only `url`, optional `locale` and `auditHandle` |
| API ownership; server domain matches the service | Pass | `prouxaudit.com` serves both the product and the MCP endpoint (LEISSON OÜ) |
| Not an unsupported use case | Pass | No payments, no transfer of assets, no AI image/video/audio generation. The connector has no checkout, plan or payment tool |
| Test credentials | Not applicable | The connector needs no account (no sign-in; claude.ai detects "No sign-in"). Every tool works anonymously within the connector budget |
| Public documentation | Pass | https://prouxaudit.com/docs/mcp |
| Privacy policy covers connector processing | Pass | https://prouxaudit.com/privacy (EN) and https://prouxaudit.com/et/privacy (ET), connector section approved in PROUXAUDIT#247 |
| Support contact | Pass | prouxaudit@leisson.eu (README "Support") |
| Tested as a custom connector in Claude | Pass | claude.ai custom connector run on 2026-10-12 (screenshots below) |
| Tested with MCP Inspector | Partial | Scripted protocol probes against production (`initialize`, `tools/list`, `resources/list`) on 2026-10-12 after PROUXAUDIT#339 and #341 (proof comments on those PRs). MCP Inspector itself was not run; run `npx @modelcontextprotocol/inspector` against the URL before ticking the portal's **Test & launch** confirmation |

## Plugin checklist

| Requirement | Status | Evidence |
|---|---|---|
| Folder contains `.claude-plugin/plugin.json` | Pass | Repository root |
| One plugin per submission | Pass | Single plugin at the root |
| Every path stays inside the plugin folder; no symlinks, submodules or LFS | Pass | Plain files only |
| No `.DS_Store`, `Thumbs.db`, `desktop.ini`, `__MACOSX` | Pass | None tracked |
| Portable file and folder names; no rewriting `.gitattributes` | Pass | No `.gitattributes` |
| Size limits (repo < 50 MiB, file < 5 MiB, non-image file < 256 KiB, ≤ 512 files) | Pass | Largest file is `evals/results/…/aggregate-result.json` at 136 KB |
| `name` lowercase, distinctive, not reserved, not taken | Pass | `prouxaudit` |
| `description`, `author`, `version` set | Pass | `plugin.json` |
| README ≥ 40 words | Pass | `README.md` |
| LICENSE | Pass | `LICENSE` (MIT, LEISSON OÜ), merged in #9 |
| No launchers, lockfile installs or custom registries | Pass | The plugin runs no local command |
| No credentials in files; no reading of environment credentials | Pass | Full-history secret scan on #1: 0 findings |
| `.mcp.json` valid; remote server `type` `http` with an `https://` URL | Pass | `{"type": "http", "url": "https://prouxaudit.com/api/mcp"}` |
| Skill and command front matter valid; exact folder names | Pass | `claude plugin validate .` passes |
| README discloses everything the plugin sends or fetches | Pass | README "Tools" and "Limits": only the URL the user supplies and audit handles go to prouxaudit.com |
| Output compared with and without the plugin | Pass | `claude plugin eval`: 5/5 cases at 1.00 with the plugin, baseline 0.00–0.80 (`evals/results/`) |
| Repository public before the listing goes live | Gap | Owner action on #1: change visibility to public |

## Screenshots

From the production endpoint in a claude.ai custom-connector run on 2026-10-12. No personal data: the audited site is prouxaudit.com, and no audit handle or account detail is visible.

1. `assets/screenshot-1-connector.png`: the connector in claude.ai with its four tools grouped by permission
2. `assets/screenshot-2-audit.png`: an audit of `https://prouxaudit.com` in a Claude conversation, with the structured result summarized
3. `assets/screenshot-3-report.jpg`: the public evidence report the audit links to

Logo: `assets/logo.png` from the PROUXAUDIT plugin package (`plugins/prouxaudit/assets/logo.png`).

## Submission (owner action, #5)

At https://claude.ai/directory/manage from the LEISSON OÜ account: **Submit new → MCP connector** with the URL above, then **Submit new → Plugin bundle** with this repository; pair the two listings. Submitting accepts the Anthropic Software Directory Terms in the owner's name.
