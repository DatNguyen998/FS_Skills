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

**ERC-3643 adoption update (2024–2025)**: institutional use accelerated sharply — $32B+ in real-world assets tokenized across 180+ jurisdictions, with adopters including DTCC (which committed to integrating it into its ComposerX tokenization platform after joining the ERC-3643 Association in March 2025), Apex Group, Invesco, Franklin Templeton, and Fasanara Capital. ISO TC 307, coordinating with ISO TC 68, has an active proposal to formalize it as a global standard, and it was cited by name in a July 2025 SEC speech. Treat it as the default comparison point for any permissioned/institutional token, not a niche choice.

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
- **Other crypto-assets** (incl. utility tokens): whitepaper notification regime; utility tokens granting access to an already-functioning product/service are exempt from the public-offer regime
- Key BA artifacts: crypto-asset whitepaper, complaint handling procedure, marketing communication rules
- **2026 update**: from 23 December 2025, whitepapers must be filed in **machine-readable format** — XHTML with Inline XBRL tagging per the Implementing Regulation. A PDF-only submission no longer satisfies the requirement. Article 12 imposes an *ongoing* duty to keep the published whitepaper accurate, complete, and up to date — treat whitepaper maintenance as a recurring compliance task, not a one-time filing.

### US
- **SEC/CFTC joint interpretive framework (March 2026)**: a 68-page release, with the CFTC agreeing to administer the Commodity Exchange Act consistently with it, sorts digital assets into **five buckets** — digital commodities, digital collectibles, digital tools, and payment stablecoins sit *outside* the securities definition; digital securities sit inside it.
- **Howey test** (still binding precedent, now refined): investment of money → common enterprise → expectation of profits → from efforts of others. The 2026 guidance weighs heavily on **marketing/promotional language** — explicit, unambiguous promises about managerial effort and profit generation push a token toward "security" status; a token that ships as functioning infrastructure without such claims tends to fall outside it. If none of the four Howey prongs are met → not a security under this test → assess against the 5-bucket taxonomy instead.
- **Investment-contract status is not perpetual**: a token sold via an investment contract at launch does not automatically drag that classification into secondary-market resales — re-assess at each material distribution event, don't assume launch-time classification is permanent.
- **GENIUS Act (stablecoins, enacted July 2025)**: first federal framework for payment stablecoins.
  - Permitted issuers: subsidiary of an insured depository institution, a federal-qualified nonbank issuer, or a state-qualified issuer.
  - Reserves: ≥$1 of permitted reserves per $1 issued.
  - Disclosure: published redemption procedures; periodic reports on outstanding stablecoins + reserve composition, executive-certified.
  - Issuers >$50B outstanding: audited annual financial statements required.
  - Interest payments to holders: **prohibited**.
  - AML/sanctions compliance program certification required.
- **FinCEN**: token issuers/exchangers may be Money Services Businesses → BSA program required.
- **State level**: NY BitLicense if serving NY residents.

### Other Key Jurisdictions
- **UK FCA**: security tokens (regulated), e-money tokens, unregulated utility — financial promotion rules apply to marketing
- **Singapore MAS**: Payment Services Act — Digital Payment Token licenses
- **UAE (VARA/ADGM)**, **Switzerland (FINMA)** common issuer domiciles — FINMA classifies payment / utility / asset tokens

### FATF Travel Rule — Enforcement Reality Check (2026)
- ~73% of assessed jurisdictions (85 of 117) have passed Travel Rule legislation; only ~40% actively enforce it — **legislation on paper ≠ enforcement in practice**.
- Confirmed active enforcement in 70+ jurisdictions, including Canada, France, Germany, Hong Kong, Japan, Singapore, Switzerland, the UK, and the US.
- Regional implementation: EU via the Transfer of Funds Regulation; US via FinCEN's recordkeeping rule; UK via the Money Laundering Regulations 2017.
- Standard threshold: USD/EUR 1,000 per transfer. Originator VASP must transmit verified name + account/wallet identifier + physical address (or equivalent alternative identifier); beneficiary data must include name + account/wallet identifier.
- **BA action**: for cross-border flows, document per-counterparty-VASP whether Travel Rule compliance is *confirmed enforced* vs. merely *legislated* — this changes your monitoring and counterparty-risk design.

