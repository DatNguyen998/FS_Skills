---
name: sap-functional-specs
description: Create comprehensive Functional Specifications (FS) for SAP implementations. Use this skill when a functional analyst or business analyst needs to write formal SAP FS documents. The skill covers the complete workflow: gather business process requirements, explore SAP data models and master data relationships, document relevant SAP transaction codes (e.g., MM01, SD01), propose 2-3 implementation approaches with pros/cons analysis, write the formal FS document in structured markdown, enable detailed user review with inline validation checklists, and transition to implementation planning with a detailed roadmap. Triggers whenever the user mentions "functional spec", "FS", "SAP requirement", "data model mapping", or wants to document SAP business requirements systematically.
---

# SAP Functional Specifications Skill

A comprehensive workflow for creating professional Functional Specifications (FS) for SAP implementations.

## Overview

This skill guides functional analysts and business analysts through a structured 7-stage workflow to create complete, implementation-ready SAP FS documents:

1. **Gather Business Context** - Understand the business requirement
2. **Explore FS Context & Structures** - Map SAP modules, tables, and transaction codes
3. **Data Model Mapping** - Visualize Master Data relationships
4. **Propose Approaches** - Present 2-3 options with detailed pros/cons
5. **Write Formal FS** - Generate the complete specification document
6. **User Review** - Iterative review with inline validation
7. **Implementation Transition** - Roadmap to development/configuration phase

---

## Stage 1: Gather Business Context

Start by understanding what the user wants to document. Ask clarifying questions about:

**Essential Questions:**
- **Business Process**: What is the core business process? (e.g., "Procure-to-Pay", "Order-to-Cash")
- **Scope**: Which SAP modules are involved? (MM=Materials Management, SD=Sales & Distribution, FI=Finance, etc.)
- **Trigger**: What event triggers this process? (e.g., "Purchase Requisition created", "Customer Order received")
- **Key Stakeholders**: Who are the primary users? (Procurement team, Sales team, Finance team, etc.)
- **Current State**: Is this a new requirement or a process improvement? Any existing documents?

**If the user hasn't provided full context, proactively ask 3-5 clarifying questions.** Structure your questions to uncover:
- Primary and secondary business actors
- Key decision points and business rules
- Integration points with other systems
- Compliance/regulatory requirements

Example approach:
```
You mentioned "procure-to-pay". Let me clarify a few things:

1. Is this for domestic, international, or both purchase scenarios?
2. Are there approval workflows based on purchase order value?
3. Do you need to handle multiple currencies or vendor types?
4. What's your priority: speed, compliance, or flexibility?
5. Are there existing SAP configurations we should leverage?
```

---

## Stage 2: Explore FS Context & Structures

Once you understand the business requirement, map it to SAP structures. Create a section documenting:

### 2.1 SAP Module & Transaction Code Mapping

Create a structured table showing:

| Business Activity | SAP Module | Transaction Code | Purpose |
|---|---|---|---|
| Create Purchase Requisition | MM | ME51N | Create purchase requisition (new) |
| Create Purchase Order | MM | ME21N | Create purchase order (new) |
| Goods Receipt | MM | MIGO | Goods receipt, invoice receipt |
| Invoice Verification | MM | MIRO | Maintain invoice |

**SAP Transaction Code Naming:**
- First letter(s) = Module code (MM, SD, FI, etc.)
- "N" suffix = New/Modern transaction (e.g., ME51N vs old ME51)
- Always include both the transaction code and description

### 2.2 Key Data Domains

Identify the main data objects involved:
- **Master Data**: Vendor Master (LFA1), Material Master (MARA), Company Code (T001)
- **Transactional Data**: Purchase Orders (EKKO/EKPO), Invoices (RSEG/RBCO)
- **Customizing**: Approval rules, number ranges, workflows

### 2.3 SAP Module Dependencies

Document which modules interact:
```
MM (Materials Management)
  ├─ Integration with FI (Finance/Accounting)
  ├─ Integration with SD (Sales & Distribution) 
  └─ Integration with LE (Logistics)
```

---

