# HELLFIRE AI Solutions — Onboarding / Training

Module 8. Documents the process of training our own "team" (currently Bob) to use each module; forms a reusable onboarding-session template (structure, duration, materials).

**Dogfooding → template:** a standardized onboarding package (sessions + documentation + video/guides) for training client staff. A separate paid catalog item, not a free step in implementation.

## Structure

- [`docs/session-template.md`](docs/session-template.md) — onboarding-session template (6 phases, 90–120 min for CLI modules / 60–80 min for documentation-only modules, materials, readiness checklist). Second version, verified on two real runs across different module shapes.
- `sessions/` — records of real template runs against each module, as they get real material. So far: [`2026-07-20-gtm-agent.md`](sessions/2026-07-20-gtm-agent.md) (CLI module), [`2026-07-24-compliance-layer.md`](sessions/2026-07-24-compliance-layer.md) (documentation-only module).

**Status:** Stage 1 in progress (2026-07-24) — session template built and verified twice: module 05 (gtm-agent, CLI-shaped) and module 11 (compliance-layer, documentation-only). Both runs found no gaps in the target module's own docs; the second run found and fixed real gaps in the template itself (phase 3 "N/A" handling, phase 4's non-CLI substitute, phase 6 checklist wording). Modules 06, 07, 08, 09, 10 are still pushed skeletons with no code; template hasn't been run against them. Stage 2 (standardized package for client staff) not started — one more run against a third module shape (e.g. an infra/RAG-pipeline module) recommended before starting it.

**License:** MIT.
