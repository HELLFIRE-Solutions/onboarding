# Onboarding session: compliance-layer (module 11), Stage 1

Date: 2026-07-24. Format: [session-template.md](../docs/session-template.md), second real run of the template — first against a **non-CLI module**.
Trainee: Bob (dogfooding on himself).

## Why this module

compliance-layer (11) is pure documentation: one `docs/standard.md` plus three supporting docs (`legitimate-interest.md`, `data-residency.md`, `ai-act-classification.md`). No CLI, no `pytest`, no `.env.example`, nothing to `pip install`. The template's own note ("modules without a CLI can collapse phases 3–4 into one block") had never been tested against a real case — this is that test.

## Phase 1 — Context and why (done, no change needed)

Module 11: documents HELLFIRE's own compliance approach (legitimate interest, data residency, AI Act risk classification) as an internal standard, built on TETA+PI's TWIRA methodology. Entry ticket to the German market — same framing as the original project plan. Stage 1 = internal standard; Stage 2 (sellable audit product) not started. This phase worked exactly as written; module shape didn't matter here.

## Phase 2 — Architecture decisions (done, took longer than the template budgets)

No `docs/architecture.md` — the equivalent is `docs/standard.md`, plus the decisions are actually spread across all three sub-docs, not concentrated in one file the way gtm-agent's single `architecture.md` was:
1. **Legitimate interest** — adopts gtm-agent's `LegitimateInterestRecord` unchanged as the HELLFIRE-wide schema; compliance-layer's own contribution is the audit/export *spec* (coverage check, staleness check, opt-out completeness, balancing-test quality), not a schema change.
2. **Data residency** — `fra1` (Frankfurt) confirmed for the shared server; flags real open gaps (HubSpot's EU-hosting is a paid-tier question, Anthropic API DPA not yet verified) rather than just asserting compliance.
3. **AI Act classification** — borrows TWIRA's *shape* (tiered, evidence-based, re-validated, audit-trailed) applied to AI Act risk tiers instead of trust ranking; classifies every HELLFIRE module (gtm-agent = limited risk, most others = minimal, inhouse-llm/onboarding out of scope for different reasons) and names concrete re-classification triggers.

**Finding:** for a documentation-only module, phase 2 isn't a 15–20 min walkthrough of one file — it's most of the session, because there's no separate code layer to demo later. Budget 30–40 min here, not 15–20, when the module has no CLI.

## Phase 3 — Install and configuration (does not apply)

Nothing to install. No dependencies, no `.env`, no test suite to run. This isn't "partially blocked" like gtm-agent's HubSpot/domain gap — it's a phase with zero content for this module shape. Skipped outright rather than compressed.

## Phase 4 — Guided run-through (adapted, not skipped)

There's no workflow to execute, but the template's "collapse 3–4 into one block" note undersells what actually filled this slot: **tracing a concrete future scenario through the documents**, not running anything. Two scenarios walked:
- A future module session (say, office-agent) picks a new third-party SaaS that touches personal data → per `data-residency.md` "How future modules should apply this," that session should record a one-line EU-residency confirmation in its own `docs/architecture.md` at integration-choice time, not defer to a later compliance-layer audit.
- A future module changes scope (e.g. office-agent starts drafting hiring-rejection replies) → per `ai-act-classification.md`'s re-classification triggers, that's the exact "client uses a template outside HELLFIRE's own risk tier" trigger, and the classification table must be re-run for that deployment, not inherited from HELLFIRE's internal use.

Both scenarios were answerable directly from the docs with no ambiguity — the guided run-through worked, it just isn't a CLI transcript.

## Phase 5 — Guardrails and limits (done, template held as-is)

Explicit non-goals and scope limits are unusually clear for this module (arguably clearer than a CLI module's guardrails, since there's no code to infer them from — they have to be written down):
- No audit/questionnaire product yet (that's Stage 2), no changes to gtm-agent's code/schema, no legal sign-off — these are HELLFIRE's internal working interpretation, not legal advice.
- Explicit "do not resolve this by picking whichever answer is more convenient" flag on the Art. 50 transparency question for gtm-agent — a genuinely open item routed to real counsel rather than quietly assumed.
- Non-goal inherited HELLFIRE-wide: no automated scraping/messaging on platforms whose ToS prohibits it.

This phase needed no adaptation — "what does the module refuse to do / what's explicitly out of scope" is shape-agnostic.

## Phase 6 — Readiness check (checklist wording didn't fit; content did)

Template wording ("install from scratch," "ran the main workflow") doesn't map cleanly onto a doc-only module. Re-read against what the checklist is actually *for* (can this person operate independently, and do they know the boundaries):

- [x] Can locate and summarize what each of the four docs covers without re-reading them cold
- [x] Can name the three components and why each exists (not just what)
- [x] Can trace a new scenario (new SaaS vendor, new module's risk tier) through the docs to the right answer
- [x] Knows what's explicitly *not* done yet (Stage 2 audit product, legal sign-off) and wouldn't mistake this for a finished client-facing deliverable
- [x] Knows where to go on a blocker — `STATE.md` session 11 section, or actual legal counsel for the flagged open items

Full pass, no partial items — unlike gtm-agent's session, nothing here was blocked on an external account, because a documentation module has no external account dependency by nature.

## Gaps found during the session

None in compliance-layer's own docs — same result as the gtm-agent run. Two real gaps found in the **template itself**, both fixed in this pass (see below): phase 3 needs an explicit "N/A" path instead of silently not applying, and phase 6's checklist wording assumed a CLI module.

## Verdict on the template's own open question

The template asked: does the 90–120 min / 6-phase structure make sense for a module without code? **Partially.** The 6 phases as *categories* hold (context, decisions, setup, applied walkthrough, limits, readiness) — nothing needed to be added or removed at that level. What breaks is the CLI-shaped assumptions baked into three of them: phase 3 assumes there's always something to install (there isn't), phase 4 assumes a runnable workflow (the substitute — tracing a scenario through docs — works but isn't what "guided run-through" suggests on its own), and phase 6's checklist language assumes install + run steps exist. Total time for this session landed around 70–80 min (longer phase 2, no phase 3, shorter phase 4) — shorter than the 90–120 min band, not longer, because a missing phase outweighs one expanded phase.

## Next steps

- `session-template.md` updated in this pass: phase 3 gets an explicit "N/A for doc-only modules" note instead of relying on the reader to infer it; phase 4's description now names "trace a scenario through the docs" as the non-CLI substitute, not just "collapse 3–4"; phase 6 checklist reworded to be shape-neutral; a duration note added for doc-only modules (~60–80 min, not 90–120).
- Two real-module runs now done (gtm-agent = CLI-shaped, compliance-layer = docs-only). Per the template's own threshold (≥2–3 runs across different shapes before Stage 2 starts), one more run against a third shape (e.g. an infra/RAG-pipeline module once one has real material, or office-agent once it has code) would be worth doing before treating the template as stable enough for Stage 2.