## Stage 3: Data Model Mapping

Create both **text and visual** representations of Master Data relationships.

### 3.1 Text Format: Master Data Relationship Table

| Master Data Table | Key Field | Related Tables | Purpose |
|---|---|---|---|
| MARA (Material) | MATNR | MARC, MARD, MVKE | Stores material master data; MARC=plant-specific, MARD=storage location, MVKE=sales view |
| LFA1 (Vendor) | LIFNR | LFB1, LFC1, LFBK | Vendor master; LFB1=company code data, LFC1=purchase org data |
| T001 (Company Code) | BUKRS | T001W, BKPF | Company code definition; T001W=plants, BKPF=accounting documents |

**Include:**
- Primary Key (MATNR, LIFNR, etc.)
- Foreign Key relationships
- Field descriptions for critical fields

### 3.2 Visual Format: Entity Relationship Diagram (ASCII/SVG)

Generate an ASCII diagram showing relationships:

```
┌─────────────┐         ┌──────────────┐
│   MARA      │         │   MARC       │
│ (Material)  │◄────────│ (Plant Data) │
│ MATNR(PK)   │  FK     │ MATNR(FK)    │
└─────────────┘         └──────────────┘
       │                       │
       │                       │
       └───────────┬───────────┘
                   │
            ┌──────▼─────┐
            │   MARD     │
            │(Storage Loc)
            │ MATNR(FK)  │
            └────────────┘
```

**Best Practice**: Use SVG for interactive visualization showing:
- Primary Keys (shown in bold or highlighted)
- Foreign Key relationships (shown as arrows)
- Cardinality notation (1:1, 1:N)
- Color coding by table type (Master Data=Blue, Transaction=Green)

---

## Stage 4: Propose 2-3 Implementation Approaches

Present distinct technical approaches with **detailed pros/cons analysis**. For each approach:

### Structure for Each Approach:

**Approach [N]: [Name/Title]**

**Description:**
Brief 2-3 sentence summary of the approach

**SAP Configuration Elements:**
- List specific customizing areas (e.g., IMG > Materials Management > Purchasing > etc.)
- Include transaction codes for setup (e.g., OMDQ for material type setup)
- Detail any BADI/User Exits involved

**Data Flow Diagram:**
ASCII or text representation of how data moves through the system

**Advantages:**
- Bullet point advantages (clarity, maintainability, performance, cost, timeline)

**Disadvantages:**
- Bullet point disadvantages

**Effort Estimate:**
- Design: X days
- Configuration: Y days
- Testing: Z days
- **Total: A days**

**Risks:**
- Key technical or business risks

**Recommendation Context:**
When to choose this approach (what business scenarios fit best)

---

## Stage 5: Write Formal FS Document

Generate a complete SAP FS document in Markdown with these sections:

```markdown
# [Document Title] - Functional Specification

## Executive Summary
- Business objective
- Scope (modules, processes)
- Expected business value
- Timeline

## 1. Business Requirement Overview
- Current State (As-Is)
- Desired State (To-Be)
- Business Problem Statement
- Success Criteria

## 2. SAP Module Landscape
- Modules Involved (MM, SD, FI, etc.)
- Key Transaction Codes Table
- Integration Points
- Data Governance

## 3. Master Data & Data Models
### 3.1 Master Data Relationships (Text Format)
[Master Data relationship table from Stage 3.1]

### 3.2 Data Model Visualization
[ASCII/SVG diagram from Stage 3.2]

### 3.3 Critical Fields & Attributes
- Key fields for each master data table
- Validation rules
- Data Quality Requirements

## 4. Detailed Process Flow
- Step-by-step process documentation
- SAP transaction codes at each step
- Decision points and business rules
- System integration points

## 5. Data Requirements & Mapping
- Input data structure
- Transformation rules
- Output data requirements

## 6. Implementation Approaches (2-3 Options)
[Detailed approaches from Stage 4]

## 7. Recommended Approach
- Rationale for recommendation
- Why it's best suited for this business case
- Expected outcomes

## 8. Configuration & Customization Details
- IMG paths for configuration
- BADI/User Exits required
- Table enhancements (if needed)
- Report requirements

## 9. Testing Strategy
- Unit test scenarios
- Integration test scenarios
- User acceptance test (UAT) scenarios
- Test data requirements

## 10. User Training & Documentation
- Training materials required
- User roles affected
- Job aids/process documentation

## 11. Validation Checklist
- [ ] Business requirements aligned with stakeholders
- [ ] SAP design reviewed by architect
- [ ] Data model validated
- [ ] Transaction codes confirmed accurate
- [ ] Configuration steps documented
- [ ] Testing scenarios defined
- [ ] Training plan in place
- [ ] Implementation roadmap approved

## 12. Risks & Mitigation
- Technical risks
- Business risks
- Data risks
- Timeline risks

## 13. Appendices
- Glossary of terms
- SAP abbreviations reference
- Change log (for iteration)
```

