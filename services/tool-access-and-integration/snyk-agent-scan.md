# Snyk Agent Scan

> **"Security scanner for AI agents, MCP servers and agent skills."**

| | |
|---|---|
| **Website** | https://github.com/snyk/agent-scan |
| **Docs** | https://github.com/snyk/agent-scan |
| **GitHub** | https://github.com/snyk/agent-scan |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/snyk/agent-scan?style=social)](https://github.com/snyk/agent-scan) |
| **Classification** | `agent-native` |
| **Category** | [Tool Access & Integration Services](README.md) |
| **License** | Apache-2.0 |

---

## Official Website

https://github.com/snyk/agent-scan

---

## Official Repo

https://github.com/snyk/agent-scan

---

## How to Use (Agent Onboarding)

```bash
uvx snyk-agent-scan@latest scan
```

Run against discovered local agent components or pass explicit MCP configuration files to inspect and scan tool descriptions, prompts, resources, and skills.

---

## Agent Skills

**Status:** ⚠️ No official Agent Skill package found; the product scans Agent Skills as first-class artifacts.

---

## MCP

**Status:** ✅ MCP-aware scanner.

Snyk Agent Scan discovers and inspects MCP configurations and MCP servers, then checks the resulting tools, prompts, and resources for agent-specific risks.

---

## What It Does

Snyk Agent Scan inventories local AI-agent components such as harnesses, MCP servers, and skills, then scans them for threats including prompt injection, tool poisoning, tool shadowing, toxic flows, malware payloads, unsafe credential handling, and hardcoded secrets.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | The official repository positions it as a security scanner for AI agents, MCP servers, and agent skills. |
| **Agent-specific primitive** | Scans MCP tools/prompts/resources and Agent Skills for risks that only exist in agent tool chains. |
| **Autonomy-compatible control plane** | Can run non-interactively in CI or agent setup flows before tools are exposed to autonomous agents. |
| **M2M integration surface** | CLI built for scripted scans of MCP configs and local agent environments. |
| **Identity / delegation** | Helps enforce which tools and skills are safe to delegate to an agent by producing attributable findings. |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Agent component inventory** | Finds local harnesses, MCP servers, and skills. |
| **MCP inspection** | Connects to MCP servers to read exposed tools, prompts, and resources. |
| **Risk detection** | Flags prompt injection, tool poisoning, tool shadowing, toxic flows, malware payloads, and credential risks. |
| **CI-friendly scan output** | Run scans before publishing or enabling agent tool bundles. |

---

## Autonomy Model

1. Agent platform or CI invokes `snyk-agent-scan` against local/discovered configs.
2. Scanner inspects agent components and MCP tool metadata.
3. Findings are used to block, quarantine, or approve tool exposure.
4. Approved tools can then be delegated to agents without per-call human review.

---

## Identity and Delegation Model

- Scan results document which tools, skills, or servers were inspected.
- Teams can use findings to decide which delegated capabilities are safe for each agent environment.
- The scanner does not replace runtime auth; it validates the artifacts that will be delegated.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| CLI | `snyk-agent-scan scan`, `inspect`, and related commands |
| MCP awareness | Reads MCP server configurations and metadata |
| CI/script usage | Non-interactive scans for build and deployment pipelines |

---

## Human-in-the-Loop Support

Recommended for review of critical findings, but normal scans can be automated and used as policy gates before agents receive tool access.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Traditional SAST** | Does not inspect MCP tool descriptions, prompts, skills, or tool-call semantics. |
| **Dependency scanner** | Finds vulnerable packages, not prompt-level or tool-shadowing attacks. |
| **Manual MCP review** | Does not scale across dynamic agent environments and CI pipelines. |

---

## Use Cases

- Preflight scanning before installing MCP servers for coding agents
- CI checks for published Agent Skills
- Security review of local agent harness configurations
- Inventory of agent tool surfaces across developer machines
