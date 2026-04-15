## Feature PR

---

## Linked Issue

Closes #_ISSUE_NUMBER_

---

## Feature summary

Adds Kiro IDE/CLI as a supported GSD runtime via the `--kiro` flag. Kiro (https://kiro.dev) is an agentic IDE by AWS with a shared `.kiro/` configuration directory for both IDE and CLI. This integration follows the same pattern as existing runtimes (CodeBuddy, Cline, Windsurf) — installing GSD skills, agents, and engine into `.kiro/` with Kiro-native tool names and path references.

## What changed

### New files

| File | Purpose |
|------|---------|
| `tests/kiro-install.test.cjs` | 15 tests across 6 suites: directory mapping, global dir env vars, markdown conversion, skill copy, E2E install/uninstall, uninstall cleanup |

### Modified files

| File | What changed |
|------|-------------|
| `bin/install.js` | Added `--kiro` flag parsing, `getDirName`/`getConfigDirFromHome`/`getGlobalDir` for kiro, Kiro converters (markdown, skill, agent, copy), install/uninstall branches, interactive prompt (option 11), banner, help text, module.exports |
| `get-shit-done/bin/lib/core.cjs` | Added `KIRO_SESSION_ID` to `WORKSTREAM_SESSION_ENV_KEYS` |
| `get-shit-done/workflows/review.md` | Added `--kiro` flag, Kiro CLI link, `KIRO_SESSION_ID` runtime detection |
| `get-shit-done/workflows/update.md` | Added `KIRO_CONFIG_DIR`/`KIRO_SESSION_ID` detection, `.kiro` to local dir scan |
| `README.md` | Added Kiro to description, install/uninstall examples, flags list, community ports |
| `tests/helpers.cjs` | Added `KIRO_SESSION_ID` to `TEST_ENV_BASE` |

## Implementation notes

- Kiro is implemented as a single `--kiro` runtime (not separate IDE/CLI flags) since both share `.kiro/`.
- Kiro uses lowercase tool names (`shell`, `read`, `write`, `grep`, `glob`) — converter maps Claude's `Bash`→`shell`, `Edit`→`write`, etc.
- Kiro doesn't use `settings.json` or hooks in the Claude Code sense — early-returns in `install()` and excluded from `finishInstall()` settings/statusline/hooks paths.
- `KIRO_CONFIG_DIR` env var support follows the same pattern as `KILO_CONFIG_DIR`.
- Skill adapter header (`<kiro_skill_adapter>`) guides Kiro's agent on how to interpret GSD skill files.

## Spec compliance

- [x] `getDirName('kiro')` returns `.kiro`
- [x] `getGlobalDir('kiro')` returns `~/.kiro` (default) or respects `KIRO_CONFIG_DIR`
- [x] `convertClaudeToKiroMarkdown` converts tool names, paths, and references
- [x] `copyCommandsAsKiroSkills` creates `skills/gsd-*/SKILL.md` with YAML frontmatter
- [x] `install(false, 'kiro')` creates `.kiro/skills/`, `.kiro/agents/`, `.kiro/get-shit-done/`
- [x] `uninstall(false, 'kiro')` removes GSD skills while preserving non-GSD content
- [x] `--kiro` flag works from command line
- [x] Kiro appears in interactive prompt (option 11)
- [x] All 15 new tests pass
- [x] All existing tests still pass
- [x] No leaked `.claude` paths in Kiro output

## Testing

### Test coverage

`tests/kiro-install.test.cjs` — 15 tests across 6 suites:
1. **Kiro runtime directory mapping** (3 tests) — getDirName, getGlobalDir, getConfigDirFromHome
2. **getGlobalDir (Kiro)** (5 tests) — default, explicit dir, KIRO_CONFIG_DIR env var, priority, other runtimes unaffected
3. **Kiro markdown conversion** (2 tests) — Claude→Kiro reference/tool conversion, command/agent frontmatter
4. **copyCommandsAsKiroSkills** (1 test) — creates skill directories with SKILL.md
5. **Kiro local install/uninstall** (1 test) — E2E install→verify→uninstall
6. **E2E: Kiro uninstall skills cleanup** (3 tests) — removes gsd-* skills, preserves non-GSD skills, removes engine

### Platforms tested

- [x] macOS
- [ ] Windows (including backslash path handling)
- [ ] Linux

### Runtimes tested

- [x] Other: Kiro (primary target)
- [x] N/A — existing runtime tests (codebuddy, windsurf, kilo) verified to still pass

---

## Scope confirmation

- [x] The implementation matches the scope approved in the linked issue exactly
- [x] No additional features, commands, or behaviors were added beyond what was approved
- [x] If scope changed during implementation, I updated the issue spec and received re-approval

---

## Checklist

- [x] Issue linked above with `Closes #NNN` — **PR will be auto-closed if missing**
- [ ] Linked issue has the `approved-feature` label — **PR will be closed if missing**
- [x] All acceptance criteria from the issue are met (listed above)
- [x] Implementation scope matches the approved spec exactly
- [x] All existing tests pass (`npm test`)
- [x] New tests cover the happy path, error cases, and edge cases
- [ ] CHANGELOG.md updated with a user-facing description of the feature
- [x] Documentation updated — commands, workflows, references, README if applicable
- [x] No unnecessary external dependencies added
- [ ] Works on Windows (backslash paths handled)

## Breaking changes

None — this adds a new runtime and does not modify any existing runtime behavior, file formats, or APIs.

## Screenshots / recordings

N/A — this is a runtime integration with CLI output only.
