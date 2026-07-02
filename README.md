# Business Analyst Skills

A collection of Claude skills for business analysts, covering functional specification writing and requirement analysis across the domains I work in: SAP, Fintech (token ecosystems), Medtech (elderly cognitive health), and AI-collaborative demo building.

## Skills Overview

| Skill | Domain | Use it when… |
|---|---|---|
| [`sap-functional-specs`](skills/sap-functional-specs/SKILL.md) | SAP / ERP | Writing SAP functional specifications: module mapping, transaction codes, master data models, implementation approaches |
| [`fintech-token-ecosystem`](skills/fintech-token-ecosystem/SKILL.md) | Fintech / Web3 | Launching a new token and managing its ecosystem: tokenomics, token standards, smart contract requirements, wallets/staking/governance, KYC/AML & MiCA/SEC compliance, TGE roadmap |
| [`medtech-cognitive-health`](skills/medtech-cognitive-health/SKILL.md) | Medtech / Digital Health | Specifying platforms where elderly users take functional brain / health tests, the system stratifies their condition, and city health services deliver treatment based on the results: care pathways, scoring, SaMD regulation, GDPR/HIPAA, HL7 FHIR integration |
| [`ai-demo-collaboration`](skills/ai-demo-collaboration/SKILL.md) | AI-assisted BA work | Collaborating directly with AI to build demos for end users: demo charter, AI-buildable specs, the build-review-refine loop, feedback capture, and converting a validated demo into production requirements |

## Repository Structure

```
FS_Skills/
├── README.md                                  (this index)
└── skills/
    ├── sap-functional-specs/
    │   ├── SKILL.md                           (7-stage SAP FS workflow)
    │   └── references/
    │       ├── sap-transactions-reference.md  (transaction codes & tables)
    │       ├── example-p2p-fs.md              (complete P2P FS example)
    │       └── quick-reference.md             (user guide)
    ├── fintech-token-ecosystem/
    │   ├── SKILL.md                           (token & ecosystem BA workflow)
    │   └── references/
    │       └── token-compliance-reference.md  (standards, MiCA/SEC/AML, audit checklist)
    ├── medtech-cognitive-health/
    │   ├── SKILL.md                           (assessment platform BA workflow)
    │   └── references/
    │       └── healthcare-standards-reference.md  (MDR/FDA, GDPR/HIPAA, FHIR, instruments)
    └── ai-demo-collaboration/
        ├── SKILL.md                           (AI-collaborative demo workflow)
        └── references/
            └── demo-spec-template.md          (charter, spec, prompt patterns, checklists)
```

## How the Skills Fit Together

- The **domain skills** (SAP, Fintech, Medtech) each follow the same discipline: gather context → map the domain → propose approaches → write a formal, testable functional specification → validate → plan implementation.
- The **AI demo skill** is cross-cutting: use it to prototype and validate an idea quickly with AI, then feed the validated learnings into the appropriate domain skill's FS workflow (its Stage 6 explicitly bridges demo shortcuts into production requirements).

## Using a Skill

1. Open the skill's `SKILL.md` and follow its staged workflow.
2. Keep the `references/` files at hand — they contain lookup tables (transaction codes, token standards, FHIR resources), regulatory checklists, and reusable templates.
3. Each skill defines its own "When to use / When not to use" section — check it before starting.

## Maintenance

Update a skill when its domain shifts:
- **SAP**: new S/4HANA transactions or processes
- **Fintech**: new regulation (MiCA technical standards, SEC actions), new token standards
- **Medtech**: MDR/FDA guidance updates, new FHIR releases, new validated instruments
- **AI demo**: new AI tooling capabilities that change the build loop
