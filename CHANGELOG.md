# Changelog

All notable changes to the FS_Skills business analyst skill set are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versioning follows [Semantic Versioning](https://semver.org/): **MAJOR** for breaking changes (e.g. moved/renamed skill paths), **MINOR** for new skills or new capability added to an existing skill, **PATCH** for corrections and reference-data updates.

A rendered, browsable view of this file is available at [`CHANGELOG.html`](CHANGELOG.html).

---

## [Unreleased]

Nothing yet.

---

## [2.1.0] — 2026-08-19

### Summary
Enriched `fintech-token-ecosystem` with current (2026) regulatory, market, and security-practice research: the SEC/CFTC joint interpretive framework, MiCA's machine-readable whitepaper mandate, the US GENIUS Act for stablecoins, FATF Travel Rule enforcement reality, ERC-3643 institutional adoption data, DAO governance/treasury best practices, and 2025–2026 exploit/audit market data.

### Changed
- **`skills/fintech-token-ecosystem/SKILL.md`**:
  - **Stage 2 (Tokenomics Design)** — added §2.4 "Design Frameworks & Current Practice (2026)": stakeholder analysis / incentive-design / participatory co-design frameworks, the hybrid inflation-then-burn market pattern, and a common-failure-modes table (excessive inflation, utility gap, weak governance, opaque unlocks).
  - **Stage 3 (Token Standard Selection)** — added ERC-4626 to the standards table; added an ERC-3643 institutional-adoption callout ($32B+ RWA tokenized, 180+ jurisdictions, DTCC/Apex/Invesco/Franklin Templeton/Fasanara adopters, ISO standardization in progress).
  - **Stage 4 (Ecosystem Component Mapping)** — added §4.1 "Governance Model — Current Best Practice": tiered decision-making, vote delegation, vote-escrow, hybrid weighting, governance minimization; added §4.2 "Treasury — Current Best Practice": multisig threshold guidance, signer rotation, hardware-key requirement, monitoring, Safe as default tooling.
  - **Stage 5 (Compliance & Risk Analysis)** — reworked §5.1 with the March 2026 SEC/CFTC 5-bucket taxonomy and the marketing-language-driven Howey analysis, the GENIUS Act stablecoin requirements, and MiCA's Dec 2025 XHTML/iXBRL whitepaper format mandate; §5.2 now states current FATF Travel Rule enforcement coverage (~73% legislated, ~40% enforced) with named enforcing jurisdictions; §5.3 risk register reordered and expanded around access-control failures, oracle manipulation, and bridge compromise as the current leading loss categories, with audit cost bands.
  - **Stage 7** — noted the shift from one-time pre-launch audit to continuous post-launch monitoring.
  - Added a closing "A Note on Currency" section pointing to the reference file's sourced research and flagging it for periodic re-verification.
  - **Impacted function:** all 7 workflow stages retain their structure; content deepened, no stage renamed or removed.
- **`skills/fintech-token-ecosystem/references/token-compliance-reference.md`**:
  - Added ERC-3643 adoption note under the standards table.
  - Expanded the Regulatory Frameworks section with the 2026 SEC/CFTC framework, GENIUS Act requirements, and MiCA whitepaper format change.
  - Added "FATF Travel Rule — Enforcement Reality Check (2026)".
  - Added new sections: "Governance Model Quick Reference" and "Treasury Multisig Checklist".
  - Added "Exploit & Audit Market Data (2025–2026)" under the Audit & Security Checklist.
  - Added glossary terms: ve-model, RWA, TWAP.
  - Added a "Sources & Research Currency" section listing every source consulted, dated August 2026.

### Impacted skills/files in this release
| Skill | Impact |
|---|---|
| `fintech-token-ecosystem` | Content enriched (Stages 2–5, 7) + reference file expanded |

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

[Unreleased]: https://github.com/DatNguyen998/FS_Skills/compare/v2.1.0...HEAD
[2.1.0]: https://github.com/DatNguyen998/FS_Skills/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/DatNguyen998/FS_Skills/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/DatNguyen998/FS_Skills/releases/tag/v1.0.0
