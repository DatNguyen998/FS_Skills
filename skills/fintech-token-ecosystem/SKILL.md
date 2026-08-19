---
name: fintech-token-ecosystem
description: Business analysis for Fintech token creation and ecosystem management. Use this skill when a business analyst needs to define requirements for launching a new digital token and managing its full ecosystem — tokenomics design, token standard selection, smart contract functional specs, wallet/exchange/staking/governance features, compliance (KYC/AML, MiCA, securities analysis), and ecosystem operations. Triggers when the user mentions "token", "tokenomics", "token launch", "crypto ecosystem", "smart contract requirements", "DeFi", "web3 BA", or wants to document requirements for blockchain-based financial products.
---

# Fintech Token & Ecosystem Business Analysis Skill

A structured workflow for business analysts defining, specifying, and managing the launch of a new token and its surrounding ecosystem.

## Overview

This skill guides a BA through 7 stages, from business intent to an implementation-ready specification package:

1. **Gather Business Context** — Why a token? What problem does it solve?
2. **Tokenomics Design** — Supply, distribution, utility, incentives
3. **Token Standard & Platform Selection** — Chain, standard, custody model
4. **Ecosystem Component Mapping** — Wallets, exchanges, staking, governance, treasury
5. **Compliance & Risk Analysis** — Regulatory classification, KYC/AML, jurisdiction
6. **Write the Functional Specification** — Token FS + ecosystem FS
7. **Launch & Lifecycle Roadmap** — TGE plan, listing, ongoing ecosystem management

---

## Stage 1: Gather Business Context

Before any token design, establish whether a token is justified and what it must achieve.

**Essential Questions:**
- **Purpose**: What is the token for? (payment, utility/access, governance, reward/loyalty, asset-backed, security)
- **Users**: Who holds and uses it? (retail users, institutions, partners, internal ecosystem participants)
- **Value flow**: Where does value enter and exit the ecosystem? (fiat on-ramp, revenue share, fees)
- **Business model**: How does the issuing organization capture value? (fee capture, treasury appreciation, service revenue)
- **Constraints**: Target jurisdictions, launch timeline, budget, existing infrastructure

**Red-flag check (document explicitly):**
- Could this be solved with a database instead of a token? If yes, why is a token still preferred?
- Does the token resemble a security in target jurisdictions? (see Stage 5)

Example clarifying questions:
```
You mentioned launching a new token. Let me clarify:

1. Is the token a utility token (access to services), a payment token, or does it carry governance rights?
2. Which jurisdictions will users come from? (EU → MiCA, US → SEC/Howey, APAC → varies)
3. Public chain, private/permissioned chain, or L2?
4. Will the token be freely tradable, or restricted (whitelist/KYC-gated transfers)?
5. Who manages the treasury and under what governance?
```

---

## Stage 2: Tokenomics Design

Document the economic design in a **Tokenomics Sheet**:

### 2.1 Supply Model

| Parameter | Definition | Example |
|---|---|---|
| Max supply | Hard cap or uncapped | 1,000,000,000 fixed |
| Initial circulating supply | Tokens liquid at TGE | 8% of max |
| Emission schedule | Inflation/minting rules | Linear over 48 months |
| Burn mechanics | Deflationary rules | 30% of protocol fees burned |
| Mint authority | Who can mint, under what rules | Multisig 3-of-5, DAO vote after year 1 |

### 2.2 Allocation & Vesting

| Bucket | % | Cliff | Vesting | Rationale |
|---|---|---|---|---|
| Team & advisors | 15% | 12 mo | 36 mo linear | Retention, market confidence |
| Investors (seed/private) | 20% | 6 mo | 24 mo linear | Capital raise |
| Ecosystem incentives | 30% | — | Programmatic | Liquidity mining, user rewards |
| Treasury/reserve | 25% | — | DAO-controlled | Runway, partnerships |
| Public sale / airdrop | 10% | — | Unlocked | Distribution, decentralization |

### 2.3 Utility & Incentive Loops

Document every reason to hold or use the token as a loop:
```
User pays fees in token → portion burned → supply pressure ↓
Staker locks token → earns fee share → circulating supply ↓ → network security ↑
Holder votes in governance → influences treasury → ecosystem grows → demand ↑
```

**BA deliverable**: each loop must map to a functional requirement (e.g., "burn 30% of fees" → smart contract requirement FR-012).

### 2.4 Design Frameworks & Current Practice (2026)

