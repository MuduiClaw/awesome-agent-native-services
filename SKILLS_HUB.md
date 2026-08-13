# Awesome Agent-Native Services Skills Hub

This repository is also a cross-agent skills source. Agents can install the same catalog workflows that maintainers use to find services, install/connect services, evaluate agent-nativeness, and prepare contribution PRs.

## Claude Code plugin marketplace

Claude Code can add this repository as a plugin marketplace because the repo root contains `.claude-plugin/marketplace.json` and the plugin manifest points at the repo's `.skills/` directory. This follows Anthropic's official Claude Code plugin marketplace flow documented at <https://code.claude.com/docs/en/discover-plugins> and the plugin manifest schema documented at <https://code.claude.com/docs/en/plugins-reference>.

```text
# If /plugin is unknown, update Claude Code first.
/plugin marketplace add haoruilee/awesome-agent-native-services
/plugin install awesome-agent-native-services@awesome-agent-native-services
/reload-plugins
```

After installation, Claude Code exposes these namespaced skills:

| Skill | Invocation | Purpose |
|---|---|---|
| `find-agent-service` | `/awesome-agent-native-services:find-agent-service` | Find the right agent-native service for a task and surface onboarding steps. |
| `install-agent-service` | `/awesome-agent-native-services:install-agent-service` | Turn a task or service name into a concrete URL onboarding, skill, MCP, CLI, or SDK install path. |
| `evaluate-agent-native` | `/awesome-agent-native-services:evaluate-agent-native` | Apply the standard or operator-surface admission track and classify a service. |
| `add-to-awesome-list` | `/awesome-agent-native-services:add-to-awesome-list` | Guide the issue-first contribution workflow and service-file template. |

## ClawHub / OpenClaw

The canonical skill source remains `.skills/`, and the existing ClawHub workflow publishes those skills for OpenClaw-compatible agents:

```bash
npx clawhub@latest install find-agent-service
npx clawhub@latest install install-agent-service
npx clawhub@latest install evaluate-agent-native
npx clawhub@latest install add-to-awesome-list
```

For China access acceleration, use the mirror documented in `clawhub/README.md`.

## Manual SKILL.md-compatible agents

Agents that load `SKILL.md` folders directly can copy or symlink individual folders from `.skills/` into their local skill directory. For example:

```bash
mkdir -p ~/.claude/skills
cp -R .skills/find-agent-service ~/.claude/skills/
```

Review any skill before installation, especially if you fetched the repository from a fork.


## Service install entrypoints

This repo is intended to be more than a reading list: after installing the repository plugin/skills above, agents can use `install-agent-service` as a router from a task or service name to the best available onboarding mechanism.

| Tier | What counts | Examples |
|---|---|---|
| Repository plugin/skill | Install this repo once, then invoke catalog skills | `/awesome-agent-native-services:install-agent-service browser automation` |
| URL Onboarding | Agent reads a machine-readable URL and self-registers | Moltbook, Ensue, db9, mem9, mails.dev, MailboxKit, Agents Mail |
| Agent Skill / plugin | A service publishes a direct skill install command | Browserbase, Firecrawl, Novu, Composio, Trigger.dev, Inngest, Tavily, Langfuse |
| MCP server | A service exposes a one-command MCP server or remote MCP URL | Browser MCP, Playwright MCP, GitHub MCP Server, Memoria, Recall, Agentgateway |
| CLI / SDK | A service is installable through a package manager and callable by the agent | Vercel Agent Browser, Steel, E2B, HumanLayer, Mem0, Vapi |

Use `install-agent-service` when the user asks “which of these can I install from the catalog?” or “make this repo an installation entry point.”
