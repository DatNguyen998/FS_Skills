# Healthcare Standards & Regulatory Quick Reference

Companion reference for the `medtech-cognitive-health` skill.

## Regulatory Frameworks

### EU — Medical Device Regulation (MDR 2017/745)
- **Rule 11** governs software: software intended to provide information used for diagnostic/therapeutic decisions → at least Class IIa; Class IIb/III if decisions may cause serious deterioration/death
- Requires: CE marking via Notified Body (Class IIa+), technical documentation, clinical evaluation report (MEDDEV 2.7/1), post-market surveillance plan, UDI registration in EUDAMED

### US — FDA
- **SaMD pathways**: 510(k) (predicate exists), De Novo (novel, low-moderate risk), PMA (high risk)
- **CDS exemption** (21st Century Cures Act): software may be exempt if the clinician can independently review the basis of recommendations — auto-triage without transparency usually breaks this
- **Digital health**: FDA Digital Health Center of Excellence guidance; predetermined change control plans for AI/ML-based SaMD

### Key Process Standards
| Standard | Scope |
|---|---|
| IEC 62304 | Medical device software lifecycle (classes A/B/C by harm potential) |
| ISO 14971 | Risk management for medical devices (hazard log methodology) |
| IEC 62366-1 | Usability engineering (use-related risk, summative evaluation) |
| ISO 13485 | Quality management system for medical devices |
| ISO 27001 / ISO 27799 | Information security (27799 = health-specific) |

## Data Protection

### GDPR (EU)
- Health data = special category (Art. 9); lawful bases typically: explicit consent 9(2)(a), health/social care 9(2)(h), public interest in public health 9(2)(i)
- DPIA mandatory (Art. 35) — large-scale processing of health data
- Controller/processor mapping: city vs. platform vendor must be contractually explicit (Art. 28 DPA)
- Rights handling: access, rectification, erasure (with medical-record retention conflicts documented), portability

### HIPAA (US)
- Privacy Rule (minimum necessary), Security Rule (administrative/physical/technical safeguards), Breach Notification Rule
- Business Associate Agreements for every vendor touching PHI
- De-identification: Safe Harbor (18 identifiers) or Expert Determination

## HL7 FHIR Resource Cheat Sheet (R4/R5)

| Resource | Use in assessment platform |
|---|---|
| `Patient` / `RelatedPerson` | Elderly user; caregiver or legal guardian |
| `Questionnaire` / `QuestionnaireResponse` | Test battery definition; user's answers |
| `Observation` | Individual test/domain scores (LOINC-coded where possible) |
| `DiagnosticReport` | Composed assessment result for clinicians |
| `RiskAssessment` | Risk band with `basis` references to observations |
| `ServiceRequest` | Referral to city service |
| `Task` | Fulfillment tracking of the referral |
| `Appointment` | Scheduled treatment/assessment slots |
| `CarePlan` / `Goal` | City-delivered treatment plan and targets |
| `Consent` | Granular consent records |
| `Device` / `DeviceUseStatement` | Sensors/wearables used in testing |
| `AuditEvent` | Access and disclosure logging |

**Terminologies**: LOINC (observations/tests), SNOMED CT (findings/conditions), ICD-10 (diagnoses for registries).

## Common Validated Instruments (for test-battery grounding)

| Instrument | Domain | Notes for digital adaptation |
|---|---|---|
| MoCA / MMSE | Global cognition | Licensed; digital versions exist; education bias documented |
| Trail Making A/B | Processing speed, executive | Adapts well to touch; norms needed per device |
| Digit Span | Working memory | Audio quality critical for elderly users |
| Verbal fluency | Language/executive | Needs speech recognition validated for aged voices |
| GDS-15 | Depression screening (geriatric) | Self-report; escalation rules required for high scores |
| Timed Up & Go (TUG) | Mobility/fall risk | Sensor/camera based; supervised mode recommended |
| Katz ADL / Lawton IADL | Functional independence | Proxy-report mode useful |

> Any adaptation of a validated instrument to digital form requires its own validation evidence — treat scores as non-equivalent until proven.

## Clinical Safety Hazard Log Starter Set

| ID | Hazard | Typical mitigations |
|---|---|---|
| H-01 | False negative → missed deterioration | Conservative thresholds, scheduled re-testing, symptom self-report channel |
| H-02 | False positive → anxiety, wasted capacity | Clinician confirmation before referral, clear "screening not diagnosis" messaging |
| H-03 | Delayed escalation of urgent result | Alert SLAs, acknowledgment tracking, escalation chain |
| H-04 | Wrong-patient data | Identity verification per session, caregiver-mode flagging |
| H-05 | Test invalid due to assistance/environment | Validity flags, supervised re-test pathway |
| H-06 | Data breach of health data | Encryption at rest/in transit, access control, audit, DPIA actions |
| H-07 | Service unavailable during urgent flow | Offline procedure, manual fallback contact protocol |

## Glossary

- **SaMD**: Software as a Medical Device — software with a medical purpose, standalone from hardware
- **MCI**: Mild Cognitive Impairment — decline greater than normal aging, short of dementia
- **Triage**: sorting users by urgency/need to route care
- **DPIA**: Data Protection Impact Assessment (GDPR)
- **Sensitivity/Specificity**: true-positive rate / true-negative rate of a screening test
- **Post-market surveillance**: ongoing monitoring of a medical device after release
- **Normative data**: reference score distributions used to judge an individual's result
