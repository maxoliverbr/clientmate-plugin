---
name: cmstrat
description: "Define your ideal design-partner and early-customer strategy before you chase logos. Usage: /cmstrat. Reads STARTUP_PROFILE.md and any cmlist.md or cmmatch-*.md files, then produces an honest go-to-market strategy: a sharp Ideal Design Partner Profile and Ideal Customer Profile, how many to sign and in what sequence, what to ask each for (LOI / paid pilot / design-partner agreement), the anti-patterns to refuse, and this week's next actions. Saves to cmstrat.md."
license: MIT
allowed-tools: Read Write Bash(find:*) Bash(ls:*)
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "1 — run first to define who you should and shouldn't sell to"
---

# /cmstrat — Design-Partner & Beachhead Strategy

The wrong early customers can kill a startup as surely as no customers: the tire-kicker who never buys, the whale who hijacks your roadmap, the free-pilot-forever logo that never converts, the design partner whose problem isn't your beachhead. This skill defines who you *should* pursue — and who to refuse — before you spend a single outreach.

Synthesize everything known about the startup into a design-partner and early-customer strategy: a precise ideal-partner profile, how many and in what order, what to ask for, the anti-patterns, and what to do this week.

## Invocation

```
/cmstrat
```

No argument needed. Reads from the current working directory.

## Execution Steps

### Step 1 — Load All Available Context

Read the following from the current working directory (load all that exist):

1. `STARTUP_PROFILE.md` — **required**. If missing, stop and tell the user to create it first.
2. `cmlist.md` — if exists, use for the account pipeline and tiers
3. `cmmatch-*.md` — load all account fit reports; use for sequencing
4. `cmposer-*.md` — if any exist, extract the Bad-Fit Score and verdict per account

### Step 2 — Produce `cmstrat.md`

Write a 7-section strategy memo. Be specific and disciplined — the goal is a profile sharp enough to *disqualify* most of the market on purpose.

---

## Section 1: The Beachhead

One tight paragraph. Name the single beachhead segment the startup should win first — specific enough that you can list real companies in it. Assess:
- Who has the problem most acutely, has budget, and can decide quickly
- Why this segment first (urgency + reachability + reference value), not a bigger but slower one
- One-sentence verdict: "Win [specific segment] first by landing [N] design partners that look like [profile]; everyone else is a distraction until then."

## Section 2: Ideal Design Partner Profile (IDPP)

A design partner is not just an early customer — they co-build, give deep feedback, and tolerate a rough product in exchange for influence and early value. Define the IDPP precisely:

| Attribute | Ideal | Why |
|-----------|-------|-----|
| **Company type / size** | [specific] | [reason] |
| **Buyer & champion role** | [who signs, who champions internally] | [reason] |
| **Pain acuity** | [how badly they feel the problem — must be top-3 priority] | [reason] |
| **Budget authority** | [can they actually pay, and when] | [reason] |
| **Speed** | [decision velocity you need] | [reason] |
| **Reference value** | [will their logo/quote move the next 10 buyers?] | [reason] |
| **Data / domain access** | [what they give you beyond money] | [reason] |

## Section 3: Ideal Customer Profile (ICP) — the paying version

How the ICP differs from the IDPP once you move from co-building to selling. Name what graduates a design partner into a paying reference, and what you'll stop tolerating (custom one-offs, free forever) once you're selling.

## Section 4: What to Ask Each For

Match the ask to the relationship. Be concrete.

| Stage | The ask | The terms that protect you |
|-------|---------|----------------------------|
| Design partner | [design-partner agreement / paid pilot] | [scope, time-box, success criteria, conversion path, who owns IP] |
| Early customer | [paid pilot → contract] | [price, term, reference rights, no perpetual free] |
| Reference | [logo + quote + intro rights] | [what you give in return] |

State plainly: **never** sign a design partner without a written success definition and a conversion path. A pilot with no defined "yes" is a free-forever trap.

## Section 5: Sequencing & Count

- **How many design partners**: the right number (usually 2–4 — enough signal, not so many you're spread thin). Justify for this startup.
- **In what order**: which segment/account first and why (reference value, speed, or learning).
- **Parallel vs. sequential**: recommend one with rationale.
- If a `cmlist.md` exists, pull Tier 1 accounts here by name.

## Section 6: Anti-Patterns — Who to Refuse

The early customers and design partners to walk away from, even when they say yes. For each, the tell and the cost.

| Anti-pattern | The tell | Why it kills you |
|--------------|----------|------------------|
| Roadmap hijacker | Wants features no one else needs | Builds a product for one company |
| Free-pilot-forever | Endless "evaluation," no budget line | Burns runway, never converts |
| No budget authority | Champion can't sign, "I'll need to check" forever | Long cycle, no close |
| Vanity logo | Big name, tiny/no usage | Looks good, proves nothing |
| Wrong-segment enthusiast | Loves it, but isn't your beachhead | Distorts your ICP and roadmap |

## Section 7: This Week — Next 3 Actions

Concrete and specific.
1. **[Action]**: [exactly what, which account, what to send] — deadline: [day]
2. **[Action]**: [exactly what] — deadline: [day]
3. **[Action]**: [exactly what] — deadline: [day]

---

## Output Rules

- The IDPP must be specific enough to name real candidate companies — if it isn't, sharpen it
- Section 6 (anti-patterns) is mandatory and must be tailored to this startup's actual risk, not generic
- Every ask in Section 4 must include the term that protects the startup (success definition, conversion path, reference rights)
- Account names in Sections 5 must come from `cmlist.md` or `cmmatch-*.md` if those exist — do not invent
- This Week actions must be doable in 7 days with no further research
- After saving, tell the user: "Run `/cmlist` to build your target account list, then `/cmposer <account>` on each Tier 1 before investing in the relationship."
