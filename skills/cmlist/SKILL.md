---
name: cmlist
description: "Build a prioritized target account list of candidate design partners and early customers from the active startup profile. Usage: /cmlist. Reads STARTUP_PROFILE.md, researches the beachhead segment, and produces a tiered list of 15–25 accounts ranked by fit with rationale, the likely champion, and a suggested entry angle. Saves to cmlist.md."
license: MIT
compatibility: Requires Claude Code with WebSearch and WebFetch. Internet connection required.
allowed-tools: WebSearch WebFetch Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "2 — run after /cmstrat to build the target account list"
---

# /cmlist — Target Account List Builder

Research the beachhead segment and produce a ranked pipeline of 15–25 candidate design partners and early customers, tiered by fit with the active startup profile and its Ideal Design Partner Profile.

## Invocation

```
/cmlist
```

No argument needed — reads `STARTUP_PROFILE.md` (and `cmstrat.md` if present) from the current working directory.

## Execution Steps

### Step 1 — Load Context

Read `STARTUP_PROFILE.md` and, if present, `cmstrat.md`. Extract and hold in context:

- The beachhead segment and Ideal Design Partner Profile (from cmstrat if available, else infer from Target Customer)
- The specific buyer role and likely internal champion
- The problem and the pain it relieves — and which companies feel it most acutely
- Business model and price point (determines who can actually buy)
- Geography and any sector constraints
- Reference-value needs (which logos would move the next wave of buyers)
- Existing traction and any named customers/pilots already in the profile

If `STARTUP_PROFILE.md` does not exist, stop and tell the user to create it first.

### Step 2 — Research Candidate Accounts

Use WebSearch (and WebFetch on company sites, news, job posts) to identify accounts that fit. Run searches across multiple angles:

1. Companies in the beachhead with the problem: `"<segment>" companies "<problem keyword>" 2025 2026`
2. Signal of active pain/spend: `"<segment>" hiring OR budget OR initiative "<problem area>"` (job posts and initiatives reveal who's actively solving this now)
3. Reference-grade logos in segment: `leading "<segment>" companies <geography>`
4. Innovation-friendly buyers: `"<segment>" pilot OR design partner OR early adopter "<adjacent tech>"`
5. Champion signal: `"<buyer role>" "<segment>" speaking OR posting "<problem area>"` (find the human, not just the logo)

For each candidate, quickly verify:
- Do they plausibly have the problem *acutely* (not just nominally)?
- Is there budget/decision authority for something like this?
- Is there a reachable champion (named person, role, or warm path)?
- Reference value: would landing them help win the next ten?

### Step 3 — Score and Tier Each Account

Rank accounts across five dimensions:
1. **Pain acuity** — is this problem top-3 for them, or a nice-to-have?
2. **Buyability** — budget + decision authority + a sales cycle you can survive
3. **Reference value** — does their logo/quote move your next wave of buyers?
4. **Reachability** — is there a warm path or an identifiable champion?
5. **Beachhead fit** — are they squarely in your wedge, or an off-segment tempter?

### Step 4 — Produce `cmlist.md`

Write the output to `cmlist.md` using this structure:

---

```markdown
# Target Account List: [Startup Name]
_Generated: [date] | Beachhead: [segment] | Looking for: [N design partners / early customers]_

---

## Tier 1 — Pursue Now (Design-Partner Grade)
*High pain + buyable + strong reference value + a reachable champion. Reach out within 2 weeks.*

### [Account Name]
- **Why**: [2–3 bullets — the acute pain, why now, reference value]
- **Likely champion**: [Name or role] — [why them]
- **Budget / authority signal**: [evidence they can buy]
- **Entry angle**: [warm intro via [name] / champion outreach / event / cold]
- **Run /cmposer first**: Yes / Already done (link if exists)

[Repeat for 6–8 accounts]

---

## Tier 2 — Warm Up First
*Good fit but missing a champion, a budget signal, or a proof point. Build the relationship; pursue after [milestone].*

### [Account Name]
- **Why**: [2–3 bullets]
- **Likely champion**: [Name or role]
- **What to wait for / build**: [the missing piece]

[Repeat for 6–8 accounts]

---

## Tier 3 — Monitor
*Off-beachhead, slow buyer, or weak reference value. Revisit later or skip.*

### [Account Name]
- **Why eventually**: [1–2 bullets]
- **Blocker**: [what would need to change]
- **Revisit when**: [milestone or date]

[Repeat for 3–6 accounts]

---

## Pipeline Summary
- Total accounts identified: [N]
- Tier 1 (pursue now): [N]
- Accounts with a named champion: [N] — *(these are your real pipeline)*
- Warm paths available: [list names and who connects them]
- Reference-grade logos in Tier 1: [list]
- Suggested first outreach order: [Account 1] → [Account 2] → [Account 3]
```

---

### After Producing `cmlist.md` — Bad-Fit Pre-Filter

Once the list is written, tell the user to run `/cmposer <account name>` on every Tier 1 account **before** investing in the relationship:

> "Before running `/cmmatch` on any of these, run `/cmposer <account name>` to screen for the bad-fit patterns that burn early-stage startups — tire-kickers, roadmap hijackers, no-budget champions, free-pilot-forever logos. Accounts scoring below 40 should be dropped. Accounts scoring 40–59 are warm-path-only. Only proceed to `/cmmatch` for accounts scoring 60 or above."

---

## Output Rules

- Every account must include a named champion or a specific role to target — not just the company
- Cite the source of pain/budget signals inline (e.g., "per their Q1 job post for a [role]")
- Reference-value reasoning is required for every Tier 1 account
- Do not include off-beachhead accounts in Tier 1 no matter how exciting — note them in Tier 3 if at all
- Warm paths take priority in the suggested order — always surface them
- Flag if any Tier 1 account already has a `/cmmatch` report saved in the current directory
