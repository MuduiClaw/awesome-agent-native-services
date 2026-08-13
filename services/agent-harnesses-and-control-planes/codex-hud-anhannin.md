# Codex HUD (anhannin)

> **"Codex HUD is an open-source status line HUD for Codex CLI, rendering Claude-HUD style usage and session status directly in the terminal."**

| | |
|---|---|
| **Website** | https://github.com/anhannin/codex-hud |
| **Docs** | https://github.com/anhannin/codex-hud/tree/master/Codex-HUD |
| **GitHub** | https://github.com/anhannin/codex-hud |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/anhannin/codex-hud?style=social)](https://github.com/anhannin/codex-hud) |
| **Classification** | `agent-native` |
| **Category** | [Agent Harnesses & Operator Surfaces](README.md) |
| **License** | MIT declared in package metadata; no root or nested `LICENSE` file as of snapshot |

---

## Official Website

No separate website is published; the official GitHub repository is the project home:

https://github.com/anhannin/codex-hud

---

## Official Repo

https://github.com/anhannin/codex-hud

---

## How to Use (Agent Onboarding)

**Interaction pattern:** `Patched Codex CLI + status-line command`

```bash
git clone https://github.com/anhannin/codex-hud.git
cd codex-hud/Codex-HUD
./install.sh

# Start a new session; existing sessions do not pick up the patch.
codex
```

The supported target is Linux with bash/zsh, Node.js/npm, Rust/cargo, and native build dependencies. This is a materially invasive install: the script may use `sudo` to install dependencies, clones and patches OpenAI Codex, compiles it, backs up an existing `~/.local/bin/codex`, installs the patched binary there, and writes `[tui].status_line_command` in `~/.codex/config.toml`. Review the script and patch before delegating installation.

---

## Agent Skills

**Status:** ⚠️ Not published

The repository contains no standard `SKILL.md` or Agent Skills package. Search community skills with `npx clawhub@latest search codex-hud`, or contribute one using the [Agent Skills specification](https://agentskills.io/specification).

---

## MCP

**Status:** ⚠️ No MCP server

This project neither publishes MCP tools nor consumes MCP as its integration surface. It reads local Codex rollout JSONL and renders a configured status-line command.

---

## What It Does

This independent Codex HUD parses local Codex rollout records and renders model, project, git branch, session usage, and five-hour/seven-day rate-window bars in Codex's terminal footer. It patches Codex to add `[tui].status_line_command`, then configures that command to invoke the local Node.js renderer.

It is distinct from `fwyc0573/codex-hud`: it embeds a compact status line in a patched Codex build rather than wrapping sessions in a managed tmux dashboard. As of the 2026-08-13 snapshot, the repository had 51 stars, no published release/tag, and no commit since 2026-05-10 UTC. It is included as a usable, purpose-built implementation, not as a latest-month momentum pick.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | Upstream calls it an **"open-source status line HUD for Codex CLI"** and derives its display directly from Codex sessions — [README](https://github.com/anhannin/codex-hud#readme) |
| **Agent-specific primitive** | It parses Codex `rollout-*.jsonl` to expose model/session state, context and rate-limit windows, project, and git branch inside the agent terminal |
| **Autonomy-compatible control plane** | The renderer is passive and does not block autonomous Codex work, but it adds no planning, approval, retry, cancellation, or session-control loop; Codex keeps all authority |
| **M2M integration surface** | Codex invokes a local `status_line_command`, which reads rollout JSONL and emits terminal text; there is no API, SDK, daemon protocol, Skill, or MCP surface |
| **Identity / delegation** | An explicit rollout path can deterministically select a session; otherwise the renderer chooses the latest rollout. It does not mint identities, delegate credentials, or enforce permissions |

This entry qualifies under the category's explicit operator-surface track. Its value is Codex-native observability, not autonomous orchestration.

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Rollout parser** | Reads Codex session metadata, turn context, token counts, and rate-limit snapshots from JSONL |
| **Status-line renderer** | Emits a compact one-shot footer through `status_line_command` |
| **Usage windows** | Displays five-hour and seven-day consumption bars with reset time |
| **Session context** | Shows current model, project, git branch, and usage state |
| **Codex TUI patch** | Adds external multi-line status-command support to the built Codex binary |
| **Color controls** | Supports `NO_COLOR` and `FORCE_COLOR` for terminal compatibility |

---

## Autonomy Model

```text
Patched Codex starts an ordinary agent session
    -> TUI invokes the configured local status-line command
    -> renderer selects an explicit rollout or the latest local rollout
    -> rollout/session and rate-limit state become terminal text
    -> Codex continues under its own agent loop and permission model
```

The HUD has no autonomous actions or control decisions. After installation it is a read-only observer of local session records.

---

## Identity and Delegation Model

- **Session selection:** Passing a rollout path provides deterministic session attribution; default latest-rollout discovery can be ambiguous when multiple sessions run concurrently.
- **Displayed identity:** Session metadata, project path, model, and git branch provide operational context rather than a service-issued principal.
- **No agent hierarchy:** The HUD does not model leader/worker roles, subagent delegation, assignments, or authority leases.
- **No credential delegation:** It reads local files and does not proxy credentials or grant tool permissions.
- **No authorization enforcement:** Codex remains responsible for approvals and sandbox policy; the HUD does not display or change them.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| Codex TUI config | `[tui].status_line_command` invokes the local renderer |
| CLI/stdout | `node dist/index.js --status-line --once --no-clear` emits the footer |
| Rollout input | Local `~/.codex/sessions/**/rollout-*.jsonl`, or an explicitly supplied rollout path |
| Git/filesystem | Reads project and branch context from the local working environment |
| Installer | Builds the TypeScript HUD, patches/builds Codex, installs a local binary, and updates config |

There is no REST API, language SDK, MCP server, or published Agent Skill.

---

## Human-in-the-Loop Support

The HUD is entirely a human-facing observation surface. It lets the operator see usage windows and session context without prompting Codex, but it provides no attach, stop, approval, or intervention command. Any steering or permission decision must happen through the underlying Codex session. New installation/configuration only takes effect after restarting Codex.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Shell prompt theme** | Can show cwd and git but does not parse Codex rollout metadata, context, or rate-limit windows |
| **Generic rate-limit dashboard** | Is not session-local and cannot associate model usage with the active Codex rollout |
| **Terminal process monitor** | Observes CPU/process state rather than Codex turn context and token/rate-limit records |

---

## Use Cases

- **Quota awareness** — keep five-hour and seven-day usage windows visible during an agent session
- **Context supervision** — see the active model and session state without asking Codex to summarize itself
- **Project attribution** — associate the compact footer with the current project and git branch
- **Low-height terminals** — embed agent telemetry in the Codex footer instead of reserving a separate dashboard pane
- **Status-line experimentation** — inspect a concrete patch-based external status-command integration for Codex
