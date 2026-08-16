# Changelog

All notable changes to the FS_Skills business analyst skill set are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versioning follows [Semantic Versioning](https://semver.org/): **MAJOR** for breaking changes (e.g. moved/renamed skill paths), **MINOR** for new skills or new capability added to an existing skill, **PATCH** for corrections and reference-data updates.

A rendered, browsable view of this file is available at [`CHANGELOG.html`](CHANGELOG.html).

---

## [Unreleased]

Nothing yet.

---

## [2.0.0] — 2026-08-16

### Summary
Restructured the repository from a single SAP skill into a multi-skill business analyst set, and added three new domain skills: Fintech token ecosystems, Medtech elderly cognitive health, and AI-collaborative demo building.

### ⚠ Breaking
- **Moved** `SKILL.md` → `skills/sap-functional-specs/SKILL.md`. Any reference, bookmark, or automation pointing at the old root-level path will break.
- **Moved** reference files into `skills/sap-functional-specs/references/`:
  - `sap-transactions-reference.md`
  - `example-p2p-fs.md`
  - `quick-reference.md`
- **Impacted function:** skill discovery/invocation for `sap-functional-specs` — the skill's own content and 7-stage workflow are unchanged, only its file location moved.

### Added
- **New skill `fintech-token-ecosystem`** (`skills/fintech-token-ecosystem/SKILL.md`) — 7-stage workflow for token launches and ecosystem management: business context, tokenomics design (supply/allocation/vesting/incentive loops), token standard & platform selection, ecosystem component mapping (wallets, exchanges, staking, governance, treasury), compliance & risk analysis (MiCA, SEC/Howey, KYC/AML), formal FS with smart-contract functional requirements, and TGE launch/lifecycle roadmap.
  - New reference: `skills/fintech-token-ecosystem/references/token-compliance-reference.md` — token standards cheat sheet, regulatory framework summaries by jurisdiction, KYC/AML requirement starter set, audit & security checklist.
- **New skill `medtech-cognitive-health`** (`skills/medtech-cognitive-health/SKILL.md`) — 7-stage workflow for elderly functional-brain/health assessment platforms: clinical & business context, care pathway mapping (test → score → triage → city-delivered treatment), assessment model definition (test battery, scoring, risk stratification, accessibility), regulatory & data protection analysis (SaMD/MDR/FDA, GDPR/HIPAA, clinical safety hazard log), interoperability design (HL7 FHIR resource mapping to city systems), formal FS, and pilot/rollout roadmap.
  - New reference: `skills/medtech-cognitive-health/references/healthcare-standards-reference.md` — MDR/FDA pathways, GDPR/HIPAA summary, FHIR resource cheat sheet, validated clinical instruments table, hazard log starter set.
- **New skill `ai-demo-collaboration`** (`skills/ai-demo-collaboration/SKILL.md`) — 6-stage workflow for business analysts building demos in direct collaboration with AI: demo framing (one-question charter), persona & journey scoping, AI-buildable spec writing, the build-review-refine loop, demo day & structured feedback capture, and the demo-to-production requirements bridge.
  - New reference: `skills/ai-demo-collaboration/references/demo-spec-template.md` — copy-paste demo charter, AI-buildable spec template, prompt patterns for the build loop, demo-ready checklist, feedback capture sheet, and demo-to-production gap table.
- `CHANGELOG.md` and `CHANGELOG.html` (this record).

### Changed
- **`README.md`** — rewritten as an index of all four skills (previously documented only the SAP skill package). Adds a skill overview table, the new `skills/` directory tree, and a note on how the AI demo skill's output feeds into the domain skills' FS workflows.

### Impacted skills/files in this release
| Skill | Impact |
|---|---|
| `sap-functional-specs` | Path moved only; workflow content unchanged |
| `fintech-token-ecosystem` | New |
| `medtech-cognitive-health` | New |
| `ai-demo-collaboration` | New |
| `README.md` | Rewritten |

---

## [1.0.0] — 2026-05-13

### Summary
Initial release: a single SAP Functional Specifications skill for business/functional analysts.

### Added
- `SKILL.md` — `sap-functional-specs` skill with a 7-stage workflow (gather business context → explore SAP structures & transaction codes → data model mapping → propose 2-3 implementation approaches → write the formal FS → user review & iteration → implementation transition roadmap).
- `sap-transactions-reference.md` — SAP module, transaction code, and master-data table reference.
- `example-p2p-fs.md` — complete worked Procure-to-Pay FS example.
- `quick-reference.md` — user guide to the skill's workflow.
- `README.md` — initial package documentation.

### Impacted skills/files in this release
| Skill | Impact |
|---|---|
| `sap-functional-specs` | New |

[Unreleased]: https://github.com/DatNguyen998/FS_Skills/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/DatNguyen998/FS_Skills/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/DatNguyen998/FS_Skills/releases/tag/v1.0.0