Don't design tokenomics ad hoc — anchor the sheet to a named framework so stakeholders can interrogate the reasoning:

- **Stakeholder Analysis Framework**: enumerate every participant group (users, LPs, validators/stakers, investors, team, DAO) and their motivation *before* setting allocations — allocations should fall out of this analysis, not the other way round.
- **Incentive/Mechanism Design Framework**: apply game-theory checks to each loop — can a rational actor extract value without contributing (free-riding), or coordinate to capture governance cheaply (plutocracy/sybil risk)?
- **Participatory co-design** (for community/city-linked tokens): a 4-phase method — contextual framing → socioeconomic modeling → mechanism design → technical token specification — useful when non-technical stakeholders (a municipality, a member cooperative) must sign off on the economic design, not just the contract.

**Current market practice to weigh against your design:**
- The dominant 2026 pattern is a **hybrid model**: inflationary emissions during the growth/bootstrap phase, phasing into deflationary burns + staking lockups as the ecosystem matures — pure fixed-supply and pure infinite-inflation designs are both increasingly seen as naive.
- Favor **fixed or capped supply with activity-linked burn** (burn rate tied to real usage, not a flat schedule) over purely time-based emission curves — it ties scarcity to adoption rather than to a calendar.
- Design for **multi-utility**, not a single use case — a token that is only a governance token, or only a fee token, is thinner ecosystem glue than one with 2–3 reinforcing utilities.

**Common failure modes to check against explicitly:**

| Risk | Symptom | Mitigation |
|---|---|---|
| Excessive inflation | Emissions outpace real demand → constant sell pressure | Cap emission as % of circulating supply per epoch; tie to usage metrics |
| Utility gap | Token is held speculatively with no required use | Require ≥1 "must-use" utility (fee payment, access gating) not just "nice-to-have" |
| Weak governance | Low quorum lets a small group push proposals | See Stage 4 governance model — set quorum/delegation rules before launch, not after a low-turnout vote fails |
| Opaque unlocks | Market surprised by cliff/unlock events | Publish the full vesting schedule and a public unlock calendar before TGE |

**BA deliverable**: before sign-off, require a simple simulation (spreadsheet is enough) modeling circulating supply vs. projected demand across at least the first 24 months, stress-tested against the worst-case unlock month.

---

## Stage 3: Token Standard & Platform Selection

Present 2–3 platform/standard options with pros/cons (mirror the approach-comparison discipline of a classic FS):

### Common Standards Reference

| Standard | Chain | Use Case |
|---|---|---|
| ERC-20 | Ethereum/EVM L2s | Fungible utility/payment tokens |
| ERC-721 / ERC-1155 | EVM | NFTs, semi-fungible assets |
| ERC-4626 | EVM | Tokenized vault shares — staking receipts, yield-bearing wrappers |
| ERC-1400 / ERC-3643 | EVM | Permissioned security/RWA tokens (built-in transfer restrictions, on-chain identity/eligibility) |
| SPL Token | Solana | High-throughput, low-fee fungible tokens |
| Native / Cosmos SDK | App-chains | Full sovereignty, custom logic |

> **Why ERC-3643 deserves a serious look for any permissioned or institutional-facing token**: institutional adoption accelerated sharply through 2024–2025 — the standard has been used to tokenize $32B+ in real-world assets across 180+ jurisdictions, with adopters including DTCC, Apex Group, Invesco, Franklin Templeton, and Fasanara Capital. ISO TC 307/68 is working to formalize it as a global standard. If compliance-gated transfers or institutional custody are in scope, treat ERC-3643 as the default comparison baseline, not a niche option.

### For Each Option Document:
- **Standard + chain** (e.g., ERC-20 on Base L2)
- **Fees & throughput** vs. expected transaction volume
- **Custody & wallet support** (MetaMask, hardware wallets, institutional custody like Fireblocks)
- **Compliance features** (can transfers be restricted/frozen if regulators require?)
- **Effort estimate** (contract dev, audit, integration)
- **Recommendation context** (when to pick this option)

---

## Stage 4: Ecosystem Component Mapping

Map the full ecosystem the token lives in. For each component, define scope (build / buy / integrate) and functional requirements.

