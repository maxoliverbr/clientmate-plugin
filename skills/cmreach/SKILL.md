---
name: cmreach
description: "Draft design-partner / early-customer outreach from a cmmatch report. Usage: /cmreach <cmmatch-report.md>. Reads STARTUP_PROFILE.md and the cmmatch report, then produces three outreach variants aimed at the champion: a cold email, a warm intro request, and a LinkedIn DM — each with a low-friction first ask (a discovery call, not a contract). Saves to cmreach-<account>.md."
license: MIT
allowed-tools: Read Write
metadata:
  author: 3Flux
  version: "1.0"
  workflow-step: "6 — run after /cmmatch to draft outreach to the champion"
---

# /cmreach — Buyer Outreach Drafter

Turn a cmmatch report into ready-to-send outreach to the champion. Three variants, each built around the account's acute pain — never a generic "we'd love to show you a demo."

## Invocation

```
/cmreach <cmmatch-report.md>
```

Example: `/cmreach cmmatch-acme-utilities.md`

## Execution Steps

### Step 1 — Load Context

Read two files:

1. `STARTUP_PROFILE.md` — extract: company name, one-liner, founder names, the proof point most relevant to this account, website, and any warm-path contact.
2. The cmmatch report passed as argument — extract:
   - Account name and the named champion (or target role)
   - The acute pain (from "The Pain — Evidenced" and "Account Snapshot")
   - Fit score and Recommended Action (Pursue / Nurture / Pass)
   - The pain framing / hook that lands with this champion ("The Path In → Lead with")
   - The low-friction first ask
   - Any warm path from the Champion Map

Derive account slug and output filename: `cmmatch-acme-utilities.md` → account = `acme-utilities`, output = `cmreach-acme-utilities.md`.

If the Recommended Action is **Pass**, stop and tell the user: "The cmmatch recommends Pass for this account. Outreach isn't advised — run `/cmmatch` on a better-fit account first."

If the Recommended Action is **Nurture**, add a top note: "⚠️ cmmatch says Nurture — the gap is [dimension]. This outreach should open a relationship, not push for a pilot yet."

If either file is missing, stop and tell the user which one to provide.

### Step 2 — Draft Three Variants

Every variant must open with the account's acute pain (from cmmatch) — specific to *them*, sourced from a real signal (an initiative, a hire, a public statement). The first ask is always low-friction: a short conversation, not a contract or a long demo.

---

#### Variant A — Cold Email (to the champion)

Rules:
- Subject line: ≤8 words, references *their* problem or initiative — not the startup's name
- Body: 4 sentences maximum
  1. Pain hook — name their specific, sourced problem (shows you did the homework)
  2. One sentence on how you address exactly that, with the single most credible proof point
  3. Why a design partner / early customer like them, now (make it feel selective, not mass-blasted)
  4. Low-friction ask: a 20-minute call to see if it's even relevant — with a concrete hook
- Sign-off: founder name, title, company, website

Format:
```
Subject: [subject line]

[Body — 4 sentences]

[Founder Name]
[Title], [Company]
[Website]
```

---

#### Variant B — Warm Intro Request

A note FROM the founder TO a warm contact, asking them to intro to the champion. The contact should be able to forward the second paragraph.

Rules:
- First paragraph (to the contact): 2 sentences — the ask and why this account specifically
- Second paragraph (forwardable): 3–4 sentences — the pain hook, the proof point, the low-friction ask
- Close: thank them, offer context

Format:
```
[Contact first name],

[Ask for the intro — 2 sentences]

Here's a note you can forward:

---
[Champion first name],

[Forwardable note — 3–4 sentences using the cmmatch pain hook + low-friction ask]

[Founder Name]
[Title], [Company]
[Website]
---

Thanks [Contact first name] — happy to send more if useful.

[Founder Name]
```

---

#### Variant C — LinkedIn DM (to the champion)

3 sentences maximum. No attachment.

Rules:
- Sentence 1: their-pain hook — reference their initiative, post, or role
- Sentence 2: one line on what you do and the strongest proof point
- Sentence 3: low-friction ask — "worth a quick call to see if it's relevant?"

Format:
```
[Body — 3 sentences]
```

---

### Step 3 — Save and Report

Write all three variants to `cmreach-<account>.md`.

Then tell the user:
- "Use **Variant B** if any warm path exists — a referral into an account converts far better than cold."
- "Use **Variant A** when you have the champion's email and no warm path."
- "Use **Variant C** if the champion is active on LinkedIn."
- "Run `/cmprep cmmatch-<account>.md` before the call so you can qualify them fast — and disqualify them if the bad-fit flags show up."

---

## Output Rules

- The pain hook must come from the cmmatch report and reference a *sourced, specific* signal — not a generic problem statement
- Every variant must name the champion specifically — never "Dear Sir/Madam" or "Hi there"
- The first ask is always low-friction (a short call) — never a contract, pricing, or a 60-minute demo
- The cold email body is 4 sentences maximum; the LinkedIn DM is 3 — non-negotiable
- Tone: peer-to-peer, you-did-your-homework, selective. Not a mass blast, not desperate.
- If fit score is below 60, add a top warning: "⚠️ Fit score is [X]/100 — use outreach to qualify, and be ready to walk if the bad-fit flags confirm."
