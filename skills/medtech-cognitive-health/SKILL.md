---
name: medtech-cognitive-health
description: Business analysis for Medtech solutions in functional brain health and elderly care. Use this skill when a business analyst needs to define requirements for health assessment platforms where elderly users take functional/cognitive tests, the system determines their health condition, and a city or municipal health service delivers treatment or care based on the results. Covers assessment workflow design, scoring and risk stratification, clinical/regulatory compliance (SaMD, HIPAA/GDPR, IEC 62304), accessibility for elderly users, HL7 FHIR interoperability, and the care-delivery pathway to municipal services. Triggers on "medtech", "brain health", "cognitive test", "health assessment", "elderly care", "care pathway", "SaMD", or healthcare requirement documentation.
---

# Medtech Cognitive Health & Elderly Care Business Analysis Skill

A structured workflow for business analysts specifying health-assessment platforms: elderly users take functional brain / health tests, the system classifies their condition, and city health services deliver treatment based on the output.

## Overview

Seven stages from clinical intent to implementation-ready specification:

1. **Gather Clinical & Business Context** — Population, outcomes, stakeholders
2. **Map the Care Pathway** — Test → result → triage → city-delivered treatment
3. **Define the Assessment Model** — Tests, scoring, risk stratification
4. **Regulatory & Data Protection Analysis** — SaMD classification, HIPAA/GDPR, consent
5. **Interoperability & Integration Design** — FHIR, city systems, EHR/registries
6. **Write the Functional Specification** — Full FS with clinical safety cases
7. **Pilot & Rollout Roadmap** — Clinical validation, municipal onboarding, scale-up

---

## Stage 1: Gather Clinical & Business Context

**Essential Questions:**
- **Population**: Which elderly cohort? (age range, community-dwelling vs. care facilities, digital literacy, languages)
- **Clinical goal**: Screening (find at-risk people), diagnosis support, or monitoring over time?
- **Conditions in scope**: Cognitive decline/MCI/dementia risk, fall risk, depression, frailty, general functional health?
- **Delivery model**: Self-administered at home, kiosk at community centers, or supervised by a nurse/social worker?
- **The city's role**: Which municipal services act on results? (home care, day centers, GP referrals, physiotherapy, social services)
- **Success metrics**: Earlier detection rate, referral-to-treatment time, reduction in emergency admissions, user completion rate

**Stakeholder Map (document explicitly):**

| Stakeholder | Interest | Key requirement source |
|---|---|---|
| Elderly user | Simple, dignified, low-anxiety testing | Accessibility, UX, consent |
| Family/caregiver | Visibility, alerts | Proxy access, notifications |
| Clinician (GP, geriatrician) | Valid results, actionable reports | Scoring validity, clinical report format |
| City health department | Population dashboards, resource planning | Aggregation, referral routing, SLAs |
| Care providers | Timely, complete referrals | Integration, task management |
| Data protection officer | Lawful processing | Consent, minimization, retention |

---

## Stage 2: Map the Care Pathway

The core artifact: an end-to-end pathway from test to treatment.

```
┌──────────┐   ┌───────────┐   ┌────────────┐   ┌─────────────┐   ┌────────────┐
│ Invite / │──▶│ Assessment│──▶│ Scoring &  │──▶│ Triage &    │──▶│ Treatment  │
│ Enroll   │   │ (tests)   │   │ Risk Strat.│   │ Referral    │   │ Delivery   │
└──────────┘   └───────────┘   └────────────┘   └─────────────┘   └────────────┘
 city outreach   at home/kiosk    algorithm +      rules engine →     city services
 consent, ID     accessibility    clinical review  right service,     execute care
 verification    adaptations      when required    right urgency      plan; outcomes
                                                                      feed back ──┐
       ▲                                                                          │
       └────────────────── re-assessment cycle (monitoring) ◀─────────────────────┘
```

**For each pathway step document:**
- Actors and handoffs (who does what, system vs. human)
- Entry/exit criteria and decision rules
- Timing SLAs (e.g., "high-risk result → clinician review within 24h → city service contact within 5 working days")
- Failure/exception flows: incomplete test, user cannot be reached, capacity shortage at city service, user declines treatment
- **Safety-critical rule**: define the escalation path for results suggesting acute risk (e.g., severe depression indicators → same-day escalation protocol)

---

## Stage 3: Define the Assessment Model

### 3.1 Test Battery Specification

For each functional/cognitive test, document:

