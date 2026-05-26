# wealthprotocol

A Claude Code plugin that audits any project through Naval Ravikant's wealth lenses and tells you whether to **KEEP, PIVOT, or KILL** it.

Run `/wealthprotocol` in any project directory. The plugin reads your repo, asks a handful of questions it can't infer (hours, revenue, distribution), runs four sequential audits, and produces a dated report with a verdict and a 14-day action plan.

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
            ├── 01-edge.md           # Edge Test
            ├── 02-leverage.md       # Leverage Profile
            ├── 03-productization.md # 3AM Test
            ├── 04-equity.md         # Equity Test
            └── 05-verdict.md        # KEEP / PIVOT / KILL + 14-day plan
```

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
