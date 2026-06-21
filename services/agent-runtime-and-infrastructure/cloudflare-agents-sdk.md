# Cloudflare Agents SDK

> **Build and host durable AI agents on Cloudflare's global network.**

| | |
|---|---|
| **Website** | https://developers.cloudflare.com/agents/ |
| **Docs** | https://developers.cloudflare.com/agents/ |
| **GitHub** | https://github.com/cloudflare/agents |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/cloudflare/agents?style=social)](https://github.com/cloudflare/agents) |
| **Classification** | `agent-native` |
| **Category** | [Agent Runtime & Infrastructure Services](README.md) |

---

## Official Website

https://developers.cloudflare.com/agents/

---

## Official Repo

https://github.com/cloudflare/agents — Agents SDK for building and deploying AI agents on Cloudflare Workers and Durable Objects.

---

## How to Use (Agent Onboarding)

**Workers + Durable Objects — start from the official agent template.**

```bash
npx create-cloudflare@latest --template cloudflare/agents-starter
cd agents-starter && npm install
npm run dev
```

The starter includes streaming chat, server-side/client-side tools, human-in-the-loop approval, and scheduled tasks. Agents can also add Browser Run, Sandbox, AI Search, MCP tools, and payments from the Cloudflare Agents docs.

---

## Agent Skills

Cloudflare publishes agent-facing setup material and skills references under its Agent setup docs and `cloudflare/skills` repository.

```bash
npx skills add https://github.com/cloudflare/skills --skill agents-sdk
```

---

## MCP

**Status:** ✅ First-class MCP support.

Cloudflare Agents includes APIs for MCP clients and servers (`McpAgent`, `McpClient`, `createMcpHandler`), remote MCP server deployment with Streamable HTTP transport, OAuth/auth guides, MCP governance, and Code Mode.

---

## What It Does

Cloudflare Agents SDK is a runtime for **persistent, stateful agent workloads** on Cloudflare. Each agent session is backed by Durable Objects with durable identity, local SQL storage, WebSocket/SSE communication, scheduling, and recovery. The same platform exposes tools for browser automation, sandboxed code execution, AI Search, MCP tools, and agentic payments.

The 2026 Agents releases expand the runtime with Project Think for long-running agents, sub-agents, durable recovery, Browser Run through a durable `browser_execute` tool, and Code Mode for letting agents write and execute typed code against external tools instead of carrying huge tool-definition prompts.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | The product is explicitly named and documented as Cloudflare Agents; docs describe hosting agents with chat, voice, email, Slack, webhooks, Browser, Sandbox, AI Search, MCP, and payments |
| **Agent-specific primitive** | Durable per-agent identity, local SQL state, sessions, WebSockets, scheduling, fibers, observability, sub-agents, Browser Run, Sandbox, Code Mode, and MCP |
| **Autonomy-compatible control plane** | Agents run globally after deploy, recover from connection churn/evictions/deploys, schedule work, call tools, and continue long-running tasks without human reconstruction of session state |
| **M2M integration surface** | TypeScript SDK, Workers bindings, HTTP/SSE/WebSockets, MCP Streamable HTTP, AI SDK integrations, and Cloudflare API surfaces |
| **Identity / delegation** | Durable Object identity per agent instance; Cloudflare account/API token/OAuth controls; MCP authorization and Access/AI Gateway governance patterns |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Agent class** | Durable Object-based agent instance with state, lifecycle hooks, and callable methods |
| **Sessions** | Per-agent durable sessions for chat, WebSockets, and programmatic turns |
| **Local SQL state** | Durable Object storage for session-local memory and coordination |
| **Project Think** | Opinionated harness for long-running agents, sub-agents, workflows, tools, and recovery |
| **Browser Run** | Durable browser automation tool using Chrome DevTools Protocol for screenshots, rendered content, and live browser sessions |
| **Sandbox / Code Mode** | Isolated execution and typed code tool runtime for interacting with external APIs/tools with approvals |
| **MCP** | Build remote MCP servers/clients, expose tools, handle OAuth, and govern MCP access |
| **Payments** | Agentic payments including x402 and Machine Payments Protocol documentation |

---

## Autonomy Model

```
Developer creates Agent class or Project Think agent
    ↓
Cloudflare deploys it to Workers + Durable Objects across the global network
    ↓
Each agent/session gets durable identity, local state, connections, and schedules
    ↓
Agent calls models and tools: Browser, Sandbox, AI Search, MCP, payments, or custom tools
    ↓
Runtime persists state and recovers from deploys, evictions, connection churn, and long-running task pauses
```

---

## Identity and Delegation Model

- **Durable Object identity** scopes each agent instance and its local state.
- **Cloudflare account and API tokens/OAuth** govern deployment and access to platform resources.
- **MCP authorization** and Access/AI Gateway patterns support controlled tool delegation.
- **Human approvals** can pause sensitive actions while preserving browser/code execution context for continuation.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| TypeScript SDK | `agents` package / `cloudflare/agents` examples |
| Workers runtime | Durable Objects, Workers bindings, scheduled tasks, WebSockets, SSE |
| MCP | Streamable HTTP servers, MCP clients, `McpAgent`, `McpClient`, `createMcpHandler` |
| Browser automation | Browser Run / Browser Rendering bindings, CDP-oriented tools |
| Code execution | Sandbox tools and Code Mode runtime |
| Observability | Logs, metrics, traces integrated with the Agents runtime |

---

## Human-in-the-Loop Support

The starter and docs include human-in-the-loop approval patterns. Browser sessions can be paused and resumed for login, MFA, or sensitive approval, and Code Mode can pause on approval-gated actions and replay completed calls from the durable log after approval.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Raw Workers / Lambda** | Stateless request handlers do not provide per-agent durable sessions, local SQL state, sub-agent orchestration, and tool-aware recovery as a packaged agent runtime |
| **Kubernetes + custom services** | Requires teams to build identity, scheduling, recovery, MCP, browser, sandbox, and observability glue themselves |
| **Agent framework only** | Frameworks define loops but do not provide the global deployment substrate, Durable Object session model, and governed tool runtime |

---

## Use Cases

- **Long-running production agents** that need durable state, scheduling, and recovery.
- **Browser-capable agents** that inspect pages, capture screenshots, and continue after human login or MFA.
- **Tool-heavy MCP agents** that expose or consume remote MCP servers with OAuth and governance.
- **Code Mode agents** that operate external APIs through compact typed code tools with approval gates.
- **Multi-channel agents** reachable through chat, voice, email, Slack, webhooks, and programmatic clients.
