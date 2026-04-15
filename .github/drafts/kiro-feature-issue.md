# Feature Request: Kiro IDE/CLI Runtime Support

## Pre-submission checklist
- [x] I have searched existing issues and discussions — this has not been proposed and declined before
- [x] I have read CONTRIBUTING.md and understand that I must wait for `approved-feature` before writing any code
- [x] I have read the existing GSD commands and workflows and confirmed this feature does not duplicate existing behavior
- [x] This feature solves a problem for solo developers using AI coding tools, not a personal preference or workflow I happen to like

## Feature name
Kiro IDE/CLI runtime support

## Type of addition
New runtime integration

## The solo developer problem
Kiro (https://kiro.dev) is an agentic IDE by AWS that also ships a CLI. It uses `.kiro/` for local configuration and `~/.kiro/` for global configuration, with support for skills (SKILL.md with YAML frontmatter), agents, steering files, and hooks. Solo developers using Kiro IDE or Kiro CLI currently cannot install GSD because there is no `--kiro` runtime option. They must manually adapt Claude Code files to Kiro's format, which is error-prone and not sustainable across GSD updates.

## What this feature adds
A single `--kiro` runtime flag that installs GSD to `.kiro/` (local) or `~/.kiro/` (global), supporting both Kiro IDE and Kiro CLI since they share the same configuration directory structure.

- `npx get-shit-done-cc --kiro --global` installs to `~/.kiro/`
- `npx get-shit-done-cc --kiro --local` installs to `./.kiro/`
- Skills installed as `skills/gsd-*/SKILL.md` with YAML frontmatter
- Agents installed to `agents/` directory
- Tool names converted: `Bash` → `shell`, `Edit` → `write`, `Read` → `read`
- `CLAUDE.md` references → `.kiro/steering/` references
- `KIRO_CONFIG_DIR` env var for custom global path
- `KIRO_SESSION_ID` for workstream detection
- Interactive prompt includes Kiro (option 11, alphabetically between Kilo and OpenCode)

## Full scope of changes

Files created:
- `tests/kiro-install.test.cjs` — 15 tests across 6 suites

Files modified:
- `bin/install.js` — Flag parsing, getDirName, getConfigDirFromHome, getGlobalDir, converters (convertClaudeToKiroMarkdown, convertClaudeCommandToKiroSkill, convertClaudeAgentToKiroAgent, copyCommandsAsKiroSkills), install/uninstall branches, interactive prompt, banner, help text, module.exports
- `get-shit-done/bin/lib/core.cjs` — KIRO_SESSION_ID in WORKSTREAM_SESSION_ENV_KEYS
- `get-shit-done/workflows/review.md` — --kiro flag, Kiro CLI link, KIRO_SESSION_ID detection
- `get-shit-done/workflows/update.md` — KIRO_CONFIG_DIR/KIRO_SESSION_ID detection, .kiro in local dir scan
- `README.md` — Kiro added everywhere runtimes are listed
- `tests/helpers.cjs` — KIRO_SESSION_ID in TEST_ENV_BASE

Systems affected:
- Runtime installation system (install.js)
- Workstream session detection (core.cjs)
- Cross-runtime review workflow (review.md)
- Self-update workflow (update.md)

## User stories
1. As a solo developer using Kiro IDE, I want to install GSD with `npx get-shit-done-cc --kiro --global` so that I can use GSD workflows and commands in Kiro without manual file conversion.
2. As a solo developer using Kiro CLI, I want GSD skills to use Kiro's native tool names (shell, read, write) so that the AI agent can execute GSD workflows correctly.
3. As a solo developer with multiple IDE setups, I want to install GSD for Kiro alongside other runtimes using `--all` so that all my environments stay in sync.

## Acceptance criteria
- [x] `getDirName('kiro')` returns `.kiro`
- [x] `getGlobalDir('kiro')` returns `~/.kiro` (default) or respects `KIRO_CONFIG_DIR`
- [x] `convertClaudeToKiroMarkdown` converts tool names (Bash→shell, Edit→write), paths (.claude/→.kiro/), and references (CLAUDE.md→.kiro/steering/)
- [x] `copyCommandsAsKiroSkills` creates skills/gsd-*/SKILL.md with correct YAML frontmatter
- [x] `install(false, 'kiro')` creates .kiro/skills/, .kiro/agents/, .kiro/get-shit-done/
- [x] `uninstall(false, 'kiro')` removes GSD skills while preserving non-GSD content
- [x] `--kiro` flag works from command line
- [x] Kiro appears in interactive prompt (option 11)
- [x] All 15 new tests pass
- [x] All existing tests still pass (codebuddy, windsurf, kilo verified)
- [x] No leaked .claude paths in non-Claude runtime output

## Which area does this primarily affect?
Runtime integration (hooks, statusline, settings)

## Applicable runtimes
- [x] All runtimes (Kiro added alongside existing 14 runtimes)

## Breaking changes assessment
None — this adds a new runtime and does not modify any existing runtime behavior, command output, file formats, or APIs. The `--all` flag now includes `kiro` in its list, which is additive.

## Maintenance burden
- No new dependencies
- Converter functions follow the exact same pattern as CodeBuddy/Windsurf/Cline converters
- Must be updated if install.js converter patterns change (same as all other runtimes)
- Kiro tool names may evolve as Kiro matures — future updates may need converter adjustments
- Test file follows the established codebuddy-install.test.cjs pattern

## Alternatives considered
1. Two separate runtimes (`--kiro-ide` and `--kiro-cli`) — rejected because both share the same `.kiro/` directory structure and configuration format, making separate runtimes unnecessary duplication.
2. Mapping Kiro to the existing `--kilo` runtime — rejected because Kilo and Kiro are completely different projects with different configuration formats (Kilo uses `.config/kilo/` with JSON config, Kiro uses `.kiro/` with steering files).

## Prior art and references
- Kiro IDE documentation: https://kiro.dev/docs/
- Kiro CLI custom agents: https://kiro.dev/docs/cli/custom-agents/configuration-reference/
- Kiro steering files: https://kiro.dev/docs/steering/
- Pattern follows existing runtime integrations: CodeBuddy (#PR), Cline (#PR), Windsurf (#PR)
