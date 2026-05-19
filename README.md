<div align="center">

# GET SHIT DONE

**English** · [Português](README.pt-BR.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja-JP.md) · [한국어](README.ko-KR.md)

**A light-weight and powerful meta-prompting, context engineering and spec-driven development system for Claude Code, OpenCode, Gemini CLI, Kilo, Kiro, Codex, Copilot, Cursor, Windsurf, Antigravity, Augment, Trae, Qwen Code, Cline, and CodeBuddy.**

**Solves context rot — the quality degradation that happens as your AI fills its context window.**

[![npm version](https://img.shields.io/npm/v/@fei2-labs/get-shit-done?style=for-the-badge&logo=npm&logoColor=white&color=CB3837)](https://www.npmjs.com/package/@fei2-labs/get-shit-done)
[![npm downloads](https://img.shields.io/npm/dm/@fei2-labs/get-shit-done?style=for-the-badge&logo=npm&logoColor=white&color=CB3837)](https://www.npmjs.com/package/@fei2-labs/get-shit-done)
[![Tests](https://img.shields.io/github/actions/workflow/status/gsd-build/get-shit-done/test.yml?branch=main&style=for-the-badge&logo=github&label=Tests)](https://github.com/gsd-build/get-shit-done/actions/workflows/test.yml)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/mYgfVNfA2r)
[![X (Twitter)](https://img.shields.io/badge/X-@gsd__foundation-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/gsd_foundation)
[![$GSD Token](https://img.shields.io/badge/$GSD-Dexscreener-1C1C1C?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgZmlsbD0iIzAwRkYwMCIvPjwvc3ZnPg==&logoColor=00FF00)](https://dexscreener.com/solana/dwudwjvan7bzkw9zwlbyv6kspdlvhwzrqy6ebk8xzxkv)
[![GitHub stars](https://img.shields.io/github/stars/Fei2-Labs/gsd?style=for-the-badge&logo=github&color=181717)](https://github.com/Fei2-Labs/gsd)
[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](LICENSE)

---

> **Fei2-Labs fork** — This is [`@fei2-labs/get-shit-done`](https://www.npmjs.com/package/@fei2-labs/get-shit-done), a community fork of the upstream [`get-shit-done-cc`](https://www.npmjs.com/package/get-shit-done-cc) with **first-class Kiro IDE/CLI support** (`--kiro`). All original features are preserved. For the official package, see [gsd-build/get-shit-done](https://github.com/gsd-build/get-shit-done).
>
> **Install this fork:**
> ```bash
> # Install for Kiro (this fork)
> npx @fei2-labs/get-shit-done --kiro --global
>
> # All other runtimes work identically to upstream
> npx @fei2-labs/get-shit-done --claude --global
> npx @fei2-labs/get-shit-done --all --global
> ```
>
> ⭐ **If you use Kiro, please [star this repo](https://github.com/Fei2-Labs/gsd)** — it helps other Kiro users find GSD!

---

<br>

```bash
npx @fei2-labs/get-shit-done@latest
```

**Works on Mac, Windows, and Linux.**

<br>

![GSD Install](assets/terminal.svg)

<br>

*"If you know clearly what you want, this WILL build it for you. No bs."*

*"I've done SpecKit, OpenSpec and Taskmaster — this has produced the best results for me."*

*"By far the most powerful addition to my Claude Code. Nothing over-engineered. Literally just gets shit done."*

<br>

**Trusted by engineers at Amazon, Google, Shopify, and Webflow.**

</div>

---

> [!IMPORTANT]
> **Returning to GSD?**
>
> Run `/gsd-map-codebase` to re-index your codebase, then `/gsd-new-project` to rebuild GSD's planning context. Your code is fine — GSD just needs its context rebuilt. See the [CHANGELOG](CHANGELOG.md) for what's new.

---

## Why I Built This

I'm a solo developer. I don't write code — Claude Code does.

Other spec-driven tools exist, but they're all built for 50-person engineering orgs — sprint ceremonies, story points, stakeholder syncs, Jira workflows. I'm not that. I'm a creative person trying to build great things consistently.

So I built GSD. The complexity is in the system, not in your workflow. Behind the scenes: context engineering, XML prompt formatting, subagent orchestration, state management. What you see: a few commands that just work.

The system gives Claude everything it needs to do the work *and* verify it. I trust the workflow. It just does a good job.

— **TÂCHES**

---

## How It Works

The loop is six commands. Each one does exactly one thing.

### 1. Initialize

```bash
/gsd-new-project
```

Questions → research → requirements → roadmap. You approve it, then you're ready to build.

> **Already have code?** Run `/gsd-map-codebase` first. It analyzes your stack, architecture, and conventions so `/gsd-new-project` asks the right questions.

### 2. Discuss

```bash
/gsd-discuss-phase 1
```

Your roadmap has a sentence per phase. That's not enough to build it the way *you* imagine it. Discuss captures your decisions before anything gets planned: layouts, API shapes, error handling, data structures — whatever gray areas exist for this specific phase.

The output feeds directly into research and planning. Skip it, get reasonable defaults. Use it, get your vision.

### 3. Plan

```bash
/gsd-plan-phase 1
```

Research → plan → verify, in a loop until the plans pass. Each plan is small enough to execute in a fresh context window.

### 4. Execute

```bash
/gsd-execute-phase 1
```

Plans run in parallel waves. Each executor gets a fresh 200k-token context. Each task gets its own atomic commit. Walk away, come back to completed work with a clean git history.

Your main context window stays at 30–40%. The work happens in the subagents.

### 5. Verify

```bash
/gsd-verify-work 1
```

Walk through what was built. Anything broken gets a diagnosed fix plan — ready for immediate re-execution. You don't debug manually; you just run execute again.

### 6. Repeat → Ship

```bash
/gsd-ship 1
/gsd-complete-milestone
/gsd-new-milestone
```

Loop discuss → plan → execute → verify → ship until the milestone is done. Then archive, tag, and start the next one fresh.

---

## Getting Started

```bash
npx @fei2-labs/get-shit-done@latest
```

The installer prompts you to choose:
1. **Runtime** — Claude Code, OpenCode, Gemini, Kilo, Kiro, Codex, Copilot, Cursor, Windsurf, Antigravity, Augment, Trae, Qwen Code, CodeBuddy, Cline, or all (interactive multi-select — pick multiple runtimes in a single install session)
2. **Location** — Global (all projects) or local (current project only)

Verify with:
- Claude Code / Gemini / Copilot / Antigravity / Qwen Code: `/gsd-help`
- OpenCode / Kilo / Augment / Trae / CodeBuddy: `/gsd-help`
- **Kiro IDE:** Type `/` in chat to see GSD skills as slash commands
- **Kiro CLI:** `/agent swap gsd` or `ctrl+g` to switch to the GSD orchestrator agent
- Codex: `$gsd-help`
- Cline: GSD installs via `.clinerules` — verify by checking `.clinerules` exists

> [!NOTE]
> Claude Code 2.1.88+, Qwen Code, and Codex install as skills (`.claude/skills/`, `./.codex/skills/`, or the matching global `~/.claude/skills/` / `~/.codex/skills/` roots). Older Claude Code versions use `commands/gsd/`. `~/.claude/get-shit-done/skills/` is import-only for legacy migration. The installer handles all formats automatically.

The canonical discovery contract is documented in [docs/skills/discovery-contract.md](docs/skills/discovery-contract.md).

> [!TIP]
> For source-based installs or environments where npm is unavailable, see **[docs/manual-update.md](docs/manual-update.md)**.

### Using with Kiro

Kiro works differently from Claude Code — there are no `/gsd-*` slash commands in Kiro CLI. Instead:

**Kiro IDE** — Skills appear as slash commands when you type `/` in the chat input. Select a GSD skill to load its instructions.

**Kiro CLI** — Skills auto-activate based on your request description. For explicit control, use the GSD orchestrator agent:

```
/agent swap gsd          # Switch to GSD agent in an active session
kiro-cli --agent gsd     # Start Kiro CLI with GSD agent from the beginning
ctrl+g                    # Quick keyboard shortcut to swap agents
```

The GSD orchestrator agent loads all 74 skills as resources and matches your request to the right workflow automatically.

### Staying Updated

GSD evolves fast. Update periodically:

```bash
npx @fei2-labs/get-shit-done@latest
```

<details>
<summary><strong>Non-interactive Install (Docker, CI, Scripts)</strong></summary>

```bash
# Claude Code
npx @fei2-labs/get-shit-done --claude --global   # Install to ~/.claude/
npx @fei2-labs/get-shit-done --claude --local    # Install to ./.claude/

# OpenCode
npx @fei2-labs/get-shit-done --opencode --global # Install to ~/.config/opencode/

# Gemini CLI
npx @fei2-labs/get-shit-done --gemini --global   # Install to ~/.gemini/

# Kilo
npx @fei2-labs/get-shit-done --kilo --global     # Install to ~/.config/kilo/
npx @fei2-labs/get-shit-done --kilo --local      # Install to ./.kilo/

# Kiro
npx @fei2-labs/get-shit-done --kiro --global     # Install to ~/.kiro/ (includes orchestrator agent)
npx @fei2-labs/get-shit-done --kiro --local      # Install to ./.kiro/

# Codex
npx @fei2-labs/get-shit-done --codex --global    # Install to ~/.codex/
npx @fei2-labs/get-shit-done --codex --local     # Install to ./.codex/

# Copilot
npx @fei2-labs/get-shit-done --copilot --global  # Install to ~/.github/
npx @fei2-labs/get-shit-done --copilot --local   # Install to ./.github/

# Cursor CLI
npx @fei2-labs/get-shit-done --cursor --global      # Install to ~/.cursor/
npx @fei2-labs/get-shit-done --cursor --local       # Install to ./.cursor/

# Windsurf
npx @fei2-labs/get-shit-done --windsurf --global    # Install to ~/.codeium/windsurf/
npx @fei2-labs/get-shit-done --windsurf --local     # Install to ./.windsurf/

# Antigravity
npx @fei2-labs/get-shit-done --antigravity --global # Install to ~/.gemini/antigravity/
npx @fei2-labs/get-shit-done --antigravity --local  # Install to ./.agent/

# Augment
npx @fei2-labs/get-shit-done --augment --global     # Install to ~/.augment/
npx @fei2-labs/get-shit-done --augment --local      # Install to ./.augment/

# Trae
npx @fei2-labs/get-shit-done --trae --global        # Install to ~/.trae/
npx @fei2-labs/get-shit-done --trae --local         # Install to ./.trae/

# Qwen Code
npx @fei2-labs/get-shit-done --qwen --global        # Install to ~/.qwen/
npx @fei2-labs/get-shit-done --qwen --local         # Install to ./.qwen/

# CodeBuddy
npx @fei2-labs/get-shit-done --codebuddy --global   # Install to ~/.codebuddy/
npx @fei2-labs/get-shit-done --codebuddy --local    # Install to ./.codebuddy/

# Cline
npx @fei2-labs/get-shit-done --cline --global       # Install to ~/.cline/
npx @fei2-labs/get-shit-done --cline --local        # Install to ./.clinerules

# All runtimes
npx @fei2-labs/get-shit-done --all --global      # Install to all directories
```

Use `--global` (`-g`) or `--local` (`-l`) to skip the location prompt.
Use `--claude`, `--opencode`, `--gemini`, `--kilo`, `--kiro`, `--codex`, `--copilot`, `--cursor`, `--windsurf`, `--antigravity`, `--augment`, `--trae`, `--qwen`, `--codebuddy`, `--cline`, or `--all` to skip the runtime prompt.
Use `--sdk` to also install the GSD SDK CLI (`gsd-sdk`) for headless autonomous execution.

</details>

<details>
<summary><strong>Development Installation</strong></summary>

Clone the repository, build hooks, and run the installer locally:

```bash
git clone https://github.com/Fei2-Labs/gsd.git
cd gsd
npm run build:hooks
node bin/install.js --kiro --local
```

The `build:hooks` step is required — it compiles hook sources into `hooks/dist/` which the installer copies from. Without it, hooks won't be installed and you'll get hook errors in Claude Code. (The npm release handles this automatically via `prepublishOnly`.)

Installs to `./.claude/` for testing modifications before contributing.

</details>

### Recommended: Skip Permissions Mode

GSD is designed for frictionless automation. Run Claude Code with:

```bash
claude --dangerously-skip-permissions
```

GSD is built for frictionless automation. Skip-permissions is how it's intended to run.

Install only the skills you need with `--profile=core` (six core-loop skills), `--profile=standard` (core + phase management), or the default full install. Profiles compose: `--profile=core,audit`. `--minimal` is an alias for `--profile=core`. See **[docs/USER-GUIDE.md](docs/USER-GUIDE.md)** for the full walkthrough, non-interactive install flags for all 15 runtimes, and permissions configuration. See [ADR-0011](docs/adr/0011-skill-surface-budget-module.md) for the profile model and runtime surface control.

Current release highlights are in [docs/RELEASE-v1.42.1.md](docs/RELEASE-v1.42.1.md): package legitimacy checks, safer installer migrations, runtime surface control, custom ship PR sections, reviewer defaults, fallow structural review, and quota-aware execution recovery.

---

## Commands

The main loop:

| Command | What it does |
|---------|--------------|
| `/gsd-new-project` | Questions → research → requirements → roadmap |
| `/gsd-discuss-phase [N]` | Capture implementation decisions before planning |
| `/gsd-plan-phase [N]` | Research + plan + verify |
| `/gsd-execute-phase <N>` | Execute plans in parallel waves |
| `/gsd-verify-work [N]` | Manual acceptance testing |
| `/gsd-ship [N]` | Create PR from verified phase work |
| `/gsd-progress --next` | Auto-detect and run the next step |
| `/gsd-complete-milestone` | Archive milestone and tag release |
| `/gsd-new-milestone` | Start next version |
| `/gsd:surface` | Enable/disable skill clusters at runtime without reinstall |

For ad-hoc tasks, autonomous mode, codebase analysis, forensics, and the full command surface — see **[docs/COMMANDS.md](docs/COMMANDS.md)**.

---

## Why It Works

Three things most AI-coding setups get wrong:

**1. Context bloat.** As a session grows, quality degrades. GSD keeps your main context clean by doing the heavy work in fresh subagent contexts. Researchers, planners, and executors each start fresh with exactly what they need.

**2. No shared memory.** GSD maintains structured artifacts that survive session boundaries: `PROJECT.md` (vision), `REQUIREMENTS.md` (scope), `ROADMAP.md` (where you're going), `STATE.md` (current position and decisions), `CONTEXT.md` (per-phase implementation decisions). Every new session loads these and knows exactly where things stand.

**3. No verification.** Code that "runs" isn't code that "works." GSD's verify step walks you through what was built, diagnoses failures with dedicated debug agents, and generates fix plans before you declare a phase done.

See **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)** for how the multi-agent orchestration and context engineering work in detail.

---

## Configuration

Settings live in `.planning/config.json`. Configure during `/gsd-new-project` or update with `/gsd-settings`.

Key dials:

| Setting | What it controls |
|---------|-----------------|
| `mode` | `interactive` (confirm each step) or `yolo` (auto-approve) |
| Model profiles | `quality` / `balanced` / `budget` — controls which model each agent uses |
| `workflow.research` / `plan_check` / `verifier` | Toggle the quality agents that add tokens and time |
| `parallelization.enabled` | Run independent plans simultaneously |

Optional structural review: set `code_quality.fallow.enabled` to `true` to add a fallow pre-pass to `/gsd-code-review`. GSD writes `.planning/phases/<phase>/FALLOW.json` and surfaces a `Structural Findings (fallow)` section in `REVIEW.md`. Install with `npm install -D fallow@^2.70.0` (or system-wide via `cargo install fallow`; note that the Rust binary's JSON schema must match the documented v2.70+ contract — older versions may produce silent zero-finding output).

Package legitimacy checks are built into the research, planning, and execution path: recommended dependencies get audited, unverified packages require a human checkpoint, and failed installs stop instead of trying similarly named alternatives.

For the full configuration reference — all settings, git branching strategies, per-runtime model overrides, workstream config inheritance, agent skills injection — see **[docs/CONFIGURATION.md](docs/CONFIGURATION.md)**.

---

## Documentation

| Doc | What's in it |
|-----|-------------|
| [User Guide](docs/USER-GUIDE.md) | End-to-end walkthrough, install options, all runtime flags, configuration reference |
| [Commands](docs/COMMANDS.md) | Every command with flags and examples |
| [Configuration](docs/CONFIGURATION.md) | Full config schema, model profiles, git branching |
| [Architecture](docs/ARCHITECTURE.md) | How the multi-agent orchestration works |
| [CLI Tools](docs/CLI-TOOLS.md) | `gsd-sdk query` and programmatic SDK dispatch seams |
| [Features](docs/FEATURES.md) | Complete feature index |
| [Changelog](CHANGELOG.md) | What changed in each release |

---

## Troubleshooting

**Commands not showing up?** Restart your runtime after install. GSD installs to `~/.claude/skills/gsd-*/` (Claude Code), `~/.codex/skills/gsd-*/` (Codex), or the equivalent for your runtime.

**Codex users — minimum supported CLI version is `0.130.0`.** Codex CLI 0.130.0 ([release notes](https://github.com/openai/codex/releases/tag/rust-v0.130.0)) removed extra-skill-roots discovery via [openai/codex#21485](https://github.com/openai/codex/pull/21485); from that version onward Codex discovers skills from standard roots (including `~/.codex/skills/<name>/SKILL.md`). GSD installs there directly. Earlier Codex CLI versions may still discover additional roots, which can surface duplicate `gsd-*` entries (one from extra-roots discovery, one from `~/.codex/skills/`); restart Codex after install and either upgrade or accept the duplicate listing.

**Something broken?** Re-run the installer — it's idempotent:
```bash
npx get-shit-done-cc@latest
```

**Containers or Docker?** Set `CLAUDE_CONFIG_DIR` before installing to avoid tilde-expansion issues:
```bash
CLAUDE_CONFIG_DIR=/home/youruser/.claude npx get-shit-done-cc --global
```

Full troubleshooting and uninstall instructions in **[docs/USER-GUIDE.md](docs/USER-GUIDE.md#troubleshooting)**.

---

## Community

OpenCode, Gemini CLI, Kilo, Kiro, and Codex are now natively supported via `npx get-shit-done-cc`.

These community ports pioneered multi-runtime support:

| Project | Platform | Description |
|---------|----------|-------------|
| [gsd-opencode](https://github.com/rokicool/gsd-opencode) | OpenCode | Original OpenCode adaptation |
| gsd-gemini (archived) | Gemini CLI | Original Gemini adaptation by uberfuzzy |

---

## Star History

<a href="https://star-history.com/#Fei2-Labs/gsd&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=Fei2-Labs/gsd&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=Fei2-Labs/gsd&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=Fei2-Labs/gsd&type=Date" />
 </picture>
</a>

⭐ **Enjoying GSD for Kiro? [Star this repo](https://github.com/Fei2-Labs/gsd)** to help other Kiro users discover it!

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

<div align="center">

**Kiro is powerful. GSD makes it reliable.** ⭐ [Star us](https://github.com/Fei2-Labs/gsd)

</div>
