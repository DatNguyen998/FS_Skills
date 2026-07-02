# SAP Transaction Codes & Module Reference

Quick reference guide for SAP transaction codes commonly used in Functional Specifications.

## SAP Modules Overview

### MM - Materials Management (Procurement & Inventory)
Primary business area for procurement, purchasing, inventory, and goods movements.

**Key Processes:**
- Procure-to-Pay (P2P)
- Inventory Management
- Physical Inventory

### SD - Sales & Distribution (Order-to-Cash)
Primary business area for sales, customer order management, and billing.

**Key Processes:**
- Order-to-Cash (O2C)
- Customer Management
- Shipping & Billing

### FI - Finance & Controlling (Accounting)
Primary business area for financial accounting and management accounting.

**Key Processes:**
- General Ledger management
- Accounts Payable
- Accounts Receivable
- Profitability Analysis

### HCM - Human Capital Management
Primary business area for HR, payroll, and employee management.

**Key Processes:**
- Recruitment
- Payroll
- Employee Records
- Time Management

---

## Commonly Used Transaction Codes

### Materials Management (MM)

#### Procurement (Purchase Requisition → PO)
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Create Purchase Requisition | ME51N | Create a new purchase requisition | Transactional |
| Display/Change Requisition | ME53N | View or modify existing requisition | Transactional |
| Purchase Requisition List | ME5A | Search/filter purchase requisitions | Transactional |
| Create Purchase Order | ME21N | Create a new purchase order | Transactional |
| Display/Change PO | ME23N | View or modify purchase order | Transactional |
| Purchase Order List | ME23 | Search/filter purchase orders | Transactional |
| Confirm PO Receipt | MIGO | Goods receipt and invoice receipt | Transactional |
| Maintain Invoice | MIRO | Create/process vendor invoice | Transactional |

#### Master Data Management
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Create Material Master | MM01 | Create new material | Master Data |
| Display/Change Material | MM03 | View or modify material master | Master Data |
| Material List | MM40 | Search materials by attributes | Master Data |
| Create Vendor Master | FK01 | Create new vendor | Master Data |
| Display/Change Vendor | FK02 | View or modify vendor master | Master Data |
| Create Purchasing Group | MEH1 | Define purchasing group | Customizing |
| Create Vendor Evaluation | ME64 | Rate vendor performance | Analytics |

#### Inventory & Storage
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Stock Transfer Order | LT01 | Create transfer between storage locations | Transactional |
| Physical Inventory | MI01 | Create/execute physical inventory | Transactional |
| Stock Counting | MI02 | Record inventory counts | Transactional |
| Inventory Posting | MI03 | Post inventory differences | Transactional |

---

### Sales & Distribution (SD)

#### Order Management
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Create Sales Order | VA01 | Create new sales order | Transactional |
| Display/Change Sales Order | VA03 | View or modify sales order | Transactional |
| Sales Order List | VA05 | Search/filter sales orders | Transactional |
| Create Quotation | VA21 | Create sales quotation | Transactional |
| Create Delivery | VL01N | Create outbound delivery | Transactional |
| Post Goods Issue | VL02N | Confirm shipment/goods issue | Transactional |
| Create Billing Document | VF01 | Create invoice/billing document | Transactional |

#### Master Data Management
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Create Customer Master | XD01 | Create new customer | Master Data |
| Display/Change Customer | XD03 | View or modify customer master | Master Data |
| Customer List | XD04 | Search/filter customers | Master Data |
| Create Product/Material | MM01 | Create new product | Master Data |

#### Shipping & Logistics
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Goods Issue | VL02N | Post goods issue/shipment | Transactional |
| Billing | VF01 | Create billing documents | Transactional |

---

### Finance & Controlling (FI)

#### General Ledger
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Post Document | FB01 | Post general ledger document | Transactional |
| Display Document | FB03 | View posted GL document | Transactional |
| GL Account List | FS10N | Display GL account balances | Analytics |
| Trial Balance | FS10 | Generate trial balance | Analytics |