```
                    ┌────────────────┐
                    │  Token (core)  │
                    │ mint/burn/tx   │
                    └───────┬────────┘
      ┌──────────┬──────────┼──────────┬────────────┐
      ▼          ▼          ▼          ▼            ▼
  ┌───────┐ ┌─────────┐ ┌────────┐ ┌─────────┐ ┌──────────┐
  │Wallet │ │Exchange │ │Staking │ │Governance│ │ Treasury │
  │custody│ │DEX/CEX  │ │rewards │ │ voting   │ │ multisig │
  └───────┘ └─────────┘ └────────┘ └─────────┘ └──────────┘
      │          │           │          │            │
  ┌───────────────────────────────────────────────────┐
  │  Shared services: KYC/AML, fiat on/off-ramp,      │
  │  oracles, analytics, block explorer, support      │
  └───────────────────────────────────────────────────┘
```

### Component Requirement Checklist

- **Wallet**: custodial vs. non-custodial, key recovery, supported platforms
- **Exchange/liquidity**: DEX pool seeding, CEX listing requirements, market-making agreements
- **Staking**: lock periods, reward source (emission vs. fees), slashing, unstaking queue
- **Governance**: proposal thresholds, quorum, voting mechanism (token-weighted, quadratic), timelock
- **Treasury**: multisig signers, spend policy, reporting cadence
- **Fiat ramps**: on-ramp partners, settlement currencies, chargeback handling
- **Oracles**: price feeds needed, provider (Chainlink, Pyth), failure fallback
- **Analytics & monitoring**: on-chain dashboards, whale alerts, supply audits

### 4.1 Governance Model — Current Best Practice (2025–2026)

Pure one-token-one-vote quorum is still the most common design (~60% of DAOs), but it's also the design most prone to voter apathy (thin quorums) or whale capture. Current practice layers mechanisms rather than picking one:

- **Tiered decision-making**: routine/operational decisions use fast token-voting + delegation + a modest quorum; high-stakes changes (treasury moves above a threshold, contract upgrades) require supermajority + a timelock, often with vote-escrow weighting.
- **Vote delegation**: let passive holders delegate to active delegates — this is the single highest-leverage fix for low turnout, and gives you named, accountable delegates to reference in the FS.
- **Vote-escrow (ve-model)**: longer lock-ups earn proportionally more voting weight, discouraging governance-attack-and-dump behavior and rewarding committed long-term holders.
- **Hybrid weighting**: combine token votes with reputation, quadratic weighting, or an expert-review committee for technical proposals — pure token-weight is rarely sufficient alone for anything safety-critical.
- **Governance minimization**: explicitly list which operational matters do *not* need a vote at all — every decision routed through governance is a liveness risk.

**FS requirement discipline**: document the exact quorum %, delegation mechanism, timelock duration, and which decision tier each governance action belongs to — "governance is token-weighted" is not a specifiable requirement on its own.

### 4.2 Treasury — Current Best Practice (2025–2026)

- **Multisig threshold**: 3-of-5 or higher for medium/large treasuries; multisig-controlled treasuries have shown dramatically fewer successful hacks than single-key wallets in industry incident data.
- **Signer hygiene**: rotate signers on a regular cadence (quarterly is a common baseline) and whenever a signer departs the organization — document the rotation policy in the FS, don't leave it as an informal practice.
- **Hardware-backed keys**: treasury signers should hold keys on hardware wallets (or HSM/MPC custody for institutional setups) as a non-negotiable baseline, never hot/browser-based keys.
- **Monitoring**: require real-time on-chain transaction alerting (e.g., a Safe{Wallet}-style transaction service plus a monitoring integration) as a functional requirement, not an afterthought — treasury moves should never be silent.
- **Tooling reference**: Safe (formerly Gnosis Safe) is the de facto standard self-custody multisig on Ethereum/EVM chains and is a reasonable default to name in the FS unless there's a reason to build custom.

---

## Stage 5: Compliance & Risk Analysis

This section is mandatory in every token FS.

### 5.1 Regulatory Classification

| Jurisdiction | Framework | Key Question |
|---|---|---|
| EU | MiCA | ART, EMT, or "other crypto-asset"? Whitepaper obligations? |
| US | SEC/CFTC joint framework (2026) + Howey test | Which of the 5 buckets does the token fall into — digital commodity, digital collectible, digital tool, payment stablecoin, or digital security? |
| US | FinCEN / CFTC | Money transmission? Commodity? |
| US | GENIUS Act (stablecoins) | If the token is fiat-referenced/stablecoin-like, does it need a qualified issuer structure and 1:1 reserves? |
| UK | FCA | Regulated security token vs. utility vs. e-money |
| Singapore | MAS PSA | Digital payment token service? |

