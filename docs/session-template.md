# Onboarding-session template (Etap 1: dogfooding on ourselves)

Status: second version, verified on two real runs: [`gtm-agent`](../sessions/2026-07-20-gtm-agent.md) (CLI module) and [`compliance-layer`](../sessions/2026-07-24-compliance-layer.md) (documentation-only module — no code, no CLI). The 6 phases as categories held on both; the CLI-specific assumptions in phases 3, 4, and 6 below have been adjusted based on the second run. Not yet verified on a third shape (infra/RAG-pipeline module) — expect further revisions.

Audience for this version: Bob, on himself ("team" = 1 person). The template is deliberately tied to the real shape of catalog modules (Python CLI package, `README.md` + `docs/architecture.md` + `docs/demo-ready-criteria.md`, `.env.example`, `pytest`) — Etap 2 will adapt it for client staff who don't read code.

## When it applies

A module should go through an onboarding session once it has **real material**: runnable code, and at least one committed architecture/demo-ready document. A module with "pushed to GitHub" status (bare skeleton, no code) isn't ready yet — a session on it would be an empty exercise.

## Materials (gather before the session)

- `<module>/README.md` — quick start, current status
- `<module>/docs/architecture.md` (if it exists) — decisions locked in and why. Documentation-only modules may not have a file with this exact name; look for whatever plays the equivalent role (e.g. compliance-layer's `docs/standard.md` plus its sub-docs) and expect the "decisions" material to be spread across more than one file
- `<module>/docs/demo-ready-criteria.md` (if it exists) — what "demoable to a client" actually means. Not every module has one (compliance-layer doesn't — its own "what Etap 1 deliberately does not do" section serves a similar scoping purpose)
- `<module>/.env.example` — which secrets/accounts are needed for a real run. **Only applicable if the module has a runtime.** Doc-only modules have nothing here — don't treat its absence as a gap
- A test suite (`pytest tests/` or equivalent) — to verify the install actually works without relying on live external accounts. Same caveat: N/A for doc-only modules
- Sample input data, if the module consumes any (e.g. `data/leads.example.csv` in gtm-agent)

## Session structure (target: 90–120 min for a CLI-shaped module, ~60–80 min for a documentation-only module — see below)

| # | Phase | Duration | Goal | Material |
|---|---|---|---|---|
| 1 | Context and why | 5–10 min | What problem the module solves, where it sits in the catalog (number, dependencies on other modules) | `README.md`, intro paragraph |
| 2 | Architecture decisions | 15–20 min (CLI module) / 30–40 min (doc-only module) | Walk through the decisions locked in and **why** (not just what) | `docs/architecture.md`, or the doc(s) playing that role |
| 3 | Install and configuration | 20–30 min, **N/A for doc-only modules** | Install dependencies, fill in `.env`, run the test suite locally | `.env.example`, `pytest` |
| 4 | Guided run-through | 30–45 min | Walk a real (or sample) workflow end-to-end, step by step, narrating what's happening and why at each step. **For a module with no runnable workflow, substitute:** trace 1–2 concrete future-usage scenarios through the documents to a specific answer (e.g. "a new module picks a SaaS vendor — what does this module require it to check, and where does that get recorded?") | sample data + the module's CLI/UI, or the docs themselves for a scenario walkthrough |
| 5 | Guardrails and limits | 10–15 min | What the module **refuses** to do and why (e.g. gtm-agent refuses to draft without a `LegitimateInterestRecord`), where a human must explicitly approve, what's explicitly out of scope / not done yet | `docs/architecture.md` §guardrails / enforcement-check code, or the doc-only module's own "what this deliberately does not do" section |
| 6 | Readiness check | 10 min | Can the person who went through the session operate independently, and do they know when to stop and ask | checklist below |

**Why phase 3 is N/A rather than "collapsed" for doc-only modules:** an earlier version of this template said non-CLI modules "collapse phases 3–4 into one block" — tested against compliance-layer (see [session record](../sessions/2026-07-24-compliance-layer.md)) and that undersold it. Phase 3 has literally nothing to fill it (no install step exists) and should just be skipped, not merged. Phase 4 does have real content for a doc-only module — the scenario-tracing substitute above — it isn't skipped, it's just not a CLI transcript. Net effect on a doc-only module: phase 2 grows (the "architecture" material *is* most of the module, with no separate code layer to reference later), phase 3 disappears, phase 4 shrinks a little — total session lands shorter (~60–80 min) than the CLI-module band, not longer.

## Readiness checklist (phase 6)

Passed if every item is a yes. Items marked **(CLI)** apply only to modules with a runtime; for doc-only modules use the paired **(doc)** item instead.
- [ ] **(CLI)** Can install the module from scratch using `README.md` alone, with no hints — or — **(doc)** can locate and summarize what each doc in the module covers, without re-reading cold
- [ ] Can name 2–3 decisions locked in by the module and why, not just what
- [ ] **(CLI)** Went through the main workflow at least once (real or sample data) — or — **(doc)** can trace a new concrete scenario through the docs to the right answer
- [ ] Knows which actions the system takes automatically and which need explicit approval — or, for a doc-only module, what's explicitly declared out of scope / not done yet
- [ ] Knows who/where to go if something breaks (the module's repo issues, `STATE.md`) — or, for a compliance/legal-adjacent doc module, where real sign-off (e.g. legal counsel) is still required before treating it as final

## Session record

Each run is documented as its own file in `sessions/YYYY-MM-DD-<module>.md`: what was covered, what worked, where the session hit an external blocker (e.g. a missing account), what documentation gaps surfaced during training. That's the dogfooding loop: gaps found during an onboarding session become issues/fixes in the module itself, not just a note here.

## What changes in Etap 2 (not now)

Standardized package for client staff:
- Phase 2 simplifies — client staff don't read `architecture.md` verbatim; decisions need translating into "what this means for you" business language
- Phase 3 becomes "the module is already installed and configured" — the client doesn't install from scratch
- Video/screencast gets added on top of the guided run-through (phase 4), not just a text guide
- The phase-6 checklist becomes a formal sign-off, not a self-check
- One client session can cover several modules depending on what they bought

Don't start Etap 2 until there are ≥2–3 real template runs across differently-shaped modules (currently 2 — one CLI module, one documentation-only module; still worth one more against a third shape, e.g. an infra/RAG-pipeline module, before treating the template as stable).
