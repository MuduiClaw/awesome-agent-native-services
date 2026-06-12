# Awesome Agent-Native Services Skills Hub

This repository is also a cross-agent skills source. Agents can install the same catalog workflows that maintainers use to find services, evaluate agent-nativeness, and prepare contribution PRs.

## Claude Code plugin marketplace

Claude Code can add this repository as a plugin marketplace because the repo root contains `.claude-plugin/marketplace.json` and the plugin manifest points at the repo's `.skills/` directory.

```text
/plugin marketplace add haoruilee/awesome-agent-native-services
/plugin install awesome-agent-native-services@awesome-agent-native-services
/reload-plugins
```

After installation, Claude Code exposes these namespaced skills:

| Skill | Invocation | Purpose |
|---|---|---|
| `find-agent-service` | `/awesome-agent-native-services:find-agent-service` | Find the right agent-native service for a task and surface onboarding steps. |
| `evaluate-agent-native` | `/awesome-agent-native-services:evaluate-agent-native` | Apply the catalog's five hard criteria and classify a service. |
| `add-to-awesome-list` | `/awesome-agent-native-services:add-to-awesome-list` | Guide the issue-first contribution workflow and service-file template. |

## ClawHub / OpenClaw

The canonical skill source remains `.skills/`, and the existing ClawHub workflow publishes those skills for OpenClaw-compatible agents:

```bash
npx clawhub@latest install find-agent-service
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
