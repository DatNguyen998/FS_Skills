# SAP Functional Specs Skill - Quick Reference Card

## When to Use This Skill

✅ Use when you need to:
- Document a new SAP business process requirement
- Create a formal Functional Specification (FS) document
- Map business requirements to SAP modules and transaction codes
- Design data models and master data relationships
- Propose multiple implementation approaches
- Iterate and review FS with stakeholders
- Plan transition from FS to implementation phase

---

## The 7-Stage Workflow

### 📋 Stage 1: Gather Business Context (15 min)
**What happens:**
- You describe the business process you want to implement in SAP
- The skill asks clarifying questions about modules, stakeholders, scope
- The skill clarifies current state vs. desired state

**What you provide:**
- Brief description of business requirement (e.g., "Procure-to-Pay with vendor evaluation")
- Business drivers/pain points
- Key stakeholders & users

**What you get:**
- Clear understanding of scope
- List of SAP modules involved
- Identified decision points

**Example:** "We need to streamline purchase order approvals with vendor quality checks"

---

### 🔍 Stage 2: Explore FS Context & Structures (20 min)
**What happens:**
- The skill maps your requirement to SAP modules and transaction codes
- Creates a table showing business activities → SAP transactions
- Documents key data domains and module dependencies
- Lists SAP abbreviations (MM, SD, FI, etc.)

**What you get:**
- Transaction code mapping (e.g., ME51N for PR, ME21N for PO)
- SAP module structure diagram
- Key data domains involved

**Example output:**
```
| Business Activity | SAP Module | Transaction |
|---|---|---|
| Create PR | MM | ME51N |
| Create PO | MM | ME21N |
| Goods Receipt | MM | MIGO |
```

---

### 🗂️ Stage 3: Data Model Mapping (20 min)
**What happens:**
- The skill creates BOTH text and visual representations
- Documents Master Data relationships
- Shows table names (MARA, MARC, LFA1, etc.)
- Creates ASCII or SVG diagram of data relationships
- Lists critical fields and validation rules

**What you get:**
- Master Data relationship table (readable format)
- Visual diagram showing FK relationships
- Understanding of which tables interact

**Example:** 
- Text table showing MARA (Material) → MARC (Plant) → MARD (Storage Location)
- ASCII diagram visualizing the relationships

---

### 💡 Stage 4: Propose 2-3 Approaches (30 min)
**What happens:**
- The skill proposes distinct implementation approaches (each is genuinely different)
- For each approach:
  - Describes the design philosophy
  - Lists SAP configuration elements (IMG paths, transactions)
  - Shows data flow
  - Details pros and cons
  - Estimates effort (days/weeks)
  - Identifies risks & mitigation
  - Recommends when to use it

**What you get:**
- **Approach 1:** Standard Config (fast, limited flexibility)
- **Approach 2:** Enhanced Config + BADI (balanced, more customization)
- **Approach 3:** Hybrid with EDI/Analytics (advanced, more integration)

**Choose based on:**
- Timeline pressure (fast = Standard Config)
- Complexity needed (high = Enhanced Config + BADI)
- Integration requirements (EDI/Analytics = Hybrid)
- Budget/resource availability

---

### ✍️ Stage 5: Write Formal FS (60 min)
**What happens:**
- The skill generates a complete, structured FS document in Markdown
- Includes all standard FS sections:
  1. Executive Summary
  2. Business Requirement Overview
  3. SAP Module Landscape
  4. Master Data & Data Models
  5. Detailed Process Flow
  6. Data Requirements & Mapping
  7. Implementation Approaches (2-3 options)
  8. Recommended Approach
  9. Configuration & Customization Details
  10. Testing Strategy
  11. User Training & Documentation
  12. Validation Checklist
  13. Risks & Mitigation
  14. Appendices

**What you get:**
- Production-ready FS document
- Detailed process flows with transaction codes
- Data model diagrams (ASCII + SVG)
- Complete approach analysis
- Testing and implementation roadmap

**Document is ready for:**
- Stakeholder review
- Architecture sign-off
- Development team handoff

---

### 👁️ Stage 6: User Review & Iteration (30-60 min, iterative)
**What happens:**
- You review the FS document (section by section or all at once)
- You provide feedback: corrections, clarifications, suggestions
- The skill updates the document with your changes
- Changes are marked with inline comments (e.g., `<!-- REVISED: ... -->`)
- Version history is tracked in a Change Log

