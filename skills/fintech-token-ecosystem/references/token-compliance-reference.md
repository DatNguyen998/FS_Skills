# Token Standards & Compliance Quick Reference

Companion reference for the `fintech-token-ecosystem` skill.

## Token Standards Cheat Sheet

| Standard | Chain family | Fungibility | Built-in compliance | Typical use |
|---|---|---|---|---|
| ERC-20 | EVM | Fungible | None (add via extensions) | Utility, payment, governance tokens |
| ERC-721 | EVM | Non-fungible | None | Unique assets, credentials |
| ERC-1155 | EVM | Mixed | None | Gaming, batch assets |
| ERC-4626 | EVM | Fungible (vault shares) | None | Yield vaults, staking receipts |
| ERC-1400 | EVM | Fungible (partitioned) | Transfer restrictions, document refs | Security tokens |
| ERC-3643 (T-REX) | EVM | Fungible | On-chain identity + eligibility checks | Regulated/permissioned tokens |
| SPL Token / Token-2022 | Solana | Fungible & NFT | Token-2022: transfer hooks, confidential transfers | High-throughput consumer apps |
| Cosmos SDK native | Cosmos app-chains | Configurable | Custom modules | Sovereign app-chains |

### Useful ERC-20 Extensions (OpenZeppelin)
- `ERC20Burnable` — holder-initiated burns
- `ERC20Pausable` — emergency stop for transfers
- `ERC20Votes` — checkpointed voting power for governance
- `ERC20Permit` (EIP-2612) — gasless approvals
- `AccessControl` — role-based mint/pause/blocklist admin

## Regulatory Frameworks Overview

### EU — MiCA (Markets in Crypto-Assets)
- **ART** (Asset-Referenced Token): references a basket of assets → heaviest regime
- **EMT** (E-Money Token): references a single fiat currency → e-money-like regime
- **Other crypto-assets** (incl. utility tokens): whitepaper notification regime
- Key BA artifacts: crypto-asset whitepaper, complaint handling procedure, marketing communication rules

### US
- **Howey test** (SEC): investment of money → common enterprise → expectation of profits → from efforts of others. If all four met → security → registration or exemption (Reg D, Reg S, Reg A+)
- **FinCEN**: token issuers/exchangers may be Money Services Businesses → BSA program required
- **State level**: NY BitLicense if serving NY residents

### Other Key Jurisdictions
- **UK FCA**: security tokens (regulated), e-money tokens, unregulated utility — financial promotion rules apply to marketing
- **Singapore MAS**: Payment Services Act — Digital Payment Token licenses
- **UAE (VARA/ADGM)**, **Switzerland (FINMA)** common issuer domiciles — FINMA classifies payment / utility / asset tokens

## KYC/AML Functional Requirements Starter Set

| ID | Requirement |
|---|---|
| AML-001 | Users SHALL complete identity verification before fiat on-ramp or token purchase |
| AML-002 | System SHALL screen users against sanctions lists (OFAC SDN, EU consolidated) at onboarding and daily |
| AML-003 | Transfers above the Travel Rule threshold SHALL include required originator/beneficiary data (via TRISA/Notabene or equivalent) |
| AML-004 | System SHALL apply risk-based transaction monitoring rules and queue alerts for compliance review |
| AML-005 | Compliance officer SHALL be able to freeze ecosystem-service access for flagged accounts (and token transfers if permissioned standard) |
| AML-006 | System SHALL retain KYC records ≥5 years after relationship end (jurisdiction-dependent) |

## Audit & Security Checklist

- [ ] ≥2 independent smart contract audits (e.g., Trail of Bits, OpenZeppelin, Certora)
- [ ] All findings resolved or risk-accepted with sign-off
- [ ] Bug bounty live before mainnet (Immunefi or similar)
- [ ] Admin functions behind multisig (≥3-of-5) + timelock
- [ ] Upgradeability decision documented (immutable vs. proxy; if proxy — who controls, what delay)
- [ ] Deployment addresses published and verified on block explorer
- [ ] Incident response runbook: pause criteria, comms plan, post-mortem template

## Glossary

- **TGE**: Token Generation Event — first mint/distribution of the token
- **Vesting cliff**: period before any allocated tokens unlock
- **Liquidity pool**: paired token reserves enabling DEX trading
- **Multisig**: wallet requiring M-of-N signatures
- **Timelock**: enforced delay between an admin action's proposal and execution
- **Travel Rule**: FATF rule requiring originator/beneficiary info on VASP transfers
- **SAR/STR**: Suspicious Activity/Transaction Report filed with financial intelligence units
