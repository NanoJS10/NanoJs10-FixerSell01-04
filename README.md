# NanoJS-FixerSell01 — FIXER COIN ($FIXER) Rugpull Detection

> ** RESOLVED — 2026-06-26:** GitHub Trust & Safety confirmed ToS violations and took action against the fixerco account. The presale page and project site are confirmed down (404). Investigation closed successfully.

---

## Case Update — 2026-06-26

### GitHub Takedown Confirmed

Two days after this investigation was published, GitHub Trust & Safety responded to the abuse report and confirmed action had been taken against the fixerco account.

### Evidence 07 GitHub Trust & Safety Confirmation Email
![GitHub Takedown Email](evidence/07_github_takedown_email.jpg)

### Evidence 08 github.com/fixerco Returns 404 (Account Suspended)
![Account 404](evidence/08_fixerco_account_404.jpg)

### Evidence 09 — fixerco.github.io/PresaleFIXERCOIN/ Returns 404 (Presale Down)
![Presale 404](evidence/09_presale_page_404.jpg)

### Evidence 10  fixerco.github.io/Fixer-Coin/ Returns 404 (Project Site Down)
![Project Site 404](evidence/10_fixer_coin_site_404.jpg)

**All three URLs confirmed down:**
| URL | Status |
|-----|--------|
| github.com/fixerco | 404 — Account suspended |
| fixerco.github.io/PresaleFIXERCOIN/ |  404 — Presale page down |
| fixerco.github.io/Fixer-Coin/ |  404 — Project site down |

**Timeline of action:**
| Date | Event |
|------|-------|
| 2026-06-24 | Investigation published. GitHub abuse report filed. |
| 2026-06-26 | GitHub Trust & Safety confirms ToS violations. Action taken. |
| 2026-06-26 | All 3 fixerco URLs return 404 — account and pages confirmed removed. |

> Report filed 2026-06-24. Takedown confirmed 2026-06-26. 48 hours from detection to full removal.

---

## ACTIVE FRAUD WARNING

This investigation was published on **2026-06-24** while the FIXER COIN presale was live and collecting investor funds. If you found this page after being recruited into the Fixer Coin Telegram or presale — **read this before sending any money.**

---

## Case Summary

| Field | Detail |
|-------|--------|
| **Case ID** | NanoJS-FixerSell01 |
| **Investigator** | NanoJS10 |
| **Detection Date** | 2026-06-24, 09:50 UTC |
| **Chain** | Ethereum Mainnet (Base Network claimed by project) |
| **Risk Level** | CRITICAL — Active presale, confirmed rugpull mechanics |
| **Status** |  GitHub pages taken down — 2026-06-26 |

---

##  What I Found

On the morning of **2026-06-24 at 09:50 UTC**, my on-chain monitoring flagged a wallet deploying three smart contracts named **FixerSellRouter** across three consecutive Ethereum blocks in under 13 minutes.

The deployer wallet had **never been used before** age of 0.0 hours at the time of deployment, with only 4 transactions total. This is not how legitimate projects deploy contracts. This is how people who do not want to be found deploy contracts.

Investigation confirmed the contracts belong to **FIXER COIN ($FIXER)**, a memecoin project running an active presale with 261 Telegram subscribers being recruited through a referral commission system while the contract gives the owner complete power to prevent every investor from ever selling their tokens.

---

## On-Chain Evidence

### Deployer Wallet
```
0x97127e96ed3af0f7194d5236984790b27ec685f2
```
- Wallet age at deployment: **0.0 hours** ← CRITICAL
- Total transactions: **4**
- ETH balance: **0** (fully spent on gas)
- Funded **20 days prior**, left dormant, activated for scripted deployment

### Deployment Timeline

| Block | Date/Time (UTC) | Action |
|-------|----------------|--------|
| 25242830 | 2026-06-04 08:27 | Funded with 0.00320811 ETH |
| 25387511 | 2026-06-24 12:36:11 | Contract Creation #1 |
| 25387512 | 2026-06-24 12:36:23 | **Create: FixerSellRouter** |
| 25387577 | 2026-06-24 12:49:35 | Contract Creation #3 |

**3 contracts deployed in 13 minutes 24 seconds — automated scripted deployment.**

### Funder Wallet
```
0x96a7C808e90b14c3d12e638aaBCAB6e12525345C
```
- ETH balance: 17.24 ETH (~$28,342)
- Total portfolio: **$101,123** multichain
- Token holdings: **>202 tokens** ($72,780)
- Total transactions: **14,896**
- Active for **348 days**
- Funded only **1 downstream wallet** the deployer

> Despite 14,896 transactions and $101k in holdings, this wallet funded only one address. That asymmetry is the tell.

### Funding Chain

```
0xC42b1785...0A433fb7D   ← Origin (348 days ago, unresolved)
        |
        ↓ funded
0x96a7C808...12525345C   ← Active trader ($101k, 14,896 txs)
        |
        ↓ funded (20-day dormancy)
0x97127e96...27ec685F2   ← Deployer (0.0h age, throwaway)
        |
   +----+----+
   |         |         |
Contract   FixerSellRouter   Contract
  #1       (named)            #3
```

---

## Contract Analysis

**Source file:** `FIXER COIN.sol`
**Contract name:** `FixerSellRouter`
**Verification:** Similar Match — `0x8a81E167...870319832`
**Compiler:** Solidity v0.8.34
**Dependencies:** OpenZeppelin ERC20, SafeERC20, Ownable

### Dangerous Owner Functions