**How it works:**
1. You say: "Please update section 4 with the approval workflow details"
2. Skill updates the section with your feedback
3. Skill marks the change: `<!-- REVISED: Added workflow detail on 2024-01-20 -->`
4. Skill shows you the updated section for confirmation
5. You approve or request further changes

**What you can revise:**
- Business process details (if requirements change)
- Transaction code accuracy
- Data model relationships
- Approach pros/cons
- Effort estimates
- Testing scenarios
- Implementation timeline
- Risk assessments

**Change Log automatically tracks:**
| Version | Date | Changes |
|---|---|---|
| 1.0 | 2024-01-15 | Initial FS draft |
| 1.1 | 2024-01-18 | Updated approval workflow (Reviewer A) |
| 1.2 | 2024-01-20 | Clarified vendor evaluation thresholds (Reviewer B) |

---

### 🚀 Stage 7: Implementation Transition (30 min)
**What happens:**
- The skill creates an **Implementation Roadmap** 
- Maps from FS to actual project execution
- Includes:
  - **Phase 1: Design & Setup** (Week 1-2) - What to configure, who's involved
  - **Phase 2: Build & Config** (Week 3-4) - IMG steps, BADI coding, testing prep
  - **Phase 3: Testing** (Week 5-6) - Unit, integration, UAT test execution
  - **Phase 4: Production Deployment** (Week 7) - Go-live, cutover, support