## Governance Model Quick Reference (2025–2026 practice)

| Pattern | What it solves | Trade-off |
|---|---|---|
| Simple token-weighted quorum | Easiest to reason about; still the majority default (~60% of DAOs) | Thin-quorum risk; whale capture |
| Vote delegation | Passive-holder apathy → concentrates informed voting in active delegates | Delegate accountability must be designed in |
| Vote-escrow (ve-model) | Rewards long-term lock-up, discourages attack-and-dump | Reduces liquidity/flexibility for holders |
| Hybrid weighting (token + reputation/quadratic/committee) | Prevents pure-capital-weight domination of technical/safety decisions | More complex to specify and audit |
| Tiered decision-making | Routine ops move fast; high-stakes changes get supermajority + timelock | Requires an explicit, documented tier map |
| Governance minimization | Fewer votable decisions = fewer liveness/apathy failure points | Requires confidence in the non-voted default behavior |

## Treasury Multisig Checklist

- [ ] Threshold ≥3-of-5 for medium/large treasuries (higher for larger treasuries)
- [ ] All signers on hardware wallets (Ledger/Trezor) or HSM/MPC custody — no browser/hot-key signers
- [ ] Signer rotation policy documented (quarterly baseline, and immediately on signer departure)
- [ ] Real-time on-chain transaction monitoring/alerting wired up (e.g., Safe Transaction Service + Tenderly or equivalent)
- [ ] Named default tooling: Safe (formerly Gnosis Safe) is the de facto standard self-custody multisig on Ethereum/EVM chains
- [ ] Spend-policy thresholds documented per transaction size (what needs full multisig vs. a delegated sub-limit)

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
- [ ] Continuous post-launch monitoring in place — a pre-launch audit alone is treated as insufficient by current industry practice
- [ ] Access-control review is a named, dedicated audit focus area (see stats below)
- [ ] Oracle design reviewed for manipulation resistance: multi-source feeds, TWAP windows sized to real liquidity, verified fallback paths
- [ ] Any bridge component uses audited, widely-adopted infrastructure rather than custom bridge code where possible

### Exploit & Audit Market Data (2025–2026)

Context for sizing your security budget and risk register:

- Sector-wide crypto theft reached **$3.4B in 2025**, the worst year on record; H1 2026 recorded 207 hacking incidents (a record count) with ~$972M in losses.
- By vulnerability class, **access-control failures rank #1** in documented losses (OWASP 2026 Smart Contract Top 10, based on 2025 incident data — $953.2M+ attributed to this category alone).
- **Oracle manipulation** (low-liquidity TWAP windows, raw spot-price reads, unverified fallback paths) is the largest category **by exploit value** in recent industry incident data.
- **Bridges** carry the highest **dollar-loss per incident** of any component category — minimize custom bridge logic.
- Audit engagement cost bands (2026): boutique firms ~$8k–25k, mid-tier ~$25k–80k, top-tier ~$80k–350k per scope — budget according to contract complexity and value at risk, and plan for more than one engagement across the build lifecycle.

## Glossary

- **TGE**: Token Generation Event — first mint/distribution of the token
- **Vesting cliff**: period before any allocated tokens unlock
- **Liquidity pool**: paired token reserves enabling DEX trading
- **Multisig**: wallet requiring M-of-N signatures
- **Timelock**: enforced delay between an admin action's proposal and execution
- **Travel Rule**: FATF rule requiring originator/beneficiary info on VASP transfers
- **SAR/STR**: Suspicious Activity/Transaction Report filed with financial intelligence units
- **ve-model (vote-escrow)**: governance weighting where longer token lock-up periods earn greater voting power
- **RWA**: Real-World Asset — an off-chain asset (bond, fund share, real estate, etc.) represented on-chain via a token
- **TWAP**: Time-Weighted Average Price — a manipulation-resistant price-averaging method used by on-chain oracles

