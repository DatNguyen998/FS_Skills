# Demo Spec Template & Prompt Patterns

Companion reference for the `ai-demo-collaboration` skill. Copy-paste and fill in.

---

## 1. Demo Charter (fill first)

```markdown
# Demo Charter: [name]

- **Primary question**: 
- **Audience**: 
- **Decision it informs**: 
- **Success signal**: 
- **In scope (max 3 flows)**: 
- **Out of scope (explicit)**: 
- **Data strategy**: realistic fake data — source: [invented / scrubbed sample]
- **Shelf life**: throwaway after [date/decision] | evolves into pilot
- **Demo device**: [laptop + projector 16:9 / iPad / phone]
- **Demo date**: 
```

## 2. AI-Buildable Demo Spec

```markdown
# Demo Spec: [name]  (v1 — [date])

## Context
[2–3 sentences + link to charter]

## Tech Constraints
- Form factor: [single-file HTML / React / notebook]
- Runtime: [browser only, no backend / mock API from static JSON]
- Device target: [exact screen it will be shown on]

## Screens & Flow
### Screen 1: [name] (Demo script Scene 1)
- Elements: [list]
- Exact copy: H1 = "…", primary button = "…"
- Interactions: [element] → [result]

### Screen 2: …

## Sample Data
| field | record 1 | record 2 | … |
|---|---|---|---|
[5–10 realistic records; include 1 imperfect/warning record]

## Design Intent
[3–5 adjectives + hard constraints, e.g. "min font 20px, WCAG AA contrast"]

## Freedom Zones (AI decides)
- [layout details, animation, component structure, …]

## Non-Goals
- [no auth, no persistence, no real API, …]
```

## 3. Prompt Patterns for the Build Loop

**Kickoff prompt:**
```
You are building a demo, not a product. Build exactly what the spec
says; where the spec is silent, check the Freedom Zones — if it's
listed there, decide yourself; otherwise ask before building.
Here is the full spec: [paste spec]
Deliver: [single HTML file / running app] I can open and click through.
```

**Refine prompt (batch feedback):**
```
Scenes 1–2 are APPROVED — do not modify them.
Changes for this cycle:
1. Scene 3: result text must read exactly "…" (currently shows …)
2. Scene 3: replace percentage with green/yellow/red badge
3. Sample data: record 4 should show the warning state
Keep everything else unchanged.
```

**Rescue prompt (when a cycle went sideways):**
```
The last change broke [X]. Revert to the version where [checkpoint
description], then apply ONLY change #2 from my previous list.
```

**Fake-it prompt (timeboxed feature):**
```
Stop implementing the live [chart/integration]. Replace it with a
static, realistic-looking image/state that matches the sample data.
It only needs to survive a 30-second walkthrough.
```

## 4. Demo-Ready Checklist

- [ ] Golden path runs start-to-finish, zero errors
- [ ] Aha-screen copy matches spec word-for-word
- [ ] Data domain-correct; one imperfect record present
- [ ] Tested on the actual demo device/resolution
- [ ] One-action reset to Scene 1
- [ ] Screen recording of golden path saved as fallback
- [ ] "Prototype" labeling visible to stakeholders

## 5. Feedback Capture Sheet

```markdown
# Demo Feedback: [name] — [date]
Primary question: [.]
Answer: VALIDATED / REFUTED / INCONCLUSIVE

## Validates (evidence)
- [who] — "[verbatim quote]" — [screen/scene]

## Challenges (must address)
- [who] — [issue] — [scene] — [severity]

## Expands (backlog candidates — not this demo)
- [idea] — [suggested by]

## Incidents
- [what broke, when, workaround used]
```

## 6. Demo → Production Gap Table

```markdown
| # | Demo shortcut | Production requirement (ID) | Risk if forgotten | Owner |
|---|---|---|---|---|
| 1 | Static JSON data | Real scoring/pricing service | Wrong expectations on latency/accuracy | |
| 2 | No auth/consent | [domain-specific auth] | Compliance blocker | |
| 3 | Single language | i18n scope | Rollout blocker | |
| 4 | Happy path only | Error/exception flows | Support load, safety | |
```

## 7. Reusable Copy Blocks

**Honesty banner (put in demo footer):**
> Prototype for concept validation — data is simulated, no real accounts or records are used.

**Demo opening line:**
> "Today we're testing one question: [primary question]. Everything you'll see is a prototype built to answer it — tell us what rings true and what doesn't."