Document the classification hypothesis and require legal sign-off as an explicit gate.

**Regulatory landscape is moving — treat these as current-state facts to verify, not permanent law:**

- **US**: in March 2026 the SEC and CFTC issued a joint interpretive framework sorting digital assets into five categories — *digital commodities*, *digital collectibles*, *digital tools*, *payment stablecoins*, and *digital securities* — with only the last requiring securities registration. The Howey analysis now weighs heavily on **how the issuer markets the token**: explicit, unambiguous promises of managerial effort and profit push a token toward "security"; a token that ships as working infrastructure with no such promises tends to fall outside it. Importantly, investment-contract status is **not permanent** — a token sold as part of an investment contract at launch does not automatically carry that status into secondary-market trading. **BA action**: write the marketing/whitepaper language review into the FS as an explicit gate alongside the legal classification — the promotional copy is now itself part of the compliance surface.
- **US stablecoins**: the GENIUS Act (enacted July 2025) created the first federal framework — only a bank subsidiary, a federal-qualified nonbank issuer, or a state-qualified issuer may issue a payment stablecoin; issuers must hold ≥$1 in permitted reserves per $1 issued, publish redemption procedures, certify AML/sanctions programs, and (above $50B outstanding) file audited annual financials. Interest payments to holders are prohibited. If your ecosystem includes a stablecoin leg, treat this as a hard gate, not a footnote.
- **EU MiCA**: from 23 December 2025, crypto-asset whitepapers must be filed in a **machine-readable format (XHTML with Inline XBRL)** — a PDF-only whitepaper no longer satisfies the filing requirement. Article 12 also creates an *ongoing* duty to keep the whitepaper accurate and current, not just accurate at filing. Utility tokens granting access to an already-functioning product/service remain exempt from the public-offer whitepaper regime (ARTs/EMTs are not).

### 5.2 KYC/AML Requirements

- Identity verification tiers (limits per tier)
- Sanctions screening (OFAC, EU lists) at onboarding and per transaction
- Travel Rule compliance for transfers above thresholds
- Transaction monitoring rules and SAR/STR escalation flow

**Travel Rule enforcement reality (2026)**: FATF Travel Rule legislation now exists in roughly 73% of assessed jurisdictions, but only about 40% actively enforce it — don't assume "the law exists" means "counterparties actually comply." Active enforcement is confirmed in 70+ jurisdictions including Canada, France, Germany, Hong Kong, Japan, Singapore, Switzerland, the UK, and the US (EU via the Transfer of Funds Regulation, US via FinCEN's recordkeeping rule, UK via MLR 2017). The standard threshold is USD/EUR 1,000 per transfer, requiring verified originator name + account/wallet identifier + address (or equivalent) and beneficiary name + account/wallet identifier. **BA action**: for any cross-border transfer flow, explicitly document which counterparty VASPs are confirmed to enforce the rule versus merely covered by legislation on paper — this materially affects your transaction-monitoring design.

### 5.3 Risk Register (minimum entries)

| Risk | Category | Mitigation |
|---|---|---|
| Access-control exploit | Technical | Role-based access control review, multisig/timelock on privileged functions, dedicated audit focus — this is currently the single largest exploit-loss category industry-wide |
| Oracle manipulation | Technical | Multi-source oracles, TWAP windows sized for real liquidity, verified fallback paths, circuit breakers — the largest exploit *value* category in recent industry data |
| Bridge compromise | Technical | Minimize custom bridge code; prefer audited, widely-used bridge infrastructure — bridges carry the highest dollar-loss per incident of any category |
| Smart contract exploit (general) | Technical | ≥2 independent audits, bug bounty, timelock on upgrades, continuous post-launch monitoring (not just a one-time pre-launch audit) |
| Regulatory reclassification | Legal | Transfer-restriction capability, legal opinions per jurisdiction, marketing/whitepaper language review (see 5.1) |
| Liquidity collapse | Market | Market-maker agreements, treasury liquidity policy |
| Key compromise | Operational | Multisig (3-of-5+), HSM/MPC custody, hardware wallets, signer rotation policy, key ceremony documentation |

