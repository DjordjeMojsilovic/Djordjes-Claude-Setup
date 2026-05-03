---
name: decision-toolkit
description: Structured decision-making frameworks for complex, high-stakes, or ambiguous choices. Use when the user needs to make a significant decision and would benefit from a formal framework — business strategy, tech architecture, career moves, startup pivots, build-vs-buy, prioritization. Activate on: "how should I decide", "help me think through", "what framework", "prioritize these", "should we build or buy", "is this worth it". Provides: RICE scoring, decision matrices, pre-mortem analysis, second-order thinking prompts, and synthesis into a clear recommendation.
---

# Decision Toolkit

Structured frameworks for making better decisions. Choose the right tool for the decision type.

## Framework 1 — RICE Prioritization
**Use for:** Feature prioritization, project backlog, competing initiatives.

Score each option:

```
RICE Score = (Reach × Impact × Confidence) / Effort

Reach:     How many people/units affected? (number per time period)
Impact:    Massive=3 / High=2 / Medium=1 / Low=0.5 / Minimal=0.25
Confidence: How sure are you? 100% / 80% / 50%
Effort:    Person-months to complete
```

Present as a ranked table. Note: RICE is a forcing function, not a truth machine — the assumptions matter more than the scores.

---

## Framework 2 — Decision Matrix
**Use for:** Choosing between multiple options across multiple criteria.

Steps:
1. List options (rows)
2. List criteria (columns) — max 6
3. Assign weight to each criterion (total = 100%)
4. Score each option on each criterion (1-5)
5. Calculate weighted score
6. Identify winner — then sanity-check: does the winner feel right? If not, the weights are wrong.

Always state the most contested assumption in the weighting.

---

## Framework 3 — Pre-Mortem
**Use for:** High-stakes decisions before commitment. Forces failure-mode thinking.

Instructions:
"Imagine it's 12 months from now. This decision was made. It failed spectacularly. What happened?"

Generate 5-7 realistic failure scenarios. For each:
- Name the failure mode
- Probability estimate (rough)
- Early warning signal (what would you see in month 1-3?)
- Mitigation: what decision change would reduce this risk?

Then: does the decision still make sense given these failure modes?

---

## Framework 4 — Second-Order Thinking
**Use for:** Decisions with complex ripple effects. Strategy, policy, architecture.

Structure:
```
FIRST-ORDER EFFECTS (immediate, obvious):
[What happens directly as a result of this decision]

SECOND-ORDER EFFECTS (3-12 months):
[What happens because of the first-order effects]

THIRD-ORDER EFFECTS (1-3 years):
[What happens because of the second-order effects]

MOST DANGEROUS ASSUMPTION:
[The one thing that, if wrong, reverses the recommendation]
```

---

## Framework 5 — Build vs Buy vs Partner
**Use for:** Technology or capability acquisition decisions.

Evaluate across:
| Dimension | Build | Buy | Partner |
|-----------|-------|-----|---------|
| Time to value | Slowest | Fastest | Medium |
| Control | Maximum | Minimum | Shared |
| Cost structure | Capex upfront | Opex ongoing | Variable |
| Strategic differentiation | High | Low | Medium |
| Maintenance burden | Full | Vendor's | Shared |

Decision rules:
- If it's core to your differentiation → Build
- If it's commodity infrastructure → Buy
- If you need speed + don't need control → Buy
- If you need capability you can't build in 6 months → Partner or Buy

---

## Framework 6 — Reversibility Test
**Use for:** Any decision. The most underused filter.

Ask:
1. Is this decision reversible? (Can you undo it in <3 months at <20% cost?)
2. If YES → move fast, decide with 70% information, learn by doing
3. If NO → slow down, gather more information, apply pre-mortem

"If in doubt, make it reversible first."

---

## Synthesis Protocol

After applying any framework:
1. **Recommendation**: State the decision clearly. No "it depends" without conditions.
2. **Confidence**: X% — what would raise or lower it?
3. **Key assumption**: The one thing that most determines the outcome.
4. **Decision trigger**: What specific signal in the next 30 days confirms or challenges this?

Source: adapted from glebis/claude-skills/decision-toolkit + standard decision frameworks
