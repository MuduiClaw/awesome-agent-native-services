# Research & Freshness Audit — 2026-06-12

This note records the latest broad review pass requested by maintainers. It is intentionally lightweight: the catalog remains issue-first for new service files, but this file captures high-signal ecosystem findings and freshness work already applied in this PR.

## Scope

- Searched for high-signal, agent-native services and skill hubs with strong discussion or visible ecosystem adoption.
- Reviewed the repository's current category coverage, generated-docs workflow, skill publishing workflow, and agent onboarding surfaces.
- Prioritized updates that make the repository itself easier for coding agents to add as a source.

## Applied updates

- Added a Claude Code-compatible plugin marketplace at `.claude-plugin/marketplace.json`.
- Added a Claude Code plugin manifest at `.claude-plugin/plugin.json` that exposes the existing `.skills/` folders without duplicating skill content.
- Added `SKILLS_HUB.md` with Claude Code, ClawHub/OpenClaw, and manual `SKILL.md` installation instructions.
- Updated the root README and `llms.txt` so agents can discover the repository as a skills source, not only as a Markdown catalog.
- Refreshed stale category service counts in the root README.
- Bumped skill metadata `catalog-version` values to `2026-06-12`.

## High-signal ecosystem findings

These were reviewed as candidate hubs or sources. Some are already cataloged as first-class service entries (for example ClawHub); others are tracked as ecosystem hubs until a maintainer opens/approves a dedicated service issue.

| Candidate | Signal observed | Current catalog action |
|---|---|---|
| Claude Code plugin marketplaces | Official Claude Code docs describe GitHub-hosted marketplaces that use `.claude-plugin/marketplace.json`, with users adding a source via `/plugin marketplace add owner/repo`. | Implemented this repo as a Claude Code marketplace. |
| ClawHub | Existing catalog entry and `.skills/` publish workflow; remains the canonical OpenClaw-style skill registry path for this repo. | Kept as first-class Tool Access & Integration entry and install path. |
| MiniMax Skills | High-signal curated `SKILL.md` packs for coding agents; already tracked in Ecosystem Hubs. | Kept as ecosystem hub. |
| Agensi | Marketplace for AI agent skills with paid/free downloads, security scanning, broad agent compatibility, and an MCP endpoint for agent-side discovery. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |
| SkillsMP | Large public `SKILL.md` index with source/repository context and API access for analytics/search. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |
| mdskills.ai | Community marketplace for skills, plugins, MCP servers, rules, and tools with CLI install flow and quality/security review. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |
| sklz.city | MCP-native skill runtime and marketplace with import, augmentation, monetization, isolation, and security-review primitives. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |
| SkillCrate | Vertical skill marketplace where each skill is a GitHub repo with `SKILL.md` and MCP server packaging for Amazon seller operations. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |
| CryptoSkill | Crypto-focused registry of open-source skills and MCP servers for Claude Code, OpenClaw, Codex, and related agents. | Added to Ecosystem Hubs / skill-hub pointers rather than a service file pending issue review. |

## Freshness checklist for future passes

1. Re-run `bash scripts/build-github-pages.sh && git diff --quiet -- docs/index.md docs/categories` after any README or `services/**` edit.
2. Re-check services whose onboarding depends on volatile install commands (`npx`, `uvx`, hosted MCP URLs, Claude plugin marketplace commands).
3. For newly found hubs, open an issue first unless the change is only an ecosystem pointer or obvious documentation fix.
4. Treat skill-hub entries as boundary cases unless they provide a machine-to-machine runtime, registry API, MCP endpoint, or agent-installable source with clear provenance.