## Sources & Research Currency

This reference was last enriched from external research in **August 2026**. Figures, adoption stats, and regulatory descriptions above should be re-verified before use in a real FS — regulation and market data in this space change quickly. Primary sources consulted for this update:

- SEC/CFTC 2026 joint framework: [Orrick](https://www.orrick.com/en/Insights/2026/04/SEC-Issues-Interpretive-Guidance-on-Crypto-Asset-Classification), [WilmerHale](https://www.wilmerhale.com/en/insights/client-alerts/20260324-the-secs-new-framework-for-crypto-assets-under-howey), [Ballard Spahr](https://www.ballardspahr.com/insights/alerts-and-articles/2026/03/sec-and-cftc-clarify-when-digital-assets-are-and-are-not-securities), [Perkins Coie](https://perkinscoie.com/insights/update/sec-speaks-2026-five-key-takeaways)
- MiCA whitepaper format changes: [Hacken](https://hacken.io/discover/mica-regulation/), [InnReg](https://www.innreg.com/blog/mica-regulation-guide), [Lexology](https://www.lexology.com/library/detail.aspx?g=e39de72a-d572-482d-a2cc-99c21736307e), [LegalBison](https://legalbison.com/blog/mica-white-paper-requirements/)
- GENIUS Act: [Congress.gov CRS summary](https://www.congress.gov/crs-product/IN12553), [Paul Hastings](https://www.paulhastings.com/insights/crypto-policy-tracker/the-genius-act-a-comprehensive-guide-to-us-stablecoin-regulation), [Skadden](https://www.skadden.com/insights/publications/2025/07/us-establishes-first-federal-regulatory-framework), [US Treasury](https://home.treasury.gov/news/press-releases/sb0435)
- FATF Travel Rule 2026 status: [21Analytics](https://www.21analytics.co/blog/fatf-crypto-travel-rule-status-2026/), [InnReg](https://www.innreg.com/blog/crypto-travel-rule-guide), [Blockchain Council](https://www.blockchain-council.org/cryptocurrency/crypto-travel-rule-vasp-compliance-2026/)
- ERC-3643 adoption: [ERC3643 Association](https://www.erc3643.org/news/erc-3643-achieves-widespread-adoption-with-support-from-92-members), [Chainalysis](https://www.chainalysis.com/blog/introduction-to-erc-3643-ethereum-rwa-token-standard/), [Finextra](https://www.finextra.com/blogposting/31460/what-is-erc-3643-the-token-standard-powering-institutional-finance)
- Tokenomics design frameworks/trends: [Gate Wiki](https://www.gate.com/crypto-wiki/article/what-is-tokenomics-a-complete-guide-to-token-allocation-inflation-design-and-governance-utility-in-2026-20260204), [Frontiers in Blockchain](https://www.frontiersin.org/journals/blockchain/articles/10.3389/fbloc.2026.1758395/full), [Idea Usher](https://ideausher.com/blog/tokenomics-design/)
- DAO governance practice: [Blockchain Council](https://www.blockchain-council.org/dao/dao-governance-models-token-voting-reputation-systems-quadratic-voting/), [DAO Times](https://daotimes.com/understanding-the-advantages-and-disadvantages-of-dao-voting-schemes/), [LedgerMind](https://theledgermind.com/what-is-dao-governance/)
- Treasury multisig practices: [OnChain Treasury](https://onchaintreasury.org/2025/09/19/best-practices-for-multisig-wallets-in-dao-treasury-management/), [Request Finance](https://www.request.finance/crypto-treasury-management/dao-treasury-management), [TRES Finance](https://tres.finance/crypto-treasury-management-best-practices-for-financial-stability/)
- Exploit/audit market data: [CoinLaw](https://coinlaw.io/smart-contract-security-risks-and-audits-statistics/), [BlockEden](https://blockeden.xyz/blog/2026/01/17/smart-contract-audit-landscape-vulnerabilities-prevention-2026/), [Pharos Production](https://pharosproduction.com/insights/engineering/state-of-smart-contract-audits-2026/)