| Attribute | Description |
|---|---|
| Test name & clinical basis | e.g., digital adaptation of MoCA-style tasks, reaction-time, memory recall, gait/balance via sensors |
| What it measures | Domain: memory, attention, executive function, processing speed, motor function |
| Validation status | Clinically validated instrument vs. novel (novel → needs validation study) |
| Duration & fatigue budget | Total battery ≤ 20–30 min for elderly users; allow pause/resume |
| Input modality | Touch, voice, camera, wearable sensor — with accessibility alternatives |
| Repeatability | Practice effects, alternate forms for re-testing |

### 3.2 Scoring & Risk Stratification

- **Raw scores → normalized scores**: age/education-adjusted norms (document the normative dataset)
- **Risk bands**: e.g., Green (no action) / Yellow (monitor, re-test in 3 months) / Orange (GP referral) / Red (urgent clinical review)
- **Human-in-the-loop rule**: which bands are auto-routed vs. require clinician confirmation before referral — *make this an explicit signed-off requirement; it drives the regulatory classification (Stage 4)*
- **Explainability**: the report must show which domains drove the score, in clinician language AND in plain language for the user
- **Longitudinal logic**: decline vs. single snapshot; thresholds on rate-of-change

### 3.3 Accessibility Requirements (non-negotiable for elderly users)

- Large fonts, high contrast, WCAG 2.1 AA minimum; adjustable text size
- Voice guidance and multi-language support
- No time pressure except where the test clinically requires it (explain why beforehand)
- Hearing/vision/motor impairment alternative flows
- Caregiver-assisted mode with clear flagging (assistance can invalidate some tests — define rules)
- Simple recovery from mistakes; no data loss on interruption

---

## Stage 4: Regulatory & Data Protection Analysis

### 4.1 SaMD (Software as a Medical Device) Classification

If the software's output informs clinical/care decisions, it is likely SaMD. Document:

| Question | Impact |
|---|---|
| Does output drive treatment decisions? | Yes → medical device; risk class depends on significance |
| EU: MDR class? | Screening/triage software typically Class IIa (Rule 11); higher if it drives urgent decisions |
| US: FDA pathway? | 510(k)/De Novo vs. Clinical Decision Support exemption analysis |
| Development standard | IEC 62304 (software lifecycle), ISO 14971 (risk management), IEC 62366 (usability) |
| Clinical evaluation | Evidence plan: literature route vs. own clinical investigation |

**BA rule**: the intended-use statement is a requirements artifact. Write it precisely — it determines the whole regulatory burden. "Wellness insights" vs. "screening for cognitive impairment" are different products.

### 4.2 Data Protection (GDPR / HIPAA)

- Health data = special category (GDPR Art. 9) — document the lawful basis (explicit consent and/or public-interest health basis for the city)
- **Consent model**: granular (assessment, sharing with city, sharing with family, research reuse), withdrawable, comprehensible to elderly users; capacity/guardianship handling
- **Data minimization**: city receives what it needs to deliver care (risk band + required context), not raw test data by default
- **Roles**: who is controller (city? platform vendor?) and processor — drives contracts (DPA) and requirements
- Retention schedule, pseudonymization for analytics, DPIA required
- If US: HIPAA — covered entity/BA agreements, minimum-necessary rule, audit controls

### 4.3 Clinical Safety

- Hazard log per ISO 14971: false negative (missed deterioration), false positive (anxiety, wasted capacity), delayed escalation, wrong-patient data
- For each hazard: severity, probability, mitigations → these become functional requirements (e.g., "identity check before each assessment session")

---

## Stage 5: Interoperability & Integration Design

### 5.1 Integration Landscape

| System | Direction | Payload | Standard |
|---|---|---|---|
| City case-management system | Outbound | Referral (risk band, needed service, urgency) | HL7 FHIR `ServiceRequest`, `Task` |
| GP / EHR systems | Outbound | Clinical report | FHIR `DiagnosticReport`, `Observation`; PDF fallback |
| National/city citizen registry | Inbound | Identity, demographics, eligibility | Per-country (e.g., eID) |
| Appointment/scheduling | Bi-directional | Treatment slots, confirmations | FHIR `Appointment` |
| Population health dashboard | Outbound | Aggregated, pseudonymized stats | Bulk FHIR / warehouse feed |
| Wearables/sensors (optional) | Inbound | Gait, activity data | FHIR `Observation`, device APIs |

### 5.2 FHIR Resource Mapping (core set)

