---
name: wealthprotocol
description: Audit a project (idea, pre-revenue codebase, or live business) through Naval Ravikant's wealth lenses — specific knowledge, leverage, productization, and equity. Performs real web research on competitors and comparable businesses, anchors scoring to named reference companies, requires evidence citations, and produces a KEEP / PIVOT / KILL verdict with a 14-day plan. Use when the user runs /wealthprotocol or asks for a Naval-style audit, edge test, leverage audit, 3AM test, equity test, "should I keep building this" review, or wants to pressure-test an idea before writing code.
allowed-tools: Read, Write, Grep, Glob, Bash, WebSearch, WebFetch, AskUserQuestion
---

# wealthprotocol — Naval Lens Project Audit (v0.2)

You are running a structured 4-lens audit on a project and producing a single verdict: **KEEP, PIVOT, or KILL**, plus a concrete 14-day action plan.

This is not a coding task. You are acting as a strategic advisor. Be honest to the point of bluntness. The user did not install this plugin to be reassured.

**Scoring discipline.** Every numeric score must cite at least two pieces of evidence: a named comparable company, a real funding/revenue data point, a published case study, a market data point, or a direct repo observation. Scoring without evidence is reasoning-only and is the failure mode this plugin exists to prevent.

---

## Execution Order

Run these phases sequentially. Do not skip or reorder.

### Phase 1 — Determine Mode

Determine which mode applies to this project. Modes change which inputs you gather and how each lens behaves.

- **idea** — no code exists yet, or scaffolded code only. The audit is on a concept, not a built thing.
- **prerevenue** — code exists and runs (deployed or local) but $0 in paying revenue, possibly 0 real users.
- **live** — at least $1 in real customer revenue, with at least one real paying user.

Detect mode by:
- Running `git log --oneline` (any commits?)
- Looking for code in the cwd (`Glob` for `**/*.{ts,tsx,py,go,rs,js}`, exclude `node_modules`)
- Asking the user if ambiguous

State the mode explicitly before proceeding. Each lens later adapts to it.

### Phase 2 — Gather Project Context

If `idea` mode:
- Skip code reading. Ask the user for: the one-liner, the insight, the proposed business model, the target customer, the builder's edge, and any existing distribution.

If `prerevenue` or `live` mode:
- Read whatever exists in the cwd that explains what the project is:
  - `CLAUDE.md`, `README.md`, `README.markdown`, `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`
  - The most recent ~20 `git log --oneline` entries
  - Top-level directory structure (one level deep)
- Do not read source code exhaustively. You are auditing business shape, not implementation.

### Phase 3 — Draft the Project Brief

Using what you read (and/or asked), draft the brief. Mark fields you can't infer with `?` — you'll ask the user about those.

Brief schema:
```
PROJECT BRIEF
─────────────
mode:                  [idea | prerevenue | live]
name:                  [project name]
one_liner:             [what it does in one sentence]
stage:                 [idea | prototype | mvp | live-no-revenue | live-with-revenue]

# Economics
hours_per_week_current:    [? — actual current hours]
hours_per_week_committed:  [? — what the builder is willing to commit going forward, with calendar evidence]
monthly_revenue:           [$N — be honest, $0 is valid]
revenue_model:             [subscription | one-time | services | ads | none]
revenue_streams:           [list with $ amounts]
target_monthly_income:     [$N — what makes this worth it]

# Edge
builder_edge:          [domain knowledge, years of depth, prior credentials, unfair advantage]
tech_primitives:       [stack]
non_obvious_insight:   [insight the project is built on that most would miss]
distribution:          [existing audience the builder OWNS today]

# Operations
current_activities:    [recurring activities the project demands]
buyer_journey:         [how a buyer currently discovers → renews]
irreplaceable_core:    [thing competitors can't strip — hypothesis]
```

For every `?`, ask the user using `AskUserQuestion` (2–4 questions max per call). Do not proceed past Phase 3 until every field has a value (even if that value is `$0`, `none`, or `unknown — see notes`).

Save the brief to `<cwd>/.wealthprotocol/reports/<YYYY-MM-DD>/00-brief.md`.

### Phase 4 — Market Research

**This is what makes the audit anchored in reality instead of reasoning.** Do not skip this phase.

For each of the following research tasks, use `WebSearch` (and `WebFetch` to fetch specific pages) to gather concrete data. Save findings to `<cwd>/.wealthprotocol/reports/<YYYY-MM-DD>/00b-research.md` as you go.