---

## Stage 6: User Review & Iteration

Enable the user to review and refine the FS with inline validation.

### Review Workflow:

1. **Present the full FS document** to the user
2. **Display validation checklist** from section 11 inline
3. **Ask for feedback** on:
   - Accuracy of business process mapping
   - Completeness of data model
   - Feasibility of proposed approaches
   - Clarity of documentation

### Handling Revisions:

When user provides feedback:
- **Mark changes** with inline comments (e.g., `<!-- REVISED: Changed transaction code from ME21 to ME21N -->`)
- **Track revision history** in the Change Log section
- **Re-validate** affected sections
- **Present updated version** with summary of changes

Example revision format:
```markdown
## 4. Detailed Process Flow

- Step 1: Create Purchase Requisition using **ME51N** <!-- REVISED: Updated to modern transaction -->
  - User fills in: Material, Quantity, Plant, Delivery Date
  - System validates material and plant combination
  - Prerequisite: Material Master (MARA) must exist in plant (MARC)
```

**Change Log Format:**
```markdown
## Change Log

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2024-01-15 | Business Analyst | Initial draft |
| 1.1 | 2024-01-18 | Functional Analyst | Updated transaction codes, clarified data model |
| 1.2 | 2024-01-20 | Business Owner | Approved approaches, added compliance requirements |
```

---

## Stage 7: Implementation Transition

Once the FS is approved, create an **Implementation Roadmap** showing the path to development.

### Implementation Roadmap Template:

```markdown
## Implementation Roadmap

### Phase 1: Design & Setup (Week 1-2)
**Deliverables:**
- SAP configuration checklist completed
- BADI/User Exit specifications reviewed
- Test environment ready (TSTCLNT)

**Key Activities:**
- Run IMG configuration for identified customizing areas
- Create number ranges (if needed): Transaction SNRO
- Setup approval workflows: SAP Business Workflow (SWDD)

**Resources:** SAP Basis, Functional Consultant
**Success Criteria:** All configurations successfully activated

---

### Phase 2: Build & Configuration (Week 3-4)
**Deliverables:**
- All SAP configurations complete
- Custom BADI implementations (if required)
- User Exits coded (if required)
- Transport requests created

**Key Activities:**
- Execute IMG steps from FS section 8
- Implement BADIs: [List specific BADI names]
- Create transport requests: Transaction SE09

**Resources:** SAP Developer, Functional Consultant
**Success Criteria:** Unit testing passed on all configurations

---

### Phase 3: Testing (Week 5-6)
**Deliverables:**
- Test cases executed: [Count]
- UAT sign-off from business
- Production readiness assessment

**Key Activities:**
- Execute test scenarios from FS section 9
- Fix defects found during testing
- Prepare production migration plan

**Resources:** QA Tester, Functional Analyst, Business Users
**Success Criteria:** All test cases passed (100% pass rate)

---

### Phase 4: Production Deployment (Week 7)
**Deliverables:**
- Transport request moved to production
- Production validation completed
- User training conducted
- Go-live readiness confirmed

**Key Activities:**
- Schedule transport deployment: Transaction SE01
- Execute post-implementation validation
- Monitor system performance (Transaction ST03)
- Provide Level-1 support

**Resources:** SAP Basis, Functional Consultant, Support Team
**Success Criteria:** System live with no critical issues

---

### Key Dependencies & Prerequisites:
- [ ] SAP system access (DEV, TST, PRD)
- [ ] Identified team roles (Basis, Developer, Functional Analyst)
- [ ] Master data ready for testing
- [ ] Business stakeholder availability for UAT
- [ ] IT approval for transport deployment

### Risk Mitigation Plan:
| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Configuration complexity | Medium | High | Assign experienced SAP consultant |
| Data quality issues | Medium | Medium | Pre-validation of master data |
| Tight timeline | High | Medium | Prioritize critical config items |

### Go-Live Checklist:
- [ ] All configurations tested and approved
- [ ] Users trained and confident
- [ ] Support team briefed on troubleshooting
- [ ] Rollback plan documented
- [ ] Business owner sign-off obtained
```

