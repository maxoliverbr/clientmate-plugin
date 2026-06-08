---
name: cmposer
description: "Detect early customers and design partners that will burn you: tire-kickers with no real pain, champions with no budget authority, roadmap hijackers, free-pilot-forever logos, vanity names that never convert, and counterparties who squeeze or ghost early-stage vendors. Usage: /cmposer <Account Name>. Runs 8 evidence-based checks, scores a Fit Score (0–100), and recommends whether to pursue. Saves to cmposer-<account>.md."
license: MIT
compatibility: Requires Claude Code with WebSearch and WebFetch. Internet connection required.
allowed-tools: WebSearch WebFetch Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "3 — run before /cmmatch to screen out bad-fit accounts"
---

# /cmposer — Bad-Fit Account Detector

Run a structured 8-check screen against a candidate design partner or early customer to determine whether the relationship will advance the startup or quietly bleed it. Produces a **Fit Score** and a verdict before a founder pours weeks of meetings, custom work, and roadmap concessions into an account that was never going to buy — or worse, one that will distort the product for everyone else.

The wrong early customer is a slow-motion disaster: the pilot that never defines "yes," the champion who can't sign, the whale whose one-off demands become your backlog, the famous logo that proves nothing because no one there actually uses the product. This screens for all of it.

## Invocation

```
/cmposer <Account Name>
```

Examples: `/cmposer "Acme Utilities"` or `/cmposer Stripe`

## Execution Steps

### Step 1 — Load Startup Context

Read `STARTUP_PROFILE.md` (and `cmstrat.md` if present). Extract and hold in context:

- The beachhead segment and Ideal Design Partner Profile
- The specific problem and the pain it relieves
- The buyer role, likely champion, and price point
- Runway / how long a sales cycle the startup can survive
- Whether the startup is selling a paid pilot, a design-partner agreement, or a contract
- Reference-value needs (which logos matter for the next wave)

This context calibrates the checks. A 9-month procurement cycle is fatal for a startup with 8 months of runway but fine for one that's well-funded. A vanity logo is worthless to a startup that needs revenue but valuable to one that needs signal for a raise. Flag relative risk, not just absolute signals.

If `STARTUP_PROFILE.md` does not exist, stop and tell the user to create it first.

Derive the account slug and output filename: lowercase, strip spaces and punctuation.
- `Stripe` → `cmposer-stripe.md`
- `Acme Utilities` → `cmposer-acme-utilities.md`

### Step 2 — Gather Raw Intel

Use WebSearch and WebFetch across exactly these 6 angles. Run all 6 before scoring.

1. `"<Account>" "<problem area>" initiative priority strategy 2025 2026` — is the pain real and active?
2. `"<Account>" budget spend procurement "<category>"` — budget reality and how they buy
3. `"<Account>" pilot vendor startup partnership case study` — do they actually adopt/convert, or pilot-and-stall?
4. `"<Account>" "<buyer role>" leadership champion LinkedIn` — who decides and who could champion
5. `"<Account>" vendor relationship payment terms lawsuit dispute layoffs` — counterparty risk and stability
6. `site:<account-website> OR news "<Account>" "<problem area>"` — confirm acuity and timing

Pull named people, budget signals, dates, and adoption history wherever possible.

**If fewer than 3 of the 6 angles return usable data** (account is small, private, or opaque): note this explicitly in the report header and default the verdict to **Caution**. Do not score what you cannot evidence — but also note that thin public data is itself a mild reachability signal.

### Step 3 — Run the 8 Fit Checks

Run each check in sequence. For each, produce:
- **Signal:** 🟢 Green / 🟡 Yellow / 🔴 Red
- **Finding:** 1–2 sentences with specifics — names, dates, budget/initiative evidence
- **Evidence:** the source (URL, quote, or named publication)

---

#### Check 1: Pain Acuity (20 pts)
**What it tests:** Is the problem you solve a top-priority, actively-funded pain for them — or a nice-to-have they'll nod at and never prioritize? Low pain is the #1 cause of stalled early deals.

- 🟢 Evidence the problem is a current, named priority (public initiative, hiring, exec statement, regulatory pressure)
- 🟡 Plausible pain but no active signal — they have the problem but may not be prioritizing it
- 🔴 No evidence of acute pain, or the problem is clearly peripheral to their actual priorities

**Points:** 🟢 = 20 · 🟡 = 10 · 🔴 = 0

---

#### Check 2: Budget & Authority (20 pts)
**What it tests:** Is there a real budget line, and a champion senior enough to commit it? "We love it, let me check with..." forever is the sound of no authority.

- 🟢 Identifiable budget for this category and a reachable champion with signing authority
- 🟡 Budget exists somewhere but authority is unclear, or the likely champion needs sign-off you can't see
- 🔴 No evidence of budget, or the only contact is too junior to commit — high risk of an endless cycle

**Points:** 🟢 = 20 · 🟡 = 10 · 🔴 = 0

---

#### Check 3: Decision Velocity (10 pts)
**What it tests:** Can they decide and contract inside a timeframe the startup's runway survives? Enterprise procurement and legal can outlast a seed round.

- 🟢 Evidence of fast vendor adoption or a lightweight buying process — they can move in weeks
- 🟡 Moderate process — quarters, not weeks; survivable but plan for it
- 🔴 Heavyweight procurement/legal/security review likely to exceed the startup's runway — a velocity trap

**Points:** 🟢 = 10 · 🟡 = 5 · 🔴 = 0

---

