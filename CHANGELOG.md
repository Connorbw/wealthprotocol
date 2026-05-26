# Changelog

## 0.2.0 — 2026-05-25

**The "actually do the research" release.** v0.1 scored projects using model intuition. v0.2 grounds every score in real-world evidence.

### Added
- **Mode awareness** — audits now run differently for `idea` (no code), `prerevenue` (code, $0 revenue), and `live` (paying customers) projects. Each lens adapts.
- **Phase 4: Market Research** — the orchestrator now performs real web research before scoring: direct competitors, adjacent threats, comparable business economics, market signals, competitor pricing/motion, audience size. Saved to `00b-research.md` in the report directory.
- **Tiered scoring anchors** — every lens now scores against 5 named tiers with real-world reference examples (Stripe, Linear, Pieter Levels, ConvertKit, etc.) instead of free-form 1–5.
- **Evidence requirements** — no score may be assigned without ≥2 cited findings from research. The synthesis verdict includes an evidence audit confirming this.
- **Mode-aware verdict rubric** — synthesis now has explicit branches for idea/prerevenue/live, with rules that handle pre-revenue-bet-dormant projects directly (previously required judgment override).
- **Leverage vacuum vs. trap distinction** — Lens 2 now separates "low-leverage because hours are poorly spent" from "low-leverage because no hours are being spent at all." Different recommendations.
- **Pre-revenue sub-classification** — Lens 4 distinguishes `pre-revenue-bet-active` (10+ hr/wk committed) from `pre-revenue-bet-dormant` (<10 hr/wk, drifting).

### Changed
- `allowed-tools` now includes `WebSearch` and `WebFetch` for research phase.
- Synthesis prompt now requires citing lens findings by name, not paraphrasing.
- Every lens has a `Research Required` section listing what must be gathered before scoring.
- Banned-actions list expanded with named-deliverable examples.

### Why this matters
v0.1 had three weaknesses surfaced by the first live run (against DriftDetect):
1. **Stale data** — model training cutoffs meant recent competitor moves, funding, shutdowns weren't reflected
2. **Unanchored scoring** — "score 1–5" produced inconsistent reads across runs
3. **No external evidence** — the model never *checked* anything

v0.2 fixes all three with the research phase, named-tier anchors, and required citations.

### Known limitations
- Research quality depends on what's publicly findable. Niche B2B markets with private data return less. Lens specs require writing `[no data found]` rather than inventing.
- The orchestrator estimates ~5–15 minutes of research per audit. Worth it; not free.
- `idea` mode is the least-tested branch. The first user to run it should report back.

---

## 0.1.0 — 2026-05-25

Initial scaffold. Four-lens audit (Edge, Leverage, 3AM Test, Equity) + synthesis verdict. Single-mode (assumed brownfield). Scoring is model-intuition based. Released, then promptly outgrown.