#### Accounts Payable
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Post Invoice | FB60 | Post vendor invoice to GL | Transactional |
| Post Payment | F-53 | Post vendor payment | Transactional |
| Vendor Line Items | FBL1N | Display vendor transactions | Analytics |
| Vendor Master | FK01 | Create/maintain vendor | Master Data |

#### Accounts Receivable
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Post Invoice | FB70 | Post customer invoice to GL | Transactional |
| Post Payment | F-28 | Post customer payment | Transactional |
| Customer Line Items | FBL5N | Display customer transactions | Analytics |
| Customer Master | FD01 | Create/maintain customer | Master Data |

#### Bank & Cash Management
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Bank Master | FI12 | Create/maintain bank account | Master Data |
| Cash Position | FF.00 | Display cash position | Analytics |

---

### Customizing & Configuration (IMG)

| Area | Transaction | Purpose |
|---|---|---|
| Maintenance Menu | SPRO | Access Implementation Guide (IMG) |
| Customizing Changes | SE14 | Modify table structures |
| Number Ranges | SNRO | Define document numbering |
| Workflows | SWDD | Define business workflows |
| Business Rules | BRF+ | Create complex business rules |
| Transport Organizer | SE09 | Manage transport requests |

---

### Human Capital Management (HCM)

#### Employee Records
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Create Employee | PA40 | Create new employee record | Master Data |
| Display/Change Employee | PA20 | View or modify employee | Master Data |
| Personnel List | PA30 | Search/filter employees | Master Data |

#### Payroll & Time
| Transaction | Code | Purpose | Transaction Type |
|---|---|---|---|
| Time Recording | CAT2 | Record employee time/attendance | Transactional |
| Payroll | PA03 | Execute payroll run | Transactional |
| Payroll Register | PC00_M99_CALC | View payroll results | Analytics |

---

## Data Tables Reference

### Master Data Tables

#### Materials Management
| Table | Key Field | Purpose | Related Tables |
|---|---|---|---|
| MARA | MATNR | Material Master (General) | MARC, MARD, MVKE |
| MARC | MATNR, WERKS | Material Plant Data | MARA |
| MARD | MATNR, WERKS, LGORT | Material Storage Location | MARA, MARC |
| MVKE | MATNR, VKORG, VTWEG | Material Sales View | MARA |
| LFA1 | LIFNR | Vendor Master (General) | LFB1, LFC1 |
| LFB1 | LIFNR, BUKRS | Vendor Company Code | LFA1 |
| LFC1 | LIFNR, EKORG | Vendor Purchasing Org | LFA1 |
| EINA | MATNR, LIFNR, EKORG | Purchasing Info Record | MARA, LFA1 |

#### Sales & Distribution
| Table | Key Field | Purpose | Related Tables |
|---|---|---|---|
| KNA1 | KUNNR | Customer Master (General) | KNB1, KNVV |
| KNB1 | KUNNR, BUKRS | Customer Company Code | KNA1 |
| KNVV | KUNNR, VKORG, VTWEG | Customer Sales Area | KNA1 |

#### Finance & Controlling
| Table | Key Field | Purpose | Related Tables |
|---|---|---|---|
| SKA1 | SAKNR | Chart of Accounts | SKAT, SAKK |
| SKAT | SAKNR, SPRAS | GL Account Text | SKA1 |
| T001 | BUKRS | Company Code Master | T001W, BKPF |
| T001W | BUKRS, WERKS | Company Code Plant Assignment | T001 |
| BKPF | BUKRS, BELNR, GJAHR | Accounting Document Header | BSEG |
| BSEG | BUKRS, BELNR, GJAHR, BUZEI | Accounting Document Line | BKPF |

#### Organizational Data
| Table | Key Field | Purpose | Related Tables |
|---|---|---|---|
| T001 | BUKRS | Company Code | All financial tables |
| T001W | BUKRS, WERKS | Plant | MM/SD tables |
| T024E | EKORG | Purchasing Organization | LFC1, EINA |

---

## Module Relationship Diagram