**For each phase:**
- Deliverables (what will be completed)
- Key activities (what will be done)
- Resources needed (who, skill level)
- Success criteria (how we know it's done)
- Dependencies & prerequisites

**Go-Live Checklist includes:**
- All configurations tested ☐
- Users trained ☐
- Support team briefed ☐
- Rollback plan ready ☐
- Business owner sign-off ☐

**What you get:**
- Clear handoff from FS → Implementation team
- Timeline from start to go-live
- Resource requirements
- Risk mitigation for each phase
- Rollback plan (if needed)

---

## Document Structure

The skill produces a Markdown (.md) file with:

```
# Title - Functional Specification

## Executive Summary
- Business objective, scope, timeline

## 1. Business Requirement Overview
- Current state, desired state, success criteria

## 2. SAP Module Landscape
- Modules involved, key transaction codes

## 3. Master Data & Data Models
- Text format table + Visual diagram (SVG/ASCII)

## 4. Detailed Process Flow
- Step-by-step transactions & business rules

## 5. Data Requirements & Mapping
- Input/output formats, transformation rules

## 6. Implementation Approaches (2-3)
- Option 1, Option 2, Option 3 (detailed pros/cons)

## 7. Recommended Approach
- Why this one is best for your situation

## 8. Configuration & Customization
- IMG paths, BADI specs, custom tables

## 9. Testing Strategy
- Unit tests, integration tests, UAT scenarios

## 10. User Training & Documentation
- Training plan, job aids, roles affected

## 11. Validation Checklist
- [ ] All requirements aligned
- [ ] Design reviewed
- [ ] Testing scenarios defined
... (20+ checklist items)

## 12. Risks & Mitigation
- Technical, business, data, timeline risks

## 13. Appendices
- Glossary, SAP abbreviations, change log, sign-off

## Change Log (Iteration History)
| Version | Date | Changes |
```

---

## How to Request Changes

### During Review (Stage 6):

**Option A: Specific Section Changes**
```
"Please update Section 4 (Process Flow) with these details:
- Step 3: Add approval workflow details
- Step 5: Change transaction code from MIRO to MM_INVOICE
- Add note about tolerance for price variance"
```

**Option B: Whole Document Review**
```
"I've reviewed the complete FS. Here are my comments:
1. Business requirements look good ✓
2. Transaction codes need verification (I'll review against our system)
3. Approach 2 looks best - can you emphasize this in recommendations
4. Testing scenarios missing UAT for vendor blocking scenario
5. Can we accelerate timeline from 8 weeks to 6 weeks?"
```

**Option C: Spot Corrections**
```
"In Section 3.1, the MARA → MARC relationship description is incomplete.
Please add: 'MARC contains plant-level material data like purchasing unit of measure and replenishment lead time.'"
```

### Change Tracking:

Every change is:
1. **Marked inline**: `<!-- REVISED: [what changed] on [date] -->`
2. **Tracked in Change Log**: Version incremented, change summary added
3. **Presented to you**: Updated section shown for confirmation

---

## Tips for Success

### ✅ DO:

- **Be specific about business requirements** → "Approve POs based on amount and cost center" (not just "approvals")
- **Involve stakeholders early** → Gather input from all user groups (procurement, finance, operations)
- **Review approaches carefully** → Each has different effort, risk, and flexibility trade-offs
- **Ask for clarifications** → If a section is unclear, ask the skill to explain with an example
- **Track changes** → Use the Change Log to document who approved what and when
- **Get sign-offs** → Get business owner + technical architect signature before implementation starts

### ❌ DON'T:

- Don't skip Stage 1 (Gather Context) → Rushing leads to incomplete requirements
- Don't ignore risks → Every approach has risks; mitigation is key
- Don't pick an approach based only on cost → Consider timeline, flexibility, S/4HANA compatibility
- Don't start coding before FS is approved → Changes mid-development are expensive
- Don't assume vendor will support all transaction codes → Verify compatibility with your SAP version

---

## Common SAP Terms Used in FS

| Term | Meaning |
|---|---|
| **MARA** | Material Master header table |
| **MARC** | Material plant-level data |
| **MARD** | Material storage location data |
| **LFA1** | Vendor Master |
| **EINA** | Purchasing Info Record (prices, terms) |
| **BADI** | Business Add-In (custom code extension point) |
| **IMG** | Implementation Guide (SAP config menu) |
| **3-Way Match** | PO quantity = GR quantity = Invoice quantity |
| **SWDD** | Workflow Definition tool |
| **FI** | Finance module |
| **MM** | Materials Management module |
| **SD** | Sales & Distribution module |

---

## Example: How to Use the Skill

**Step 1: You Describe Your Need**
"We're implementing SAP Procure-to-Pay with vendor evaluation. Need to ensure only high-quality vendors are used. Critical to block low-rated vendors at PO creation."

**Step 2: Skill Gathers Context**
"Perfect. Let me ask a few questions:
1. What modules involved? (MM, FI, which else?)
2. Who approves PRs? (Manager, Finance, Director?)
3. How is vendor score calculated? (Quality metrics, cost, delivery?)
4. Timeline? (Weeks to implement?)"

**Step 3: You Provide Context**
"MM and FI. Manager → Finance → Director approval (amount-based). Vendor score = 80% quality + 20% cost/delivery. Need to go live in 8 weeks."

**Step 4: Skill Creates FS**
*Generates 50-page document with all sections, diagrams, approaches, roadmap*

**Step 5: You Review (2-3 iterations)**
"Section 4: Clarify the vendor blocking logic"
→ Skill updates with clarification
→ You approve

"Section 6: Approach 2 looks best for our timeline"
→ Skill emphasizes Approach 2 in recommendations

**Step 6: Skill Creates Implementation Roadmap**
*Detailed 8-week plan with phases, deliverables, resources*

**Step 7: Document Ready for Handoff**
*Complete FS document approved by all stakeholders, ready for development team*

---

## Getting Help

**If you need clarification:**
- Ask the skill to "explain [section]" with examples
- Request a "summary of [approach]" for quick comparison
- Ask for "more detail on [topic]" if something is vague

**If requirements change mid-stream:**
- Document the change in Stage 6 (User Review)
- Update the FS with new details
- Re-evaluate affected approaches
- Track all changes in Change Log

**If you want to restart:**
- Save the current FS (good starting point)
- Start fresh with new business requirement
- Reference old FS for comparison/learnings

---

## Next Steps After FS Approval

1. **Design Review** (Architecture team) - Validate technical approach
2. **Project Planning** - Build detailed project plan from Phase 1-4 roadmap
3. **Configuration** - Execute IMG configuration from Section 8
4. **Development** - Implement BADI/custom code (if needed)
5. **Testing** - Execute test scenarios from Section 9
6. **Training** - Deliver training materials from Section 10
7. **Go-Live** - Execute Phase 4 deployment plan
8. **Support** - Monitor system for 2 weeks post-go-live

---

## Questions?

The skill is designed to be self-guided, but if you get stuck:
- Ask the skill to **explain any section** in simpler terms
- Request **examples** of how to use specific transaction codes
- Ask for **alternatives** if a proposed approach doesn't fit
- Request **side-by-side comparison** of the 3 approaches

**Your FS document will be:**
- ✅ Complete & comprehensive
- ✅ Ready for stakeholder review
- ✅ Implementable by your project team
- ✅ Aligned with SAP best practices
- ✅ Tracked with version history & change log