#### Check 4: Roadmap Alignment (15 pts)
**What it tests:** Does what this account needs match where the product is going — or will they pull you into one-off custom work that serves no one else? The roadmap hijacker builds you a product for a market of one.

- 🟢 Their needs map onto the planned roadmap and would benefit the broader ICP
- 🟡 Mostly aligned with some bespoke asks — manageable if scoped and time-boxed
- 🔴 Their core need requires custom work off the roadmap — a distraction that distorts the product

**Points:** 🟢 = 15 · 🟡 = 8 · 🔴 = 0

---

#### Check 5: Conversion Intent (15 pts)
**What it tests:** Will a pilot actually become paid? Look for a culture of buying tools vs. endless free evaluations. Pilot-to-paid history is the best predictor.

- 🟢 Evidence they convert pilots to paid contracts and pay vendors fairly
- 🟡 Mixed or unknown — they pilot, but conversion history is unclear
- 🔴 Pattern of perpetual free pilots, "innovation theater," or extracting vendor work without buying — a free-forever trap

**Points:** 🟢 = 15 · 🟡 = 8 · 🔴 = 0

---

#### Check 6: Reference Value (10 pts)
**What it tests:** If you win them, does it move the next ten buyers? A logo only has value if it converts to a usable reference, quote, or intro — not just a badge.

- 🟢 Respected logo in the beachhead **and** plausibly willing to be a real, usable reference
- 🟡 Decent reference value but uncertain whether they'd go public, or limited reach in your segment
- 🔴 Vanity logo — impressive name but off-segment, or known never to provide references — proves nothing

**Points:** 🟢 = 10 · 🟡 = 5 · 🔴 = 0

---

#### Check 7: Engagement Capacity (5 pts)
**What it tests:** For a design partner specifically — will they actually give time, candid feedback, and data access? A design partner who signs and goes dark gives you a logo and no learning.

- 🟢 Evidence of an engaged, hands-on team with capacity to co-build (innovation team, prior partnerships)
- 🟡 Willing but stretched — engagement may be inconsistent
- 🔴 No capacity or culture for hands-on partnership — likely to sign and disappear

**Points:** 🟢 = 5 · 🟡 = 3 · 🔴 = 0

---

#### Check 8: Counterparty Health (5 pts)
**What it tests:** Are they a fair, stable counterparty? Search for a history of squeezing small vendors, abusive procurement, payment disputes, instability, or layoffs that could kill the deal mid-flight.

- 🟢 Stable, fair reputation with vendors; no red flags
- 🟡 Thin or mixed signal — nothing damning, but unverified
- 🔴 Documented pattern of squeezing/ghosting vendors, payment disputes, or instability threatening the deal

**Points:** 🟢 = 5 · 🟡 = 3 · 🔴 = 0

---

### Step 4 — Score and Verdict

Sum the points across all 8 checks.

**Fit Score: XX/100** *(higher = better fit, lower bad-fit risk)*

Show the per-check breakdown in a table:

| Check | Signal | Points Earned / Max |
|-------|--------|---------------------|
| 1. Pain Acuity | 🟢/🟡/🔴 | X / 20 |
| 2. Budget & Authority | 🟢/🟡/🔴 | X / 20 |
| 3. Decision Velocity | 🟢/🟡/🔴 | X / 10 |
| 4. Roadmap Alignment | 🟢/🟡/🔴 | X / 15 |
| 5. Conversion Intent | 🟢/🟡/🔴 | X / 15 |
| 6. Reference Value | 🟢/🟡/🔴 | X / 10 |
| 7. Engagement Capacity | 🟢/🟡/🔴 | X / 5 |
| 8. Counterparty Health | 🟢/🟡/🔴 | X / 5 |
| **Total** | | **XX / 100** |

**Verdict:**

| Score | Verdict | What it means |
|-------|---------|---------------|
| 80–100 | **Strong Fit** | Real pain, real budget, real reference value — pursue now |
| 60–79 | **Workable** | Yellow flags present; pursue if a champion path exists, mitigate the gaps |
| 40–59 | **Caution** | Material bad-fit signals; only pursue with a warm path and eyes open |
| 0–39 | **Walk Away** | The relationship will cost more than it returns — redirect the energy |

### Step 5 — Save and Report

Write the full check report to `cmposer-<account>.md`.

Then tell the user:
- **Strong Fit (80–100):** "This account is worth real investment. Run `/cmmatch <account>` to map the deal and the champion."
- **Workable (60–79):** "Pursue, but mitigate the flagged gaps first. Run `/cmmatch <account>` to plan around them."
- **Caution (40–59):** "Only pursue with a warm path and a time-boxed pilot with a written success definition. Otherwise redirect."
- **Walk Away (0–39):** "Skip it — the flags (e.g., [top red flag]) will burn runway. Run `/cmlist` for better-fit accounts."

---

## Output Format

When producing the output file, read the exact template from [references/output-format.md](references/output-format.md).

---

## Output Rules

- Every check must cite named evidence — URLs, dates, named people, budget/initiative signals. If absent, say what was searched and why it came up empty.
- Show the per-check score table before the check details.
- If an account has <3 angles with usable data, print this warning at the top: `⚠️ Limited public data — fewer than 3 checks could be fully evidenced. Verdict defaulted to Caution regardless of score.`
- The Fit Score measures bad-fit *risk* — it is not a measure of how much you want them. A dream logo can be a Walk Away.
- Total word budget for check details: ≤700 words. The score table and verdict rationale are not counted.
- Do not recommend `/cmmatch` until the verdict is Workable or Strong Fit.
- Name the single biggest red flag explicitly in the Walk Away / Caution recommendation.
