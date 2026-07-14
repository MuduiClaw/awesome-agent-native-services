# Chimely

> **"Open-source, self-hostable in-app notification inbox infrastructure that agents can call through an HTTP API."**

| | |
|---|---|
| **Website** | https://chimely.dev |
| **Docs** | https://chimely.dev |
| **GitHub** | https://github.com/dodopayments/chimely |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/dodopayments/chimely?style=social)](https://github.com/dodopayments/chimely) |
| **Classification** | `agent-native` |
| **Category** | [Communication Services](README.md) |
| **License** | AGPL-3.0 (server), MIT (SDKs) |
| **Stars** | Not specified |

---

## Official Website

https://chimely.dev

---

## Official Repo

https://github.com/dodopayments/chimely — Core platform (open-source)

---

## Agent Skills

**Status:** ⚠️ No dedicated Agent Skills listed

Chimely is not a full agent toolkit. It is notification-inbox infrastructure with an HTTP notification API that agents can call to deliver in-app notifications to end users.

| Skill | What It Teaches the Agent |
|---|---|
| HTTP notification API | Call Chimely's API to deliver in-app notifications to end users |

**Compatibility:** Any agent runtime that can make HTTP API calls.

---

## MCP

**Status:** ⚠️ Not listed

Chimely's agent-facing surface is its HTTP API, not an MCP server.

| Detail | Value |
|---|---|
| **MCP Docs** | Not listed |
| **Transport** | HTTP API |
| **Compatible Clients** | Any agent runtime that can call HTTP APIs |

---

## What It Does

Chimely is open-source, self-hostable in-app notification inbox infrastructure built with Rust, Postgres, and Redis. It provides an HTTP API, a Server-Sent-Events hint plane, and a drop-in `<Inbox />` React component.

Agents can call Chimely's HTTP notification API to deliver in-app notifications to end users. Chimely is a self-hosted alternative to Knock, Courier, MagicBell, and Novu.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | The HTTP notification API can be called by AI agents to deliver in-app notifications to end users |
| **Agent-specific primitive** | Agent-callable notification API backed by an in-app inbox for end users |
| **Autonomy-compatible control plane** | Agents can deliver notifications through the API without operating a human-facing dashboard per notification |
| **M2M integration surface** | HTTP API, Server-Sent-Events hint plane, and React `<Inbox />` component |
| **Identity / delegation** | Notifications are delivered to end users through an application inbox rather than through a human mailbox proxy |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **HTTP Notification API** | Agents can call the API to deliver in-app notifications to end users |
| **In-App Notification Inbox** | Self-hostable inbox infrastructure for application users |
| **Server-Sent-Events Hint Plane** | Real-time hint plane for notification updates |
| **Drop-In React Inbox** | `<Inbox />` React component for embedding the inbox in an application |
| **Self-Hosted Runtime** | Rust service backed by Postgres and Redis |

---

## Autonomy Model

```
Agent needs to notify an end user
    ↓
Agent calls Chimely's HTTP notification API
    ↓
Chimely stores the notification in the in-app inbox
    ↓
Chimely emits a Server-Sent-Events hint
    ↓
The application shows the notification through <Inbox />
```

The agent does not need to own email, SMS, or push-channel delivery logic. Chimely provides the in-app notification inbox layer the application can host.

---

## Identity and Delegation Model

- Notifications are addressed to end users inside the application
- Chimely is not a human mailbox proxy or a separate agent identity provider
- Agent delegation is through API access to the application's notification infrastructure

---

## Protocol Surface

| Interface | Detail |
|---|---|
| HTTP API | Notification API agents can call to deliver in-app notifications |
| Server-Sent Events | Hint plane for notification updates |
| React Component | Drop-in `<Inbox />` component |
| Self-Hosting | Rust + Postgres + Redis |
| Docs | https://chimely.dev |

---

## Human-in-the-Loop Support

Chimely is not a full HITL workflow engine. It can deliver in-app notifications that an application may use for human-facing alerts, requests, or status updates.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Raw notification table** | Agent must own inbox API behavior, real-time hints, and frontend inbox integration |
| **Human mailbox** | Routes notifications through a human email account instead of an application inbox |
| **Push-only transport** | Handles delivery hints but not a durable in-app notification inbox |
| **Hosted notification SaaS only** | Does not provide the same self-hostable Rust + Postgres + Redis infrastructure |

---

## Use Cases

- **Agent status updates** — agent writes task completion, failure, or progress notifications to an end user's in-app inbox
- **In-app alerts** — agent delivers product alerts without owning email, SMS, or push-channel logic
- **Approval prompts** — agent notifies a user that application-side approval or review is needed
- **Self-hosted notification infrastructure** — teams run the notification inbox stack alongside their own application
