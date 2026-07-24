# Onboarding-session template (Etap 1: dogfooding on ourselves)

Status: first version, verified on one real run ([`gtm-agent`](../sessions/2026-07-20-gtm-agent.md)). Not yet verified on a differently-shaped module (non-CLI, infra module) — expect revisions after further runs.

Audience for this version: Bob, on himself ("team" = 1 person). The template is deliberately tied to the real shape of catalog modules (Python CLI package, `README.md` + `docs/architecture.md` + `docs/demo-ready-criteria.md`, `.env.example`, `pytest`) — Etap 2 will adapt it for client staff who don't read code.

## When it applies

A module should go through an onboarding session once it has **real material**: runnable code, and at least one committed architecture/demo-ready document. A module with "pushed to GitHub" status (bare skeleton, no code) isn't ready yet — a session on it would be an empty exercise.

## Materials (gather before the session)

- `<module>/README.md` — quick start, current status
- `<module>/docs/architecture.md` (if it exists) — decisions locked in and why
- `<module>/docs/demo-ready-criteria.md` (if it exists) — what "demoable to a client" actually means
- `<module>/.env.example` — which secrets/accounts are needed for a real run
- A test suite (`pytest tests/` or equivalent) — to verify the install actually works without relying on live external accounts
- Sample input data, if the module consumes any (e.g. `data/leads.example.csv` in gtm-agent)

## Session structure (target: 90–120 min, one module at a time)

| # | Phase | Duration | Goal | Material |
|---|---|---|---|---|
| 1 | Context and why | 5–10 min | What problem the module solves, where it sits in the catalog (number, dependencies on other modules) | `README.md`, intro paragraph |
| 2 | Architecture decisions | 15–20 min | Walk through the decisions locked in and **why** (not just what) | `docs/architecture.md` |
| 3 | Install and configuration | 20–30 min | Install dependencies, fill in `.env`, run the test suite locally | `.env.example`, `pytest` |
| 4 | Guided run-through | 30–45 min | Walk a real (or sample) workflow end-to-end, step by step, narrating what's happening and why at each step | sample data, the module's CLI/UI |
| 5 | Guardrails and limits | 10–15 min | What the module **refuses** to do and why (e.g. gtm-agent refuses to draft without a `LegitimateInterestRecord`), where a human must explicitly approve | `docs/architecture.md` §guardrails, the enforcement-check code |
| 6 | Readiness check | 10 min | Can the person who went through the session run the main workflow independently, and do they know when to stop and ask | checklist below |

Modules without a CLI (infra, pure documentation, a RAG pipeline with no separate frontend) can collapse phases 3–4 into one "walk through a live example" block — session length depends on module complexity, not a fixed rule.

## Readiness checklist (phase 6)

Passed if every item is a yes:
- [ ] Can install the module from scratch using `README.md` alone, with no hints
- [ ] Can name 2–3 architecture decisions and why, not just what
- [ ] Went through the main workflow at least once (real or sample data)
- [ ] Knows which actions the system takes automatically and which need explicit approval
- [ ] Knows who/where to go if something breaks (the module's repo issues, `STATE.md`)

## Session record

Each run is documented as its own file in `sessions/YYYY-MM-DD-<module>.md`: what was covered, what worked, where the session hit an external blocker (e.g. a missing account), what documentation gaps surfaced during training. That's the dogfooding loop: gaps found during an onboarding session become issues/fixes in the module itself, not just a note here.

## What changes in Etap 2 (not now)

Standardized package for client staff:
- Phase 2 simplifies — client staff don't read `architecture.md` verbatim; decisions need translating into "what this means for you" business language
- Phase 3 becomes "the module is already installed and configured" — the client doesn't install from scratch
- Video/screencast gets added on top of the guided run-through (phase 4), not just a text guide
- The phase-6 checklist becomes a formal sign-off, not a self-check
- One client session can cover several modules depending on what they bought

Don't start Etap 2 until there are ≥2–3 real template runs across differently-shaped modules (currently 1 — a CLI module).
