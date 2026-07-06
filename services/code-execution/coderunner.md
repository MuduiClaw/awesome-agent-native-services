# CodeRunner

> **"A local sandbox for your AI agents."**

| | |
|---|---|
| **Website** | https://github.com/instavm/coderunner |
| **GitHub** | https://github.com/instavm/coderunner |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/instavm/coderunner?style=social)](https://github.com/instavm/coderunner) |
| **Classification** | `agent-native` |
| **Category** | [Category README](README.md) |

---

## Official Website

https://github.com/instavm/coderunner

---

## Official Repo

https://github.com/instavm/coderunner

---

## How to Use (Agent Onboarding)

Install CodeRunner from GitHub and run agent workloads in isolated Apple containers

The entry was added as a recent high-signal candidate because the official materials position it around AI agents and expose machine-to-machine interfaces rather than a human-only UI.

---

## Agent Skills

**Status:** ⚠️ No dedicated catalog skill verified in this entry. Search ClawHub or the upstream README for the latest installable skills.

---

## MCP

**Status:** ✅ Verified/documented by upstream or MCP server listings.

---

## What It Does

CodeRunner provides a local sandbox for your AI agents. Its agent-facing value is to give autonomous systems a programmatic primitive that can be invoked during a task loop without requiring a human to operate a dashboard for each action.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | Upstream tagline/README explicitly targets AI agents: "A local sandbox for your AI agents." |
| **Agent-specific primitives** | Apple Containers, local sandbox CLI, MCP. |
| **Autonomy-compatible control plane** | Agents can call the CLI/API/MCP surface repeatedly during a run after operator provisioning. |
| **M2M integration surface** | Apple Containers, local sandbox CLI, MCP. |
| **Identity / delegation** | Delegation is enforced through the runtime boundary, policy configuration, or caller credentials; auditability is attributable to the configured agent session. |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Agent runtime surface** | Apple Containers, local sandbox CLI, MCP |
| **Session boundary** | Isolates work by run, process, sandbox, memory namespace, or policy scope depending on deployment |
| **Machine-readable output** | Returns artifacts, traces, memory records, or policy decisions for direct agent consumption |

---

## Autonomy Model

```
Operator provisions CodeRunner
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
| **Primary surface** | Apple Containers, local sandbox CLI, MCP |
| **Repository** | https://github.com/instavm/coderunner |
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

- Autonomous coding, research, support, or operations agents that need a local sandbox for your AI agents
- Multi-agent systems that need shared, auditable infrastructure boundaries
- Production agent deployments where repeatable machine interfaces matter more than human UI