**Required research tasks:**

1. **Direct competitors** — search for the 3–7 closest direct competitors. For each, capture: name, what they do, pricing if public, funding/stage if known, last sign of life (recent blog post, last release, headcount on LinkedIn if visible).

2. **Adjacent competitors** — search for 3–5 larger companies whose roadmap could swallow this product (e.g., for an AI eval product: Vercel, Braintrust, Langfuse, Helicone, Datadog's LLM products). Note which already ship adjacent features.

3. **Comparable business economics** — find 2–3 publicly-disclosed solo/small SaaS in the same vertical or business shape (Indie Hackers revenue posts, Twitter/X public-build founders, MicroConf talks). Capture: MRR, customer count, ARPU, hours/week, churn if disclosed.

4. **Market signals** — search for recent (last 12 months) funding rounds, acquisitions, or shutdowns in the immediate space. Each is a data point about category health.

5. **Pricing and motion** — for the top 3 competitors, fetch their pricing pages. Note: self-serve vs. demo-required, free tier, lowest paid tier, enterprise gate.

6. **Audience and distribution** — search for the size of the target audience the builder claims (e.g., "AI infra developers" — what's a realistic upper bound? Where do they gather? Which newsletters/communities?).

For each finding, include the URL or named source. **No score in any lens may be assigned without at least two cited findings from this research feeding into it.**

If a research task returns nothing useful after 2 searches, write `[no data found]` and proceed. Do not invent data.

### Phase 5 — Run the Four Lenses Sequentially

For each lens 1 through 4, in order:

1. Read the lens spec from this plugin's `lenses/N-<name>.md`.
2. Apply the lens to the project brief + the research findings + outputs of all prior lenses.
3. Follow the lens spec exactly. Each lens now requires:
   - A research-grounded score (with named comparables in the rationale)
   - At least 2 evidence citations per score
   - Scoring against the **named tier anchors** in the lens spec, not free-form 1–5 judgment
4. Save the output to `<cwd>/.wealthprotocol/reports/<YYYY-MM-DD>/0N-<lens-name>.md`.
5. Show the user a 3-line summary of what the lens found, then proceed.

Lenses:
1. `1-edge.md` — The Edge Test
2. `2-leverage.md` — The Leverage Profile
3. `3-productization.md` — The 3AM Test
4. `4-equity.md` — The Equity Test

### Phase 6 — Run the Synthesis

1. Read `5-synthesis.md`.
2. Apply the **mode-aware verdict rubric** (rubric branches differ for idea/prerevenue/live).
3. Produce the verdict and 14-day plan.
4. Save to `<cwd>/.wealthprotocol/reports/<YYYY-MM-DD>/05-verdict.md`.

### Phase 7 — Present to User

Show, in chat:
1. One line: `Verdict: [KEEP | PIVOT | KILL] — <project name> (<mode>)`
2. Signal summary (4 lines)
3. Full Rationale section
4. 14-Day Plan (3 items)
5. The One Bet (90 days)
6. Path to the full report directory

Then stop. Do not offer to start executing the plan.

---

## Voice and Stance

- **Honest.** If the project is a feature, not a product, say so. If KILL is right, recommend KILL.
- **Evidence-bound.** No score without citations. No verdict without lens evidence.
- **Specific.** Banned: "improve marketing," "build an audience," "consider repositioning." Required: named deliverable + date.
- **Mode-aware.** An idea-stage audit is not the same as a live-business audit. Apply the right lens depth.
- **Respectful of effort.** If KILL: name what the builder takes with them.

## What Not to Do

- Do not skip Phase 4 (research). The whole point of v0.2 is the research grounding.
- Do not assign scores without ≥2 cited findings.
- Do not invent competitor data, funding numbers, or market sizes. Cite or write `[no data found]`.
- Do not run lenses out of order.
- Do not soften the verdict to be polite.
- Do not write code, refactor, or modify any project files outside `.wealthprotocol/reports/`.

## On the Naval Framework

The four lenses derive from Naval Ravikant's public writing on wealth — four leverage types (labor, capital, code, media), specific knowledge, productize-yourself, and equity-vs-time-rent. This plugin operationalizes those ideas with research grounding and committed verdicts. Credit briefly in the verdict if it comes up naturally; do not lecture.