---

## Best Practices & Tips

### When Writing FS Documents:

1. **Be Specific About SAP Objects**
   - Always use the correct transaction code (prefer "N" versions like ME21N)
   - Reference table names (MARA, EKKO, etc.)
   - Include IMG paths when describing configuration

2. **Master Data is Critical**
   - Clearly identify all master data requirements
   - Show relationships visually AND textually
   - Document data quality rules

3. **Transaction Codes Matter**
   - Include both code and description
   - Note deprecated vs. modern transactions
   - Show the complete user journey through multiple transactions

4. **Approaches Should Be Distinct**
   - Each approach should represent a different design philosophy (Standard Config vs. Custom Development vs. Hybrid)
   - Include detailed effort estimates
   - Make the comparison easy for decision-makers

5. **Validation is Key**
   - The checklist in section 11 is your quality gate
   - Every item should be checkable by business/technical stakeholders
   - Review should be iterative, not a one-shot approval

6. **Implementation Roadmap Alignment**
   - Connect the roadmap to the FS: reference specific sections
   - Include resource estimates based on approach complexity
   - Add contingency for typical SAP implementation risks

---

## Example: Procure-to-Pay (P2P) FS Structure

If documenting SAP P2P, your FS would include:

**Key Modules & Transactions:**
- MM (Materials Management): ME51N, ME21N, MIGO, MIRO
- FI (Finance): F-43, FK02, FK10N (for vendor management)

**Master Data Tables:**
- MARA (Materials), MARC (Plant-level), MARD (Storage location)
- LFA1 (Vendors), LFB1 (Company code vendor data)
- T001 (Company codes), T001W (Plants)

**Typical Approaches:**
1. **Standard SAP with Minimal Configuration** - Using standard P2P processes, minimal customizing
2. **Extended Configuration with Approval Workflows** - Custom approval hierarchies via SAP Workflow (SWDD)
3. **Hybrid with Custom Development** - Standard P2P + custom BADIs for integration with procurement system

---

## When to Use This Skill

✅ **Use this skill when:**
- Writing a new SAP functional specification document
- Mapping business requirements to SAP modules
- Documenting data model and master data relationships
- Creating implementation approaches with pros/cons
- Need to review and iterate on FS documents
- Planning transition from FS to implementation phase

❌ **Don't use this skill for:**
- Basic SAP transaction training (use SAP training materials instead)
- Pure technical configuration without business context
- Data migration (use data migration skills)
- System performance tuning (use SAP basis skills)

---

## Glossary of Terms

- **FS (Functional Specification)**: Document describing what the system should do from a business perspective
- **BADI**: Business Add-In; extension point in SAP for custom code
- **IMG**: Implementation Guide; SAP's configuration/customization tool
- **Master Data**: Reference data that doesn't change frequently (materials, vendors, customers)
- **Transactional Data**: Data created during business processes (orders, invoices, receipts)
- **Transport Request**: Vehicle for moving code/configuration between SAP systems
- **Module**: Business area in SAP (MM, SD, FI, HCM, etc.)

---

## Document Change Log

This skill document itself may be updated. Track updates here:

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2024-01 | Initial skill creation |

