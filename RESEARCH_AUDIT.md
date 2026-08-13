# Research & Freshness Audit — 2026-08-13

This note records the latest catalog-wide research and freshness pass. New
services remain issue-first; this file records the scope, evidence window, and
maintenance work that was actually completed.

## Scope

- Reviewed official sources for candidates created, released, or materially
  active from 2026-07-13 through 2026-08-13.
- Reconciled the complete catalog inventory across `services/`, `README.md`,
  `skill.md`, and `llms.txt`.
- Audited website discovery, structured metadata, generated documentation,
  machine-readable entry points, Skills publishing, and deployment workflows.
- Rechecked the new Agent Harnesses & Operator Surfaces admission boundary,
  including purpose-built Codex HUDs.

## Applied catalog updates

- Added 21 source-backed dossiers across existing collections and the new Agent
  Harnesses & Operator Surfaces collection.
- Added the latest-month collection with 20 in-window arrivals; the older
  `anhannin/codex-hud` entry is intentionally included without a freshness badge.
- Reconciled 172 service files across 16 collections and repaired orphaned or
  duplicated index rows.
- Updated category guidance to distinguish runtime substrates, durable harnesses,
  and narrow live-agent operator surfaces.
- Recorded licensing, pre-1.0, audit, authentication, identity, and durability
  caveats where official sources exposed them.

## Agent-native infrastructure audit

- Confirmed the public site was agent-readable through its homepage but lacked
  same-origin `llms.txt` and `skill.md` endpoints before this update.
- Added a versioned JSON catalog and JSON Schema as the deterministic ingestion
  surface, while preserving Markdown dossiers as the editorial source material.
- Added validation for inventory integrity, machine artifacts, local links,
  generated pages, and public discovery endpoints.
- Updated canonical, sitemap, robots, and machine-discovery metadata to the
  `lihaorui.com/awesome-agent-native-services/` origin.
- Tightened Skills publishing and deployment gates so failures cannot be silently
  reported as successful.

## Evidence and acceptance

- Primary evidence came from official repositories, releases, documentation,
  hosted protocol files, package metadata, and live endpoints.
- Latest-month snapshots use 2026-08-13 UTC and are embedded in the affected
  dossiers rather than inferred from this audit date.
- Generated documentation must reproduce without diff; the public machine files
  must pass schema/parser checks and deployment smoke tests.
- Scheduled freshness automation treats this audit date as the catalog-wide
  review watermark. It does not imply that every legacy claim was independently
  reverified on this date.

## Freshness checklist for future passes

1. Re-run the generator and contract validator after any catalog change.
2. Re-check volatile onboarding commands, hosted MCP endpoints, releases, license
   boundaries, and authentication requirements against official sources.
3. Keep per-entry verification evidence explicit; do not convert this broad audit
   date into a fabricated service-level `verified_at` value.
4. Open an issue before admitting a new service or category unless the change is
   an obvious factual or broken-link correction.
5. Run a broad research pass before the freshness watermark exceeds 45 days.
