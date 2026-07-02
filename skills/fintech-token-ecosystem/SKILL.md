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

---

## Stage 3: Token Standard & Platform Selection

Present 2–3 platform/standard options with pros/cons (mirror the approach-comparison discipline of a classic FS):

### Common Standards Reference

| Standard | Chain | Use Case |
|---|---|---|
| ERC-20 | Ethereum/EVM L2s | Fungible utility/payment tokens |
| ERC-721 / ERC-1155 | EVM | NFTs, semi-fungible assets |
| ERC-1400 / ERC-3643 | EVM | Permissioned security tokens (built-in transfer restrictions) |
| SPL Token | Solana | High-throughput, low-fee fungible tokens |
| Native / Cosmos SDK | App-chains | Full sovereignty, custom logic |

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

---

## Stage 5: Compliance & Risk Analysis

This section is mandatory in every token FS.

### 5.1 Regulatory Classification

| Jurisdiction | Framework | Key Question |
|---|---|---|
| EU | MiCA | ART, EMT, or "other crypto-asset"? Whitepaper obligations? |
| US | SEC / Howey test | Investment of money in a common enterprise with expectation of profit from others' efforts? |
| US | FinCEN / CFTC | Money transmission? Commodity? |
| UK | FCA | Regulated security token vs. utility vs. e-money |
| Singapore | MAS PSA | Digital payment token service? |

Document the classification hypothesis and require legal sign-off as an explicit gate.

### 5.2 KYC/AML Requirements

- Identity verification tiers (limits per tier)
- Sanctions screening (OFAC, EU lists) at onboarding and per transaction
- Travel Rule compliance for transfers above thresholds
- Transaction monitoring rules and SAR/STR escalation flow

### 5.3 Risk Register (minimum entries)

| Risk | Category | Mitigation |
|---|---|---|
| Smart contract exploit | Technical | ≥2 independent audits, bug bounty, timelock on upgrades |
| Regulatory reclassification | Legal | Transfer-restriction capability, legal opinions per jurisdiction |
| Liquidity collapse | Market | Market-maker agreements, treasury liquidity policy |
| Key compromise | Operational | Multisig, HSM/MPC custody, key ceremony documentation |
| Oracle manipulation | Technical | Multi-source oracles, circuit breakers |

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

### Phase 1: Build & Audit (contract dev, internal review, 2 external audits, fixes)
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
