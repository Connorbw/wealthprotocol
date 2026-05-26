# wealthprotocol

A Claude Code plugin that audits any project — an **idea** on the drawing board, a **pre-revenue** codebase you've been sitting on, or a **live business** with paying customers — through Naval Ravikant's wealth lenses and tells you whether to **KEEP, PIVOT, or KILL** it.

Run `/wealthprotocol` in any project directory (or in an empty dir, for an idea-stage audit). The plugin:

1. Reads your repo (or asks for the concept if no code exists)
2. **Does real market research** — finds direct competitors, adjacent threats, comparable business economics, current pricing, audience size
3. Asks you for the things it can't infer (hours, revenue, distribution)
4. Runs four sequential audits with scoring anchored to named real companies — not free-form 1–5 judgment
5. Produces a dated report with a verdict, 14-day plan, and evidence audit

Every score cites at least 2 pieces of real evidence. No reasoning-only verdicts.

It's an honest second opinion you can re-run quarterly.

---

## The Four Lenses

| # | Lens | Question it answers |
|---|---|---|
| 1 | **Edge Test** | Does this project sit at a rare intersection of knowledge only you can ship — or could a funded team replicate it in a quarter? |
| 2 | **Leverage Profile** | Where are your hours actually going? Labor, capital, code, or media? What's your Leverage Index? |
| 3 | **3AM Test** | Does this project sell, ship, and support itself while you're asleep? Where does it break? |
| 4 | **Equity Test** | Is your revenue equity (compounds, outlives your hours) or time-rent (stops when you stop)? |
| 5 | **Verdict** | Synthesis: KEEP, PIVOT, or KILL — plus the next 14 days. |

---

## Install

```
/plugin marketplace add Connorbw/wealthprotocol
/plugin install wealthprotocol@wealthprotocol
```

Then `cd` into any project repo and run:

```
/wealthprotocol
```

The plugin will read the project, draft a brief, ask you to fill in what it can't infer, and walk through the audit.

---

## Output

Each run writes a dated report to your project:

```
<your-project>/
└── .wealthprotocol/
    └── reports/
        └── 2026-05-25/
            ├── 00-brief.md          # the project brief you confirmed
            ├── 00b-research.md      # competitor + market research findings
            ├── 01-edge.md           # Edge Test
            ├── 02-leverage.md       # Leverage Profile
            ├── 03-productization.md # 3AM Test
            ├── 04-equity.md         # Equity Test
            └── 05-verdict.md        # KEEP / PIVOT / KILL + 14-day plan
```

## How the scoring works (and what grounds it)

Every lens uses a 5-tier scoring scale anchored to real companies. Example for the Edge Test:

- **5** — Category-defining edge. *Stripe at founding: Patrick + John Collison + Auctomatic exit, fewer than 50 people on earth had that combination of payment-API frustration and engineering chops.*
- **4** — Strong edge. *Linear: Karri Saarinen brought design-leadership taste from Airbnb/Uber.*
- **3** — Real edge. *Pieter Levels launching Nomad List with deep nomad-lifestyle knowledge + small Twitter audience.*
- **2** — Motivation edge only. *"I had this problem at work, so I built a tool."*
- **1** — No edge. *Generic SaaS, no insight, no audience.*

Before scoring, the orchestrator does live web research: competitors, funding rounds, pricing pages, comparable businesses' actual revenue numbers. Scores must cite at least 2 of those findings. If something can't be found, the report says `[no data found]` rather than inventing.

The point: the verdict isn't a vibe. It's evidence-bound.

`.wealthprotocol/` is meant to be gitignored — these are your private notes.

---

## When to use it

- You've been building something for 3+ months and you're not sure if it's working.
- You're deciding whether to start a new project — run the brief against the idea before writing code.
- You want a quarterly check-in: re-run the protocol and diff the verdicts.
- You feel busy but unsure if the work is leveraged. Lens 2 will tell you.

## When not to use it

- For pure engineering questions ("is my architecture good"). Use `/code-review` or `/security-review`.
- If you want validation. The plugin is built to be honest, not encouraging.
- For employer projects you don't own. The lenses assume you're the equity holder.

---

## Philosophy

The framework draws on Naval Ravikant's public writing on wealth — the four leverage types (labor, capital, code, media), specific knowledge, productize-yourself, and the equity-vs-time-rent distinction. None of that is novel; the value here is **operationalizing it as a repeatable project triage**, with state carried across lenses and a single committed verdict at the end.

Sunk cost is not respected. If KILL is the right call, the plugin will say KILL.

---

## License

MIT.

## Author

[Connor Williamson](https://github.com/Connorbw)
