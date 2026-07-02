---
name: ai-demo-collaboration
description: Business analysis workflow for building demos in direct collaboration with AI. Use this skill when a business analyst works hands-on with an AI assistant (like Claude) to turn a business idea into a working demo for end users — without waiting for a full development team. Covers demo goal definition, persona and user-journey scoping, writing an AI-buildable demo spec, the rapid build-review-refine loop with AI, demo-day preparation, feedback capture, and converting a validated demo into production requirements. Triggers on "build a demo", "prototype with AI", "vibe coding", "POC", "proof of concept", "mockup", "AI-assisted prototyping", or when an analyst wants to co-create something tangible with AI for stakeholders or end users.
---

# AI-Collaborative Demo Building Skill (for Business Analysts)

A workflow for business analysts who collaborate directly with AI to build specific demos for end users — turning requirements into something clickable in hours instead of waiting weeks for a dev team.

## Overview

Six stages from idea to validated demo and production handoff:

1. **Frame the Demo** — One question the demo must answer
2. **Scope Personas & Journey** — Who clicks through it, and what story it tells
3. **Write the AI-Buildable Spec** — A spec the AI can build from in one or few passes
4. **Build Loop with AI** — Rapid build → review → refine cycles
5. **Demo Day & Feedback Capture** — Run the demo, harvest structured feedback
6. **Demo → Production Bridge** — Convert validated learning into real requirements

**Mindset shift**: In this workflow the BA is the product owner, tester, and demo operator; the AI is the builder. Your job is precision of intent, not code. The demo is a *learning instrument*, not a product — optimize for the question it answers, not for completeness.

---

## Stage 1: Frame the Demo

Every demo exists to answer exactly one primary question. Write it down first.

**Demo Charter (one page, always):**

| Field | Example |
|---|---|
| Primary question | "Will elderly users understand their health report without staff help?" |
| Audience | Who watches/uses the demo (end users? executives? city officials?) |
| Decision it informs | Fund phase 2? Choose design A vs. B? Validate a workflow? |
| Success signal | What reaction/measurement means "validated"? |
| Scope: in | The 1–3 flows shown live |
| Scope: out (say it loud) | Auth, admin, edge cases, real integrations, performance |
| Data strategy | Realistic fake data (see Stage 3) — never real customer/patient data |
| Shelf life | Throwaway after decision / evolves into pilot |

**Anti-patterns to reject at this stage:**
- "Demo everything" → split into multiple demos, each with one question
- "Make it production-ready" → that's a different workflow with different cost
- No named audience → no demo; a demo without a viewer is a hobby

---

## Stage 2: Scope Personas & Journey

### 2.1 Persona Cards (lightweight)

For each demo persona: name, role, goal in one sentence, pain point the demo addresses, and their "aha moment" — the exact screen/second the demo wins them over. Design backwards from the aha moment.

### 2.2 The Demo Script (golden path)

Write the demo as a narrated script BEFORE building:

```
Scene 1 (0:00–0:30) — Maria, 74, opens the app from an SMS link.
   Screen: welcome page, huge text, one button "Start my check-up".
Scene 2 (0:30–2:00) — She completes a 3-question memory exercise.
   Screen: one question at a time, voice guidance on.
Scene 3 (2:00–2:30) — Her result appears in plain language with a green badge.
   ★ AHA: "Your memory is doing well. Your next check is in March."
Scene 4 (2:30–3:00) — Cut to city dashboard: her result appears in the triage queue.
   ★ AHA for officials: results flow to services automatically.
```

Rules: total ≤ 5 minutes of golden path; each scene names the screen state and who is watching; mark every aha moment. The script IS the acceptance test for the demo.

---

## Stage 3: Write the AI-Buildable Spec

The quality of what AI builds is bounded by the quality of this spec. Structure it so the AI can execute without guessing on things that matter, and free to decide things that don't.

### 3.1 Spec Template

```markdown
# Demo Spec: [name]

## Context (2-3 sentences)
What this demos and to whom. Link/paste the Demo Charter.

## Tech Constraints
- Form factor: single-file HTML / React app / notebook / slide-linked prototype
- Runs: locally in browser, no backend (or: mock API with static JSON)
- Must work on: [projector 16:9 / iPad / phone] — state the demo device!

## Screens & Flow
For each scene in the demo script: screen name, elements, exact copy
for headlines and buttons (write the real words — AI-invented copy
dilutes your message), what clicking each element does.

## Sample Data
Provide it explicitly: 5-10 realistic records (names, values, dates)
that make the story land. Realistic ≠ real: never paste actual
customer/patient/financial records into the spec.

## Design Intent
Adjectives + references: "calm, high-contrast, elderly-friendly,
minimum font 20px" beats a full design system for a demo.

## Freedom Zones
Explicitly list what the AI may decide: layout details, animations,
component structure. This prevents both over-specification and
unwanted surprises.

## Non-Goals
No login, no persistence, no real API, ... (repeat from charter)
```

### 3.2 Data Realism Rules

