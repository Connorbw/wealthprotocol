# Project Brief Template

Fill this in once per project you want to audit. The `/wealthprotocol` command will draft this for you from the repo and ask only about fields it can't infer — but if you want to write it yourself first, here's the schema.

```
name:                  [project name]
one_liner:             [what it does in one sentence — no jargon, no "AI-powered"]
stage:                 [idea | prototype | mvp | live-no-revenue | live-with-revenue]

hours_per_week:        [how many hours you actually spend on this each week]
monthly_revenue:       [current MRR or equivalent — $0 is fine, be honest]
revenue_model:         [subscription | one-time | services | ads | none]
revenue_streams:
  - name: [stream name]
    monthly: $[amount]
    type:    [subscription | one-time | retainer | services | ads]
target_monthly_income: [what you want this project to earn monthly]

builder_edge:          [your domain knowledge, history, unfair advantage — what makes you specifically the right person to ship this]
tech_primitives:       [stack: e.g., Cloudflare Workers + D1 + React]
non_obvious_insight:   [the insight this project is built on that most people would miss or dismiss]
distribution:          [existing audience, email list, channel, community you OWN today — not "I plan to build one"]

current_activities:
  - [activity 1 — be specific: "responding to support tickets" not "support"]
  - [activity 2]
  - ...

buyer_journey:
  discovery:   [how does a buyer find this today]
  trial:       [can they try without talking to you]
  purchase:    [self-serve checkout, or sales call]
  onboarding:  [automated, docs, or human handoff]
  first_value: [how quickly does the product deliver value without you]
  renewal:     [renews quietly, or someone has to check in]

irreplaceable_core:    [the thing about this project a competitor cannot strip and resell — if you can't name one, write "none"]
```

## Tips

- **Be honest about hours.** The audit is useless if you understate them.
- **Be honest about revenue.** $0 is a valid answer. Padding the number defeats the point.
- **"Building" is not an activity.** Break it down: "shipping new features," "writing custom code for one customer," "designing UI mockups."
- **Distribution must be owned, not rented.** Email list = owned. Twitter followers = rented (platform can change overnight).
