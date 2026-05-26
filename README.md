```
                    _ _   _                     _                  _
__      _____  __ _| | |_| |__  _ __  _ __ ___ | |_ ___   ___ ___ | |
\ \ /\ / / _ \/ _` | | __| '_ \| '_ \| '__/ _ \| __/ _ \ / __/ _ \| |
 \ V  V /  __/ (_| | | |_| | | | |_) | | | (_) | || (_) | (_| (_) | |
  \_/\_/ \___|\__,_|_|\__|_| |_| .__/|_|  \___/ \__\___/ \___\___/|_|
                               |_|
```

**An honest second opinion on whether your project is worth building.**

A Claude Code plugin that audits any project — an **idea** on the drawing board, a **pre-revenue** codebase you've been sitting on, or a **live business** with paying customers — through Naval Ravikant's wealth lenses and tells you whether to **KEEP, PIVOT, or KILL** it.

[![Version](https://img.shields.io/badge/version-0.2.0-00d4ff)](./CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-3ddc97)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-plugin-ff4d6a)](https://claude.com/claude-code)

---

## What it does

```
$ /wealthprotocol
```

In any project directory, the plugin:

1. **Reads your repo** — `CLAUDE.md`, `README.md`, `package.json`, recent commits, structure (or asks you about the idea if no code exists)
2. **Does real market research** — finds direct competitors, adjacent threats, comparable business economics, current pricing, audience size — using live web search, not training data
3. **Asks you for what it can't infer** — hours/week, revenue, distribution, edge
4. **Runs four sequential audits** scored against named real companies (not free-form 1–5 vibes)
5. **Produces a dated report** with verdict, 14-day plan, and an evidence audit confirming every score is backed by ≥2 cited findings

```
Verdict: PIVOT — DriftDetect (prerevenue)

Edge:           no-edge — 2/5
Leverage:       leverage-vacuum — index 1.0/5.0
Productization: untested — 3/5
Equity:         pre-revenue-bet-dormant

→ 14-day plan: 3 named actions, each with date + deliverable
→ The one bet (90 days): become the voice, not the builder
```

---

## The four lenses

| # | Lens | The question it answers |
|---|---|---|
| 1 | **Edge Test** | Does this project sit at a rare intersection of knowledge only you can ship — or could a funded team replicate it in a quarter? |
| 2 | **Leverage Profile** | Where are your hours actually going? Labor, capital, code, or media? Is this a leverage trap or a leverage vacuum? |
| 3 | **3AM Test** | Does this project sell, ship, and support itself while you're asleep? Where does it break? |
| 4 | **Equity Test** | Is your revenue equity (compounds, outlives your hours) or time-rent (stops when you stop)? |
| 5 | **The Verdict** | Synthesis: KEEP, PIVOT, or KILL — plus the next 14 days. |

---

## Install

```
/plugin marketplace add Connorbw/wealthprotocol
/plugin install wealthprotocol@wealthprotocol
```

Then in any project repo (or empty dir, for idea-stage audits):

```
/wealthprotocol
```

Plan ~10–20 minutes for the run. Most of it is the research phase fetching competitor data and reading pricing pages.

---

## How the scoring is grounded

Every lens uses a **5-tier scoring scale anchored to real companies**, not free-form judgment. Example for the Edge Test:

| Score | Tier | Anchor |
|---|---|---|
| **5** | Category-defining edge | *Stripe at founding: Patrick + John Collison + Auctomatic exit — fewer than 50 people on earth had that combination of payment-API depth and engineering chops.* |
| **4** | Strong edge | *Linear: Karri Saarinen brought design-leadership taste from Airbnb/Uber + a small but engaged early-adopter audience.* |
| **3** | Real edge | *Pieter Levels launching Nomad List with deep nomad-lifestyle knowledge + a few thousand Twitter followers.* |
| **2** | Motivation edge only | *"I had this problem at work, so I built a tool" — succeeds ~5–10% of the time, almost always with concurrent audience-building.* |
| **1** | No edge | *Generic SaaS — Notion clone, ChatGPT wrapper, "Stripe for X" without X expertise.* |

Before scoring, the orchestrator does live web research: competitors, recent funding, pricing pages, comparable businesses' actual revenue numbers. **Every score must cite at least 2 of those findings.** If something can't be found, the report says `[no data found]` rather than inventing.

The verdict isn't a vibe. It's evidence-bound.

---

## Output

Each run writes a dated report to your project:

```
<your-project>/
└── .wealthprotocol/
    └── reports/
        └── 2026-05-25/
            ├── 00-brief.md          # project brief you confirmed
            ├── 00b-research.md      # competitor + market findings
            ├── 01-edge.md           # Edge Test
            ├── 02-leverage.md       # Leverage Profile
            ├── 03-productization.md # 3AM Test
            ├── 04-equity.md         # Equity Test
            └── 05-verdict.md        # KEEP / PIVOT / KILL + 14-day plan
```

`.wealthprotocol/` is meant to be gitignored — these are your private notes.

---

## When to use it

- You've been building something for 3+ months and you're not sure if it's working
- You're deciding whether to start a new project — run it on the idea before writing code
- You want a quarterly check-in: re-run the protocol and diff the verdicts
- You feel busy but unsure if the work is leveraged. Lens 2 will tell you

## When not to use it

- For pure engineering questions ("is my architecture good"). Use `/code-review` or `/security-review`
- If you want validation. This plugin is built to be honest, not encouraging
- For employer projects you don't own — the lenses assume you're the equity holder

---

## Modes

The audit adapts depending on where your project is:

| Mode | When | What changes |
|---|---|---|
| **idea** | No code yet — just a concept | Skips code reading, lens depth shifts to "would the proposed shape work?" |
| **prerevenue** | Code exists, $0 paying revenue | Lens 4 distinguishes `active` (10+ hr/wk committed) from `dormant` (drifting) |
| **live** | At least $1 in paying customer revenue | Full audit with revenue projections grounded in comparable growth curves |

---

## Philosophy

The framework draws on Naval Ravikant's public writing on wealth — the four leverage types (labor, capital, code, media), specific knowledge, productize-yourself, and the equity-vs-time-rent distinction. None of that is novel. The value here is **operationalizing it as a repeatable project triage**, with real research, evidence requirements, and a single committed verdict.

Sunk cost is not respected. If KILL is the right call, the plugin will say KILL.

---

## License

MIT — see [LICENSE](./LICENSE).

## Author

[Connor Williamson](https://github.com/Connorbw)

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).
