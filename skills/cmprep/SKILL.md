---
name: cmprep
description: "Prepare for a design-partner / early-customer discovery call from the active startup profile and a cmmatch report. Usage: /cmprep <cmmatch-report.md>. Produces complete call prep: a timed agenda, the qualifying questions that confirm pain/budget/authority/timeline, the value story, preemptive answers to their likely objections, the deal shape and ask, and the disqualify triggers that tell you to walk. Saves to cmprep-<account>.md."
license: MIT
allowed-tools: Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "7 — run after /cmmatch when a discovery call is booked"
---

# /cmprep — Discovery Call Prep

Prepare the founders for a discovery call with a candidate design partner or early customer, using the startup profile and a previously generated cmmatch report. The goal of a discovery call is not to sell — it's to *qualify*: confirm the pain is acute, the budget and authority are real, and the account isn't one of the bad-fit patterns. Prep to qualify and to disqualify.

## Invocation

```
/cmprep <cmmatch-report.md>
```

Example: `/cmprep cmmatch-acme-utilities.md`

## Execution Steps

### Step 1 — Load Context

Read two files:

1. `STARTUP_PROFILE.md` — the full profile.
2. The cmmatch report — extract: account name, the acute pain, fit score and Recommended Action, the champion map, the deal shape, the discovery questions, and the Key Risks & Bad-Fit Watch.

If the Recommended Action is **Pass**, stop and tell the user: "cmmatch says Pass — don't spend prep time on an account you shouldn't pursue."

Derive slug: `cmmatch-acme-utilities.md` → output `cmprep-acme-utilities.md`.

If either file is missing, stop and tell the user which one to provide.

### Step 2 — Produce the Prep

Assume a 30-minute call. The founder should leave knowing whether this is a real opportunity, who decides, and what the path to a signed pilot looks like — or that it's a no.

---

## 1. Timed Agenda (30 minutes)

| Time | Segment | Goal |
|------|---------|------|
| 0:00–3:00 | Rapport + frame | Set it as a fit conversation, not a pitch |
| 3:00–13:00 | Discovery (their world) | Confirm pain, current solution, what "fixed" looks like |
| 13:00–20:00 | Your value story | Map your solution to *their* words — brief |
| 20:00–26:00 | Qualify the deal | Budget, authority, timeline, success criteria |
| 26:00–29:00 | Propose next step | The deal shape and a concrete next action |
| 29:00–30:00 | Close + recap | Confirm owner, date, next step |

## 2. The Frame (verbatim)

Two sentences to open: position the call as a mutual fit check, not a sales pitch. This lowers their guard and earns honest answers.

## 3. Discovery Questions — to Qualify

The questions that confirm (or kill) the opportunity. For each, note what a good answer vs. a disqualifying answer sounds like.

- **Pain acuity:** [question] — good: [signal] · bad: [signal]
- **Current solution / status quo:** [question] — good / bad
- **Budget:** [question that surfaces whether there's a real line] — good / bad
- **Authority:** [question that reveals who signs] — good / bad
- **Timeline:** [question on urgency] — good / bad
- **Success definition:** [question: "what would make this a clear win for you?"] — good / bad

## 4. Your Value Story (brief)

Three sentences mapping your solution to *their* language, using the pain from cmmatch. Lead with the outcome, not the features. Name the single proof point most relevant to them.

## 5. Objection Handling

For each likely objection (from cmmatch Key Risks + the categories below), a calm, concrete response.

| Their objection | Your response |
|-----------------|---------------|
| "We could build this ourselves" | [response] |
| "You're too early / too small" | [response — turn it into the design-partner advantage] |
| "Security / data concerns" | [response] |
| "[account-specific risk from cmmatch]" | [response] |

## 6. The Ask & Deal Shape

State exactly what to propose if they qualify (from cmmatch Deal Shape):
- Instrument: [design-partner agreement / paid pilot]
- Time-box and **written success definition** (their "yes")
- Conversion path to paid
- What you ask in return (reference rights, feedback cadence, data access)
- The protective terms (no perpetual free, scoped customization)

The concrete next step to land on the call: [e.g., "send a one-page pilot scope by Friday; 30-min scoping call next week"].

## 7. Disqualify Triggers — When to Walk

The signals that mean this is a bad-fit account, even if the call feels warm. If two or more show up, slow down or pass.

- [No budget line and no path to one]
- [Champion can't name who signs]
- [Wants features off your roadmap as a condition]
- [Wants it free "to evaluate" with no conversion path]
- [Off-beachhead — the pain isn't your wedge]
- [account-specific trigger from cmposer/cmmatch]

---

### After Saving

Save to `cmprep-<account>.md`. Then tell the user, out of prep voice:
- "Spend the first half listening, not pitching. The discovery questions in Section 3 decide whether this is real."
- "If two disqualify triggers fire, it's a no — a polite, fast no protects your runway. That's a win, not a loss."

---

## Output Rules

- Every question and answer must use real facts from the profile and cmmatch — no unfilled placeholders
- The success-definition question (Section 3) and the written success definition (Section 6) are both mandatory — a pilot without a defined "yes" is the trap this whole toolkit exists to prevent
- Section 7 (disqualify triggers) must be tailored to this account's specific bad-fit risks, not generic
- Keep the value story to ≤3 sentences — discovery is about listening
- Tone: curious, consultative, willing to walk — not eager-to-please