| Severity | Function | What It Actually Does |
|----------|----------|-----------------------|
| CRITICAL | **BLACKLIST** | Owner can freeze any wallet investors cannot sell |
|  HIGH | **DYNAMIC FEES (0–50%)** | Owner drains up to half of every transaction |
|  HIGH | **SET FEE WALLET** | Owner redirects all fees to any address, no notice |
| HIGH | **SET AMM PAIR** | Owner swaps out the liquidity pool |
| MEDIUM | **SET TIER** | Owner manually controls price tiers |
| MEDIUM | **EMERGENCY WITHDRAW** | Owner recovers non-FIXER tokens from contract |

**The blacklist function is the primary exit mechanism.** Once retail investors hold tokens, the owner blacklists all non-owner wallets, preventing sales. The owner then dumps their allocation.

---

## Social Media Evidence

| Platform | Link | Status |
|----------|------|--------|
| Telegram | t.me/FixerCoin_Org | Active — 261 subscribers at detection |
| Twitter/X | x.com/FixerCoin | Active |
| Website | fixerco.github.io/Fixer-Coin/ |  **TAKEN DOWN — 404** |
| Presale | fixerco.github.io/PresaleFIXERCOIN/ |  **TAKEN DOWN — 404** |
| GitHub Account | github.com/fixerco |  **SUSPENDED — 404** |

### Grooming Language Identified

- *"Please refrain from requesting any compensation before you begin your contributions"*
- *"Commitment and loyalty will be rewarded in the future"*
- *"Our team actively monitors all contributions"*
- *"5% commission via your referral link"*
- *"Will operate exclusively on DEXes"*

---

## Evidence Screenshots

### Evidence 01 Contract Overview (Zero ETH, Creator confirmed)
![Contract Overview](evidence/01_contract_overview.jpg)

### Evidence 02  Funder Wallet ($101,123 portfolio, 348 days active)
![Funder Wallet](evidence/02_funder_wallet.jpg)

### Evidence 03  Deployer Transaction History (4 txs, scripted deployment)
![Deployer Transactions](evidence/03_deployer_transactions.jpg)

### Evidence 04  Telegram Grooming Language (presale recruitment)
![Telegram Grooming](evidence/04_telegram_grooming.jpg)

### Evidence 05  Telegram Owner Powers Diagram (blacklist, fees confirmed)
![Telegram Owner Powers](evidence/05_telegram_owner_powers.jpg)

### Evidence 06  Contract Source: FIXER COIN.sol (identity confirmed)
![Contract Source](evidence/06_contract_source_fixercoin.jpg)

### Evidence 07 GitHub Trust & Safety Takedown Confirmation
![GitHub Takedown](evidence/07_github_takedown_email.jpg)

### Evidence 08  fixerco.github.io Returns 404 (Confirmed Down)
![404 Confirmed](evidence/08_fixerco_404_confirmed.jpg)

---

## Modus Operandi

| Phase | Action |
|-------|--------|
| **Phase 1** | Establish 3-wallet funding chain over 348 days |
| **Phase 2** | Fund throwaway deployer wallet 20 days before activation |
| **Phase 3** | Deploy 3 FixerSellRouter contracts via automated script |
| **Phase 4** | Build Telegram community (261 subscribers) via referral commissions |
| **Phase 5** | Run presale on DEX — collect investor funds |
| **Phase 6** | Trigger blacklist or max fees — dump owner tokens — disappear |

---

## Reports Filed & Outcomes

| Platform | Report | Outcome |
|----------|--------|---------|
| Etherscan | Deployer wallet flagged | Filed — pending label |
| Etherscan | Funder wallet flagged | Filed — pending label |
| Base / HackerOne | Fraud report submitted | Filed — under review |
| Base Discord | Security alert posted | Filed |
| GitHub Abuse | Presale page reported | **Confirmed action taken — 2026-06-26** |

---

## Full Investigation Timeline

| Time (UTC) | Event |
|------------|-------|
| 09:50, 2026-06-24 | On-chain monitoring detects FixerSellRouter deployment |
| 10:07 | Manual Etherscan investigation — deployer confirmed 0.0h age |
| 10:22 | Funder wallet traced — $101k portfolio, 1 downstream target |
| ~10:35 | Contract source confirmed as FIXER COIN.sol |
| ~16:35 | Telegram located — 261 subscribers, active presale confirmed |
| ~16:50 | Grooming language documented. Chain discrepancy noted. |
| Same day | All platform reports filed. Repository published. |
| 2026-06-26 | GitHub Trust & Safety confirms ToS violation. Action taken. |
| 2026-06-26 | fixerco.github.io returns 404 — presale page confirmed down. |

---

## If You Are in the Fixer Coin Telegram

The presale page is now down. If you have already sent funds, document everything — wallet addresses, transaction hashes, amounts — for any future law enforcement report.

Do not send further funds. Do not recruit friends.

---

## Key Addresses

```
Deployer:  0x97127e96ed3af0f7194d5236984790b27ec685f2
Funder:    0x96a7C808e90b14c3d12e638aaBCAB6e12525345C
Origin:    0xC42b1785...0A433fb7D (under investigation)
```

---

## About NanoJS Investigations

NanoJS Investigations is an independent blockchain forensic operation. All investigations are conducted using publicly available on-chain data and open-source tools. No financial compensation is received prior to disclosure.

**GitHub:** github.com/NanoJS10

> *"Data on the blockchain is permanent — analysis makes it powerful."*

---

*Published: 2026-06-24 | Updated: 2026-06-26 | Case: NanoJS-FixerSell01 | Chain: Ethereum Mainnet*
