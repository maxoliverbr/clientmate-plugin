---
name: cmvalue
description: "Audit the full value a design partner or early customer delivers beyond the contract value — reference economics and expansion, but also data access, domain expertise, co-development, distribution, and brand signal — scored by relevance to the active startup and netted against the cost to serve them (support burden, customization, discounts, founder time). Usage: /cmvalue <Account Name>. Saves to cmvalue-<account>.md."
license: MIT
compatibility: Requires Claude Code with WebSearch and WebFetch. Internet connection required.
allowed-tools: WebSearch WebFetch Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "5 — run after /cmmatch to weigh true value against cost-to-serve"
---

# /cmvalue — Design-Partner & Customer Value Audit

Early customers are priced in revenue but paid for in something else entirely. The best design partner might pay little and be worth enormous strategic value; a big-paying account might cost more to serve than it returns. This audits the full picture: **Part A — Commercial Value** (contract, expansion, reference economics) and **Part B — Strategic Value** (data, domain expertise, co-development, distribution, brand signal) — then **nets it against the cost to serve** (support burden, customization, discounts, founder time) for a clear verdict.

Use this after `/cmmatch` to decide how hard to chase an account and what concessions are actually justified.

## Invocation

```
/cmvalue <Account Name>
```

Examples: `/cmvalue "Acme Utilities"` or `/cmvalue Stripe`

## Execution Steps

### Step 1 — Load Startup Context

Read `STARTUP_PROFILE.md` (and `cmstrat.md` if present). Extract and hold in context:

- Stage and what the startup needs most right now (revenue, references, data, distribution, learning)
- Beachhead segment and the reference logos that would move the next wave
- Business model and price point
- Product maturity — how much support/customization an early customer will demand
- Whether the startup needs domain data or co-development to improve the product
- Distribution gaps a customer's channels could fill

If `STARTUP_PROFILE.md` does not exist, stop and tell the user to create it first.

Derive slug and filename: lowercase, strip spaces/punctuation. `Acme Utilities` → `cmvalue-acme-utilities.md`.

### Step 2A — Research Commercial Value

Use WebSearch and WebFetch across these angles:

1. `"<Account>" size revenue employees budget "<category>"`
2. `"<Account>" expansion divisions subsidiaries footprint` (land-and-expand potential)
3. `"<Account>" references case study testimonial vendor` (will they go public?)
4. `"<Account>" "<segment>" influence reputation leader` (does their endorsement carry weight?)

**Collect:** plausible contract value and expansion path, and reference economics — would they be a public, quotable reference whose name moves your beachhead?

### Step 2B — Research Strategic Value

Use WebSearch and WebFetch across these angles:

5. `"<Account>" data scale operations "<domain>"` (what data/scale would they expose you to?)
6. `"<Account>" innovation team co-development partnership startups`
7. `"<Account>" channels distribution partners customers network`
8. `"<Account>" "<buyer role>" thought leadership conference influence`

**Collect:**
- Data & domain access: what their scale/operations would teach your product
- Co-development capacity: do they have a team that will build *with* you
- Distribution: do their channels, network, or platform open doors to other buyers
- Brand signal: what their name does for your fundraising, hiring, and next customers

**Source labeling:** mark each item **[Confirmed]** or **[Reported]**.

**If fewer than 3 angles across both steps return usable data:** state this at the top and list the questions to ask the account directly.

### Step 3 — Score and Net Against Cost-to-Serve

#### Part A — Commercial Value
Estimate + relevance per item. Categories: **Contract Value** (initial + expansion potential) · **Reference Economics** (public reference / quote / intro value to the beachhead).

#### Part B — Strategic Value
Impact rating + assessment per dimension (no dollar value):
1. **Data & Domain Access** — **High / Medium / Low**. What their scale and operations teach the product.
2. **Co-Development Capacity** — **High / Medium / Low**. Will they build with you, or just consume?
3. **Distribution & Network** — **High / Medium / Low**. Do their channels open the next ten buyers?
4. **Brand Signal** — **High / Medium / Low**. What their logo does for your raise, hiring, and pipeline.
5. **Learning Value** — **High / Medium / Low**. How much this specific partner sharpens your ICP and product.

#### Cost-to-Serve — what they take
Quantify honestly: expected support burden (early product = high touch), customization demanded (and whether it's reusable or one-off), discounts/free terms given, integration/security overhead, and founder time. Flag any roadmap-distortion risk.

#### Net Verdict
State whether total value clears cost-to-serve **for this startup at this stage** — Worth Chasing Hard / Worth It / Marginal / Costs More Than It Returns — with one sentence of reasoning, and the maximum concession (discount, customization, free time) that's justified.

### Step 4 — Produce the Value Report

Write `cmvalue-<account>.md` using the template.

---

## Output Format

When producing the output file, read the exact template from [references/output-format.md](references/output-format.md).

---

### Step 5 — Save and Route

Write the full report to `cmvalue-<account>.md`.

Then tell the user:
- "The best design partner is often not the biggest payer — weight data, co-development, and reference value, not just contract size."
- "Check the Net Verdict and the max justified concession before you negotiate. If it's Costs More Than It Returns, walk or re-scope."
- "Run `/cmprep cmmatch-<account>.md` to fold this into your discovery-call value story."

---

## Output Rules

**Commercial value:**
- **[Confirmed]** vs. **[Reported]** labels mandatory for every row
- Contract and expansion estimates use a `~` prefix unless sourced
- Reference economics must reference the startup's *specific* beachhead — does this logo move *those* buyers?

**Strategic value:**
- Every dimension assessed — write "Not documented — ask directly" rather than skipping
- Impact ratings mandatory
- Data & Domain Access and Co-Development must be concrete, not generic

**Net verdict:**
- Cost-to-serve must include an honest founder-time and support-burden estimate, plus roadmap-distortion risk
- The Net Verdict and the maximum justified concession are both mandatory and must reference the startup's stage
- The verdict must hold even against a prestigious logo — prestige is not value to serve

**Top Picks & Questions:**
- Top Picks reference something specific from `STARTUP_PROFILE.md` — ≤150 words
- Questions section includes ≥3 specific items to confirm with the account directly (budget, expansion, reference willingness, data access)