**Why the ordering above**: industry incident data attributes access-control failures the largest documented single-category losses, with oracle manipulation the largest by exploit *value* and bridges the costliest *per incident*. Total sector losses to hacks/exploits reached record levels in 2025 and remained elevated into 2026 — treat "we got audited once before launch" as insufficient; budget for continuous monitoring alongside the pre-launch audit(s). Audit engagement cost bands to budget against: boutique ~$8k–25k, mid-tier ~$25k–80k, top-tier ~$80k–350k per scope, scaling with contract complexity and value at risk.

---

## Stage 6: Write the Functional Specification

Generate the FS in Markdown with these sections:

```markdown
# [Token Name] — Token & Ecosystem Functional Specification

## Executive Summary
## 1. Business Requirement Overview (problem, token rationale, success criteria/KPIs)
## 2. Tokenomics Specification (supply, allocation, vesting, utility loops)
## 3. Token Standard & Platform (chosen option + rejected alternatives with rationale)
## 4. Smart Contract Functional Requirements
   - FR table: ID, requirement, actor, acceptance criteria
   - Mint/burn/transfer rules, pausability, upgradeability, access control roles
## 5. Ecosystem Components (per-component requirements from Stage 4)
## 6. Compliance Requirements (classification, KYC/AML flows, reporting)
## 7. Integration & Data Requirements (oracles, ramps, custodians, APIs, events to index)
## 8. Security Requirements (audits, multisig policy, incident response)
## 9. Testing Strategy (unit, testnet, audit, simulation/economic testing, UAT)
## 10. Launch Plan Summary (TGE sequence — detail in Stage 7)
## 11. Validation Checklist
## 12. Risks & Mitigation
## 13. Appendices (glossary, addresses registry, change log)
```

**Smart contract FR format example:**

| ID | Requirement | Actor | Acceptance Criteria |
|---|---|---|---|
| FR-001 | Token contract SHALL cap total supply at 1B | System | Mint beyond cap reverts |
| FR-012 | 30% of collected fees SHALL be burned per epoch | Fee contract | Burn event emitted; supply decreases by exact amount |
| FR-020 | Transfers SHALL be blockable for sanctioned addresses | Compliance admin | Blocked address transfer reverts with reason |

---

## Stage 7: Launch & Lifecycle Roadmap

### Phase 1: Build & Audit (contract dev, internal review, 2 external audits, fixes, then transition to continuous monitoring rather than treating audit as a one-time gate)
### Phase 2: Testnet & Dry Run (full TGE rehearsal, vesting contract verification, integration tests with ramps/wallets)
### Phase 3: TGE — Token Generation Event
- Deploy sequence with verified addresses published
- Seed initial liquidity per treasury policy
- Activate vesting contracts; verify allocations against Tokenomics Sheet
- Enable monitoring/alerting before public announcement
### Phase 4: Ecosystem Rollout (staking launch, governance activation, exchange listings, incentive programs)
### Ongoing Operations
- Monthly supply/treasury transparency report
- Quarterly tokenomics review (are incentive loops working? KPI dashboard)
- Governance proposal pipeline management
- Regulatory watch (MiCA technical standards, SEC actions) → change requests

---

## Best Practices

1. **Every economic rule is a requirement** — if it's in the tokenomics sheet, it must have an FR ID and a test.
2. **Design for compliance optionality** — even utility tokens should support transfer restrictions; retrofitting is expensive.
3. **Separate token FS from ecosystem FS when large** — the token contract spec freezes at audit; ecosystem specs keep iterating.
4. **Immutability changes the review bar** — unlike classic software, deployed contracts can't be patched freely. The validation checklist and audits are the last gate.
5. **Model the economics, don't just describe them** — require a simulation (even a spreadsheet) of emissions vs. expected demand before sign-off.

## When to Use This Skill

✅ Launching a new token, writing tokenomics or smart contract requirements, planning TGE, defining wallet/staking/governance features, compliance analysis for crypto assets.

❌ Not for: trading strategy advice, price prediction, Solidity implementation details (dev skill), pure payment-gateway integrations without a token.

## A Note on Currency

Fintech/crypto regulation and market practice move fast. The regulatory specifics in Stage 5 (SEC/CFTC framework, MiCA whitepaper format, GENIUS Act, Travel Rule enforcement status), the ERC-3643 adoption figures in Stage 3, and the exploit/audit statistics in Stage 5.3 reflect research current as of **August 2026** — see `references/token-compliance-reference.md` for source links. Before relying on any specific figure, threshold, or legal conclusion in a real FS, verify it against a primary source or legal counsel; re-run the research pass periodically and update both this file and the reference file when it does.
