# OutreachAgent

> **"The Cold Outbound Engine for AI Agents."**

| | |
|---|---|
| **Website** | https://outreachagent.dev/ |
| **Docs** | https://outreachagent.dev/docs/introduction |
| **GitHub** | Not public; OpenAPI spec: https://api.outreachagent.dev/v1/openapi.json |
| **Classification** | `agent-native` |
| **Category** | [Communication Services](README.md) |
| **Funding / Compliance** | Free tier available; built-in opt-out, pacing, warmup, bounce/complaint thresholds, and approval policies |

---

## Official Website

https://outreachagent.dev/

---

## Official Repo

Not public. The public machine-readable API surface is the OpenAPI 3.1 specification:

https://api.outreachagent.dev/v1/openapi.json

---

## How to Use (Agent Onboarding)

**The quickest path for an agent to start using this service.**

```bash
npm install @outreachagent/sdk-ts
# or
pip install outreachagent
```

Then create an API key in OutreachAgent, set `OUTREACHAGENT_API_KEY`, and use the REST API, SDK, or MCP server to create an inbox, define a workflow, enroll contacts, and receive signed webhook events for replies.

For MCP-compatible clients:

```json
{
  "mcpServers": {
    "outreachagent": {
      "command": "npx",
      "args": ["@outreachagent/mcp"],
      "env": {
        "OUTREACHAGENT_API_KEY": "rm_live_..."
      }
    }
  }
}
```

Agent-facing quick reference: https://outreachagent.dev/for-agents

---

## Agent Skills

**Status:** ✅ Available

```bash
npx skills add https://github.com/pagefarms/cold-outreach-writer.git --skill cold-outreach-writer
```

| Skill | What It Teaches the Agent |
|---|---|
| `cold-outreach-writer` | Research a target, draft compressed human cold emails, design follow-up angles, and hand off copy to OutreachAgent templates and workflows. |

---

## MCP

**Status:** ⚠️ Documented, but package availability could not be independently verified from this environment.

| Detail | Value |
|---|---|
| **MCP Package** | Package documented as `@outreachagent/mcp` |
| **Transport** | stdio |
| **Compatible Clients** | Cursor, Claude Desktop, and MCP-compatible clients |

---

## What It Does

OutreachAgent is an API-first outbound email infrastructure platform for teams building AI agents. It lets external agent runtimes create and operate sending identities, compose or manage templates, run multi-step outbound workflows, and route replies or delivery events back into the agent loop.

The service explicitly keeps prospecting, reasoning, copy generation, and next-step decisions in the caller's runtime while it handles inboxes, delivery state, workflows, waits, retries, webhooks, and operational visibility.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | The homepage tagline is "The Cold Outbound Engine for AI Agents," and the docs say OutreachAgent is an API-first email infrastructure platform for teams building AI agents. Sources: https://outreachagent.dev/ and https://outreachagent.dev/docs/introduction |
| **Agent-specific primitive** | Reply-aware outbound execution around agent-operated inboxes: workflow waits, retries, branches, exit-on-reply behavior, delivery events, queryable thread history, webhook routing, and deliverability guardrails. |
| **Autonomy-compatible control plane** | Agents can create inboxes, contacts, templates, workflows, enrollments, webhook endpoints, domains, policies, approvals, send limits, and simulations through API/MCP surfaces rather than a required dashboard. |
| **M2M integration surface** | REST API at `https://api.outreachagent.dev/v1`, OpenAPI 3.1, TypeScript and Python SDKs, signed webhooks, LLM context files, and MCP tools. |
| **Identity / delegation** | Organizations are tenant boundaries; pods isolate environments; inboxes are email identities; named API keys delegate runtime access; policies, approvals, audit logs, workflow logs, and webhook delivery logs capture attributable external actions. |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Organization** | Tenant and billing boundary for operators and runtime credentials. |
| **Pod** | Regional or logical isolation unit for environments and data residency. |
| **Inbox** | Email identity used by an agent runtime to send and receive messages. |
| **Thread / Message** | Queryable conversation state that lets the runtime recover context across follow-ups. |
| **Workflow / Enrollment** | Durable multi-step outbound sequence with waits, branches, retries, and execution logs. |
| **Webhook endpoint / Event** | Signed event delivery for inbound replies, workflow state changes, bounces, unsubscribes, and retries. |
| **Policy / Approval** | Governance controls that can allow, block, or require review before outbound actions. |
| **Send limits / Metrics** | Pacing, warmup, deliverability thresholds, and summaries that constrain autonomous senders. |

