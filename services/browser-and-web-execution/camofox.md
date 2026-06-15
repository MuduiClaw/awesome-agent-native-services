# CamoFox Browser

> **"Stealth headless browser for AI agents — bypass Cloudflare, bot detection, and anti-scraping."**

| | |
|---|---|
| **Website** | https://github.com/jo-inc/camofox-browser |
| **Docs** | https://github.com/jo-inc/camofox-browser |
| **GitHub** | https://github.com/jo-inc/camofox-browser |
| **Stars** | [![GitHub Stars](https://img.shields.io/github/stars/jo-inc/camofox-browser?style=social)](https://github.com/jo-inc/camofox-browser) |
| **Classification** | `agent-native` |
| **Category** | [Browser & Web Execution Services](README.md) |
| **License** | MIT |

---

## Official Website

https://github.com/jo-inc/camofox-browser

---

## Official Repo

https://github.com/jo-inc/camofox-browser

---

## How to Use (Agent Onboarding)

```bash
npm install -g camofox-browser
camofox-browser --help
```

Run the browser server, connect an agent via its REST/automation surface, and use isolated browser sessions for sites that block ordinary headless browsers.

---

## Agent Skills

**Status:** ⚠️ No official portable Agent Skill package found.

---

## MCP

**Status:** ⚠️ No official MCP server found in the main repository at time of listing.

---

## What It Does

CamoFox Browser is an anti-detection browser server for AI-driven web automation. It wraps a stealth browser runtime with a server/CLI interface so agents can open pages, maintain sessions, capture screenshots, extract content, and complete web tasks without exposing raw credentials or relying on a human-operated browser window.

---

## Why It Is Agent-Native

| Criterion | Evidence |
|---|---|
| **Agent-first positioning** | The official repository describes it as a stealth headless browser for AI agents. |
| **Agent-specific primitive** | Agent-facing browser sessions, structured command output, tab/page control, screenshots, and content extraction. |
| **Autonomy-compatible control plane** | An agent can start the server and drive browsing actions programmatically without per-click human approval. |
| **M2M integration surface** | CLI/server automation surface designed for coding agents and LLM-powered automation. |
| **Identity / delegation** | Browser profiles and credential injection patterns let a host delegate web access to the browser without putting secrets directly in the LLM transcript. |

---

## Primary Primitives

| Primitive | Description |
|---|---|
| **Stealth browser session** | Headless browser context hardened against common bot-detection signals. |
| **Server/CLI control** | Non-interactive browser lifecycle and navigation from scripts or agents. |
| **Credential-safe profiles** | Keep credentials in browser-side profiles instead of exposing them to the agent text stream. |
| **Screenshots and extraction** | Return visual or text artifacts to the agent for reasoning and follow-up actions. |

---

## Autonomy Model

1. Agent starts or connects to the CamoFox Browser server.
2. Agent opens a page or reuses an authenticated profile.
3. Agent navigates, observes page state, extracts information, and submits actions.
4. Browser-side profiles and automation boundaries constrain delegated access.

---

## Identity and Delegation Model

- Browser profiles represent delegated web identity.
- Credentials can be injected into the browser runtime while remaining outside the LLM context.
- Sessions can be separated per task, site, or agent to reduce cross-run leakage.

---

## Protocol Surface

| Interface | Detail |
|---|---|
| CLI | Install and operate browser sessions from terminal workflows |
| Browser server | Programmatic browser automation endpoint for agents |
| Playwright/Puppeteer-style ecosystem | Designed as a drop-in automation browser for existing agent stacks |

---

## Human-in-the-Loop Support

Optional. Humans can create or refresh browser profiles, but agents can run normal browsing loops autonomously once the runtime is available.

---

## Why Generic Alternatives Do Not Qualify

| Alternative | Why It Fails |
|---|---|
| **Plain headless Chrome** | Commonly fingerprinted and blocked; does not provide agent-specific credential-safety guidance. |
| **Manual browser** | Requires a human to operate the session. |
| **Generic scraping library** | Lacks full browser state, screenshots, and authenticated session delegation. |

---

## Use Cases

- Coding agents that need to inspect authenticated web apps safely
- Research agents navigating sites that block standard headless browsers
- QA agents exercising web flows with screenshots and stateful sessions
- Data agents extracting dynamic pages requiring JavaScript execution
