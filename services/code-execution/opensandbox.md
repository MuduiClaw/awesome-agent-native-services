# OpenSandbox

> **"Secure, fast, extensible sandbox runtime for AI agents."**

| | |
|---|---|
| **Website** | https://open-sandbox.ai |
| **GitHub** | https://github.com/opensandbox-group/OpenSandbox |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/opensandbox-group/OpenSandbox?style=social)](https://github.com/opensandbox-group/OpenSandbox) |
| **Classification** | `agent-native` |
| **Category** | [Category README](README.md) |

---

## Official Website

https://open-sandbox.ai

---

## Official Repo

https://github.com/opensandbox-group/OpenSandbox

---

## How to Use (Agent Onboarding)

Follow open-sandbox.ai docs or run the OpenSandbox MCP server

The entry was added as a recent high-signal candidate because the official materials position it around AI agents and expose machine-to-machine interfaces rather than a human-only UI.

---

## Agent Skills

**Status:** ⚠️ No dedicated catalog skill verified in this entry. Search ClawHub or the upstream README for the latest installable skills.

---

## MCP

**Status:** ✅ Verified/documented by upstream or MCP server listings.

---

## What It Does

OpenSandbox provides secure, fast, extensible sandbox runtime for AI agents. Its agent-facing value is to give autonomous systems a programmatic primitive that can be invoked during a task loop without requiring a human to operate a dashboard for each action.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | Upstream tagline/README explicitly targets AI agents: "Secure, fast, extensible sandbox runtime for AI agents." |
| **Agent-specific primitives** | Sandbox runtime, Kubernetes, MCP server. |
| **Autonomy-compatible control plane** | Agents can call the CLI/API/MCP surface repeatedly during a run after operator provisioning. |
| **M2M integration surface** | Sandbox runtime, Kubernetes, MCP server. |
| **Identity / delegation** | Delegation is enforced through the runtime boundary, policy configuration, or caller credentials; auditability is attributable to the configured agent session. |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Agent runtime surface** | Sandbox runtime, Kubernetes, MCP server |
| **Session boundary** | Isolates work by run, process, sandbox, memory namespace, or policy scope depending on deployment |
| **Machine-readable output** | Returns artifacts, traces, memory records, or policy decisions for direct agent consumption |

---

## Autonomy Model

```
Operator provisions OpenSandbox
  ↓
Agent connects through the documented CLI/API/MCP surface
  ↓
Agent performs bounded actions under policy/session limits
  ↓
Results, state, traces, or approvals return to the agent loop
```

---

## Identity and Delegation Model

- **Agent session identity** is represented by the caller configuration, sandbox/session, memory namespace, or policy subject.
- **Delegation controls** come from runtime limits, allowlists, approval thresholds, or deployment credentials.
- **Audit trail** is provided by logs, traces, memory history, policy events, or sandbox artifacts exposed by the service.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| **Primary surface** | Sandbox runtime, Kubernetes, MCP server |
| **Repository** | https://github.com/opensandbox-group/OpenSandbox |
| **MCP** | ✅ |

---

## Human-in-the-Loop Support

Humans configure the service and policy boundaries. Normal agent operation proceeds unattended until a deployment-specific limit, approval gate, or error condition requires review.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Generic developer tool** | Does not expose an agent-first primitive or machine-to-machine loop tailored for autonomous agents. |
| **Manual dashboard workflow** | Requires a human to click through the same action the agent needs to perform programmatically. |

---

## Use Cases

- Autonomous coding, research, support, or operations agents that need secure, fast, extensible sandbox runtime for AI agents
- Multi-agent systems that need shared, auditable infrastructure boundaries
- Production agent deployments where repeatable machine interfaces matter more than human UI