---

## Autonomy Model

1. The operator creates or delegates an API key to the agent runtime.
2. The agent creates a pod and one or more inbox identities for outbound work.
3. The agent creates contacts, verifies addresses, drafts templates, and defines a workflow with stop-on-reply exit criteria.
4. The agent simulates and previews the workflow before sending, then publishes it when constraints pass.
5. The agent enrolls contacts and monitors delivery, bounce, reply, unsubscribe, and approval events through signed webhooks or MCP tools.
6. When a recipient replies or opts out, OutreachAgent updates thread/enrollment state and stops follow-ups according to the workflow policy.
7. The agent queries thread history and metrics to decide the next action in its own runtime.

---

## Identity and Delegation Model

- **Organization** models the human/team tenant boundary with billing and membership.
- **Pod** separates runtime environments or regions under an organization.
- **Inbox** is the agent-operated email identity; threads and messages are scoped under it.
- **API keys** are named credentials that can be created and revoked for runtime delegation.
- **Policies and approvals** constrain what the runtime may send automatically and when review is required.
- **Audit logs, enrollment logs, webhook delivery logs, and metrics** preserve evidence of state changes and outbound execution.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| REST API | `https://api.outreachagent.dev/v1` |
| OpenAPI | https://api.outreachagent.dev/v1/openapi.json |
| TypeScript SDK | `npm install @outreachagent/sdk-ts` |
| Python SDK | `pip install outreachagent` |
| MCP | `npx @outreachagent/mcp` with `OUTREACHAGENT_API_KEY` |
| Webhooks | Signed inbound and workflow event callbacks with retry/replay support |
| LLM context | https://outreachagent.dev/llms-full.txt and https://outreachagent.dev/llms.txt |

---

## Human-in-the-Loop Support

OutreachAgent supports policy outcomes that can allow, block, or require approval before sends. Approval requests can be inspected and resolved through the API or MCP layer, so humans can review high-risk outbound actions without becoming mandatory for every step. Simulations, template previews, test sends, metrics, and auto-pauses provide additional operator control before and during live campaigns.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Gmail / Outlook APIs** | They are built around human mailboxes and OAuth consent, not high-volume programmatic inbox provisioning, reply-aware outbound workflows, or agent-specific pacing and governance. |
| **Transactional email APIs** | They send messages well, but generally do not provide agent-owned inbox identities, durable follow-up state machines, stop-on-reply semantics, signed inbound routing, approval gates, workflow simulations, and per-workflow execution logs as one agent control plane. |
| **Marketing automation tools** | They center human dashboard configuration and campaign management, while OutreachAgent exposes the operational loop to external runtimes through API, SDK, MCP, and webhooks. |

---

## Use Cases

- **Agent SDR campaigns** — let an external prospecting/reasoning agent create contacts, templates, and multi-touch workflows while OutreachAgent handles pacing, delivery, and replies.
- **Reply-aware follow-up** — stop a sequence automatically when a recipient replies, bounces, unsubscribes, or triggers a custom workflow event.
- **Multi-inbox sender rotation** — provision and operate multiple sending identities with limits and warmup controls for safer autonomous outreach.
- **Audited outbound automation** — combine approvals, logs, webhook replay, metrics, and simulations to make agent-driven email operations reviewable.
