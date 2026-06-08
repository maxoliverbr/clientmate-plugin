---
name: cmmatch
description: "Match the active startup against a single candidate account as a design partner or early customer. Usage: /cmmatch <Account Name>. Reads STARTUP_PROFILE.md, researches the account, and produces a structured Account Fit Report with 7-dimension fit scoring summing to /100, the champion map, the deal shape to propose, the path in, and a clear Pursue / Nurture / Pass recommendation. Saves to cmmatch-<account>.md."
license: MIT
compatibility: Requires Claude Code with WebSearch and WebFetch. Internet connection required.
allowed-tools: WebSearch WebFetch Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "4 — run after /cmposer scores 60+"
---

# /cmmatch — Account Fit Analysis

Match the active startup against a single account to answer: is this a design partner or early customer worth pursuing, who is the champion, and what deal should you propose? Produces a structured report with a 7-dimension fit score summing to /100, a champion map, the deal shape, and the path in.

## Invocation

```
/cmmatch <Account Name>
```

Example: `/cmmatch "Acme Utilities"` or `/cmmatch Stripe`

## Execution Steps

### Step 1 — Load Startup Context

Read `STARTUP_PROFILE.md` (and `cmstrat.md` if present). Extract and hold in context:

- Company name and one-liner
- The problem, the solution, and the precise pain relieved
- Beachhead segment and Ideal Design Partner Profile
- Buyer role, likely champion, price point, business model
- Whether you're proposing a design-partner agreement, paid pilot, or contract
- Runway / survivable sales-cycle length
- Reference-value needs
- Any warm path / named contacts

Derive the account slug: lowercase, strip punctuation and spaces.

If `STARTUP_PROFILE.md` does not exist, stop and tell the user: "Create `STARTUP_PROFILE.md` first — all /cmmatch research is personalized to your startup."

### Step 2 — Bad-Fit Pre-Check

Before researching, check for `cmposer-<account-slug>.md` in the current directory.

- **Score < 40:** Stop. Tell the user: "This account scored [N]/100 on `/cmposer` — a likely bad fit. Review the evidence or move to the next account."
- **Score 40–59:** Continue, but flag for a warning banner in the final report.
- **Score 60+ or file not found:** Proceed normally.

### Step 3 — Research the Account

Use WebSearch and WebFetch across these angles. Pull named people, initiatives, budget signals, and tech stack.

1. `"<Account>" "<problem area>" initiative priority 2025 2026`
2. `"<Account>" "<buyer role>" OR "head of <function>" leadership team`
3. `"<Account>" technology stack vendors partnerships pilots`
4. `"<Account>" budget spending procurement "<category>"`
5. `"<Account>" news strategy earnings priorities`
6. `site:linkedin.com "<Account>" "<buyer role>"` — identify the human champion (do not include names in image queries; text search is fine)

### Step 4 — Score the 7 Fit Dimensions

Score each on the evidence. Every score must cite specifics — no uncalibrated guesses.

| Dimension | Max Points | What it measures |
|-----------|-----------|------------------|
| Pain–Solution Fit | 25 | Does the product hit *their* acute pain precisely — not a generic version of it? |
| Buyability | 20 | Real budget + decision authority + a sales cycle the runway survives |
| Reference & Strategic Value | 15 | What landing them does beyond revenue (signal, segment proof, intros) |
| Champion Strength | 15 | Is there an identifiable, motivated, empowered internal champion? |
| Roadmap Fit | 10 | Their needs align with where the product is going (no one-off hijack) |
| Data / Domain Access | 10 | What they give beyond money — data, feedback, co-development (design-partner value) |
| Reachability | 5 | Warm path or an accessible champion vs. cold and walled |

**Overall Fit Score:** sum of all 7. Maximum 100.

**Recommended Action thresholds:**
- **75–100 → Pursue:** Strong pain fit, buyable, real value, a champion path. Proceed to `/cmreach`.
- **50–74 → Nurture:** Good fit but a missing champion, budget signal, or proof point. Build the relationship, then return.
- **0–49 → Pass:** Weak pain fit, no buyability, or a bad-fit pattern. Move on.

### Step 5 — Write Output and Report

Read the output template from `references/output-format.md`. Populate all sections.

Write the completed report to `cmmatch-<account-slug>.md`.

The following strings must appear verbatim (downstream skills `cmreach` and `cmprep` parse them by exact match):
- `Recommended Action:` followed by `Pursue`, `Nurture`, or `Pass`
- `Fit Score:` followed by the numeric score

Then tell the user:
- The Fit Score and Recommended Action
- If **Pursue**: "Run `/cmvalue <account>` to map what they give you beyond revenue, then `/cmreach cmmatch-<account>.md` to draft outreach to the champion."
- If **Nurture**: "The gap is [the lowest-scoring dimension]. Build toward it, then re-run `/cmmatch`."
- If **Pass**: "This account won't pay off — [primary reason]. Run `/cmlist` for better-fit accounts."

---

## Output Rules

- Every score must cite specific evidence — not "seems promising"
- The Champion Map must name a real person or a specific role and why they'd champion — never "someone in procurement"
- The Deal Shape must specify the proposed instrument (design-partner agreement / paid pilot / contract), a time-box, and a written success definition with a conversion path — a pilot without a defined "yes" is a trap
- The Verdict table must include a row labeled exactly `Recommended Action`
- If no champion can be identified, cap Champion Strength at 4/15 and flag it as the top risk
- Each prose section should stay under 200 words; use tables and bullets
- Do not fabricate names, budgets, or initiatives — cite sources or mark `Unknown`
- A dream logo with weak pain fit scores low on Pain–Solution Fit regardless of prestige