- Use domain-correct values (a MoCA-style score of 26/30, a token vesting cliff of 12 months) — stakeholders spot fake-feeling data instantly and lose trust
- Include one imperfect record (a warning state, an edge case) — all-green demos feel staged
- Never real personal data; never production credentials; scrub anything you paste from real systems

---

## Stage 4: Build Loop with AI

### 4.1 The Loop

```
┌────────────┐    ┌────────────┐    ┌──────────────┐    ┌────────────┐
│ 1. Prompt  │───▶│ 2. AI      │───▶│ 3. BA reviews│───▶│ 4. Refine  │
│ with spec  │    │ builds     │    │ AS the user  │    │ or accept  │
└────────────┘    └────────────┘    └──────┬───────┘    └─────┬──────┘
       ▲                                   │ walkthrough        │
       └───────────────────────────────────┴────────────────────┘
              typically 3-6 cycles to demo-ready
```

### 4.2 Collaboration Rules for the BA

1. **First prompt = whole spec** — paste the full Stage 3 spec; don't drip-feed screens.
2. **Review by walking the demo script** — play each persona, out loud if possible. Log deviations from the script, don't fix style you didn't specify (that was a freedom zone).
3. **Batch feedback per cycle** — one message with a numbered change list beats ten micro-corrections; keep each item concrete: *"Scene 3: result text must read exactly 'Your memory is doing well' — currently shows a percentage."*
4. **Pin what's approved** — tell the AI "Scenes 1–2 are approved, don't change them" to prevent regression churn.
5. **Timebox aggressively** — if a feature resists 2–3 refine cycles, cut it or fake it (a static image behind a click is a legitimate demo technique).
6. **Version the checkpoints** — save/commit each demo-ready state before requesting risky changes, so you can always demo *something*.
7. **You own correctness of domain content** — AI will happily invent plausible-but-wrong domain details (fees, scores, regulation names). Verify every domain fact shown on screen.

### 4.3 Definition of Demo-Ready

- [ ] Golden-path script runs start-to-finish with zero errors
- [ ] All copy matches the spec word-for-word on aha screens
- [ ] Sample data is domain-correct and includes the planned imperfect record
- [ ] Works on the actual demo device/screen (test the projector aspect ratio!)
- [ ] Reset mechanism exists (one action returns demo to Scene 1)
- [ ] A fallback exists: screen recording of the golden path, captured while it works

---

## Stage 5: Demo Day & Feedback Capture

### 5.1 Running the Demo

- Open with the primary question ("Today we're testing whether…") — it focuses feedback
- Narrate personas, not features: "Maria receives an SMS…" not "This button triggers…"
- Let end users drive when the question is usability; you drive when the question is concept buy-in
- When something breaks: switch to the recording, note it, keep the story going

### 5.2 Structured Feedback Capture

Capture during/immediately after, in three buckets:

| Bucket | Question | Fate |
|---|---|---|
| Validates | What confirmed the hypothesis? | Evidence for the decision |
| Challenges | What confused/blocked/was disbelieved? | Must address before decision or in next iteration |
| Expands | "Could it also…" ideas | Backlog candidates — do NOT stuff into this demo |

Also record: who said it (persona/stakeholder weight differs), verbatim quotes for the aha screens, and the answer to the primary question (validated / refuted / inconclusive → new demo needed).

---

## Stage 6: Demo → Production Bridge

A validated demo is evidence, not a codebase. Produce the bridge artifacts:

1. **Decision memo** (1 page): primary question, answer, evidence (quotes, observations), recommendation
2. **Validated requirements extraction**: every demo element that earned its place becomes a real requirement with acceptance criteria; everything faked (mock data, fake integration, skipped auth) becomes an explicitly listed gap
3. **Demo-vs-production gap table**:

| Demo shortcut | Production requirement | Owner |
|---|---|---|
| Static JSON results | Scoring service integration (FR-xxx) | Dev team |
| No auth | eID login + consent flow | Dev + DPO |
| One language | i18n per city requirements | Dev team |

4. **Disposition ruling**: state explicitly whether code is throwaway (default) or eligible as a starting skeleton — and get engineering to make that call, not the BA
5. **Feed the domain skill**: requirements flow into the relevant domain workflow (e.g., the `fintech-token-ecosystem` or `medtech-cognitive-health` FS process) — the demo learnings become inputs to Stage 1 of those skills

---

## Best Practices

1. **One demo, one question** — the discipline everything else hangs on.
2. **Write copy yourself** — button labels and result texts carry your business message; never delegate the words on aha screens.
3. **Spec the story, free the pixels** — over-specifying visuals wastes cycles; under-specifying content creates wrong demos.
4. **Demos decay in days** — run them while the context is hot; don't polish for two weeks.
5. **Honesty banner** — label the demo as a prototype to stakeholders; demos that pass as finished products create delivery-expectation debt.
6. **Keep a demo journal** — prompts and specs that worked are reusable assets; your spec library is your velocity.

## When to Use This Skill

✅ Building stakeholder/end-user demos with AI, POCs to de-risk a decision, usability mockups for concept testing, converting a validated demo into production requirements.

❌ Not for: production system development (use engineering workflows + domain FS skills), demos requiring real production data or live integrations with regulated systems, load/performance validation.