```
                    ┌──────────────────────────────┐
                    │      FI (Finance)            │
                    │   BKPF, BSEG, SKA1, SKAT    │
                    └──────────────────────────────┘
                         ▲            ▲
                         │            │
                    ┌────┴────┐  ┌────┴──────┐
                    │          │  │           │
                 ┌──▼──┐   ┌──▼──▼──┐   ┌──▼──┐
                 │ MM  │   │  MM/SD │   │ SD  │
                 │P2P  │   │ Shared │   │O2C  │
                 └──▲──┘   └────┬───┘   └──┬──┘
                    │           │          │
          ┌─────────┴─┬─────────┴──────────┴─────────┐
          │           │                              │
      ┌───▼───┐   ┌──▼────┐              ┌─────────▼─┐
      │MARA   │   │LFA1   │              │KNA1       │
      │MARC   │   │LFB1   │              │KNB1       │
      │MARD   │   │LFC1   │              │KNVV       │
      │EINA   │   └───────┘              └───────────┘
      └───────┘

Modules: MM (Materials Management)
         SD (Sales & Distribution)
         FI (Finance & Controlling)
         PS (Project Systems)
         HCM (Human Capital Management)
```

---

## Transaction Code Naming Convention

### Structure:
**[Module Code][2-3 Letter Abbreviation][Optional: N for New version]**

Examples:
- **ME51N** = Materials Management (M-) + Requisition (-E-) + New (-N)
- **VA01** = Sales & Distribution (V-) + Order (-A-) + Create (-01)
- **FB01** = Finance (-F-) + Document (-B-) + Create (-01)

### Key Suffixes:
- **N** = New/modern version (preferred for SAP 4/HANA)
- **1** = Create
- **2** = Change
- **3** = Display
- **4** = List/Selection

### Common Module Prefixes:
- **M** = Materials Management (MM)
- **V** = Sales & Distribution (SD)
- **F** = Finance (FI/CO)
- **H** = HR/HCM
- **P** = Project Systems (PS)
- **O** = Operations (SCM)

---

## SAP Table Naming Convention

### Structure:
**[1-5 Characters: Functional Area][3-5 Characters: Specific Table]**

Examples:
- **MARA** = Materials (MA) + Articles (RA)
- **LFA1** = Supplier (LF) + Account (A1)
- **BKPF** = Accounting (BK) + Posted (PF)
- **KNA1** = Customer (KN) + Account (A1)

### Key Suffixes:
- **1** = Master record header
- **2** = Details/Line items
- **H** = Header
- **D** = Details

---

## When Documenting FS: What to Include

For each transaction code, document:
1. **Code + Description** (e.g., "ME51N - Create Purchase Requisition")
2. **Purpose** (What business activity does it support?)
3. **Key Master Data Required** (Which master records must exist?)
4. **Input Requirements** (What must user enter?)
5. **Output/Results** (What does the system create?)
6. **Related Transactions** (What comes before/after?)

Example:
```markdown
### ME51N - Create Purchase Requisition

**Purpose:** Create a new purchase requisition for procurement

**Prerequisites:**
- Material Master (MARA) must exist
- Plant (MARC) must exist for the material
- Purchasing Group (EKGRP) must be defined

**User Input:**
- Material Number (MATNR)
- Plant (WERKS)
- Quantity Requested (MENGE)
- Delivery Date Required (EINDT)

**Output:**
- Purchase Requisition Number (BANFN) created in PR header (EBAN)
- PR item details stored in (EBANPOS)

**Next Step:**
- Convert to PO via ME21N (Create Purchase Order)
```

---

## Glossary of SAP Terms

- **BADI**: Business Add-In; extension point for custom code
- **BKPF/BSEG**: Accounting document header and line items
- **BUKRS**: Company Code (4-character identifier)
- **EKORG**: Purchasing Organization
- **GJAHR**: Fiscal Year
- **IMG**: Implementation Guide (SAP's configuration menu)
- **LIFNR**: Vendor/Supplier account number
- **MATNR**: Material number/SKU
- **VKORG**: Sales Organization
- **WERKS**: Plant/Facility identifier