- `Patient` — the elderly user; `RelatedPerson` — caregiver/proxy
- `Questionnaire` / `QuestionnaireResponse` — test definitions and answers
- `Observation` — individual scores; `DiagnosticReport` — the assessment result
- `RiskAssessment` — stratification output with reasoning references
- `ServiceRequest` + `Task` — referral to city services and its fulfillment tracking
- `Consent` — recorded consent decisions
- `CarePlan` — the treatment plan the city delivers; outcomes close the loop

**Requirement discipline**: every pathway arrow in Stage 2 must map to an integration row here, with an owner and an error-handling flow (what happens when the city system is down and a Red result must be delivered?).

---

## Stage 6: Write the Functional Specification

```markdown
# [Platform Name] — Functional Specification

## Executive Summary
## 1. Intended Use & Clinical Context (intended-use statement, population, clinical claims)
## 2. Stakeholders & Care Pathway (Stage 1–2 outputs, pathway diagram, SLAs)
## 3. Assessment Module (test battery, scoring, risk bands, human-in-the-loop rules)
## 4. User Experience & Accessibility Requirements
## 5. Referral & Care Delivery Module (triage rules, city-service routing, tracking, outcome feedback)
## 6. Data Model (FHIR resource mapping, consent model, retention)
## 7. Integrations (per-system specs, error handling, downtime procedures)
## 8. Regulatory & Clinical Safety Requirements (classification, hazard log summary, usability engineering)
## 9. Security & Privacy Requirements (access control, audit trail, DPIA actions)
## 10. Reporting & Analytics (clinician report, user report, city population dashboard)
## 11. Testing Strategy (verification, clinical validation plan, usability testing with elderly participants, UAT with city staff)
## 12. Validation Checklist
## 13. Risks & Mitigation
## 14. Appendices (glossary, normative data sources, change log)
```

**Requirement format** — always testable and traceable to a hazard or pathway step:

| ID | Requirement | Source | Acceptance Criteria |
|---|---|---|---|
| FR-014 | System SHALL flag Red-band results to on-call clinician within 15 min | Hazard H-03 | Alert delivered + acknowledged; unacknowledged alerts escalate at 30 min |
| FR-022 | User SHALL be able to pause and resume assessment within 24h without data loss | Accessibility A-02 | Resume restores exact state; timed subtests restart per test rules |

---

## Stage 7: Pilot & Rollout Roadmap

### Phase 1: Clinical Validation Pilot
- Small cohort (e.g., 100–300 users, 1–2 city districts), supervised mode
- Compare digital scores against gold-standard clinical assessment
- Usability sessions with elderly participants (IEC 62366 evidence)
- **Gate**: sensitivity/specificity targets met; usability issues resolved

### Phase 2: Municipal Integration Pilot
- Live referrals to a limited set of city services; measure referral-to-treatment time
- Train city staff; refine triage thresholds against real capacity
- **Gate**: SLA compliance, no unresolved safety incidents, DPIA actions closed

### Phase 3: City-wide Rollout
- Outreach program (invitations via city channels), kiosk + home deployment
- Population dashboard live for health department planning
- Re-assessment cycles scheduled (monitoring mode)

### Ongoing Operations
- Quarterly threshold/algorithm review board (clinical governance)
- Post-market surveillance (SaMD obligation): incident tracking, performance drift monitoring
- Annual consent/retention audit; outcome-loop analysis (did treatments improve trajectories?)

---

## Best Practices

1. **Write the intended-use statement first** — it drives regulation, validation scope, and marketing claims.
2. **Design the exception flows as carefully as the happy path** — unreachable users and full care services are the norm, not the edge case.
3. **The elderly user is the primary persona** — every UX requirement is tested with real elderly users, not proxies.
4. **Risk bands must match city capacity** — a clinically perfect triage that floods services helps no one; involve the city in threshold sign-off.
5. **Close the outcome loop** — treatment outcomes feeding back into the platform is what turns screening into a learning health system.
6. **Traceability is your audit armor** — requirement ↔ hazard ↔ test case linkage will be inspected.

## When to Use This Skill

✅ Specifying health assessment platforms, cognitive/functional test workflows, elderly-focused digital health UX, municipal care-pathway integration, SaMD requirement documentation, FHIR integration mapping.

❌ Not for: giving medical advice or choosing clinical treatments (clinician's domain), regulatory legal opinions (needs qualified RA/legal), hospital ERP implementations, medical hardware design.
