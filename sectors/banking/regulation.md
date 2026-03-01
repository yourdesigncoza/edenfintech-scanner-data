# US Banking Regulatory Landscape

## Regulatory Bodies

The US employs a "dual banking system" (state vs federal charters) with overlapping jurisdictions.

| Regulator | Jurisdiction | Authority Type | Key Powers |
|-----------|-------------|---------------|------------|
| **Federal Reserve (FRB)** | Bank Holding Companies, State-Chartered Member Banks, Foreign Banks in US | Prudential Supervisor & Central Bank | Stress tests (CCAR), capital/liquidity requirements, M&A approval, lender of last resort (Discount Window) |
| **OCC** | National Banks (Federal Charter), Federal Savings Associations | Primary Chartering Authority (rules-based + discretionary) | Grants/revokes national charters, on-site examinations, enforcement actions (MRA/MRIA), preemption of state laws |
| **FDIC** | State-Chartered Non-Member Banks; insures deposits at ALL banks | Resolution & Insurance (highly discretionary in crisis) | Manages Deposit Insurance Fund (DIF), resolution authority (receivership) for failed banks, backup exam authority |
| **CFPB** | All banks >$10B assets (consumer protection) | Consumer Protection (discretionary) | Enforces consumer laws (TILA, RESPA), polices UDAAP (Unfair, Deceptive, or Abusive Acts or Practices) |
| **State Banking Depts** | State-Chartered Banks | State Chartering Authority | Charters state banks, enforces state usury/lending laws, examines state-licensed branches |
| **SEC** | Publicly Traded Bank Holding Companies | Securities Market Regulator (rules-based) | Disclosure/reporting (10-K/Q), insider trading, accounting standards (via FASB/GAAP oversight) |

**Discretion assessment:** HIGH to EXTREME. While capital requirements (CET1 ratios) are rigid and rules-based, the regulatory *response* to distress is highly discretionary and political. Whether a bank receives a "Systemic Risk Exception" (bailout of uninsured depositors) vs standard failure (equity wipeout) is a subjective real-time decision.

## Key Frameworks

### Dodd-Frank Act (2010)
- **Systemic Risk:** Created FSOC (Financial Stability Oversight Council) to designate SIFIs
- **Resolution Plans ("Living Wills"):** Banks must detail how they can be dismantled without public bailouts
- **Orderly Liquidation Authority (OLA):** FDIC power to unwind failing systemically important companies
- **Volcker Rule:** Prohibits proprietary trading; limits hedge fund/PE fund ownership

### Basel III / Basel III Endgame
- **Current:** Focuses on quality of capital (CET1) and risk-weighted assets (RWA)
- **Endgame (upcoming):** Replaces internal risk models with standardized approaches for credit, operational, and market risk. Proposes removing the AOCI opt-out for banks >$100B (forcing mark-to-market of unrealized bond losses)

### The "Tailoring Rule" (Category I-IV Framework)

Regulatory burden scales by asset size and risk profile:

| Category | Asset Size | Key Requirements | Example Banks |
|----------|-----------|-----------------|---------------|
| **I (G-SIBs)** | $700B+ or significant cross-jurisdictional | Full LCR, NSFR, eSLR, G-SIB surcharge, annual CCAR | JPM, BAC, C, WFC, GS, MS |
| **II** | $700B+ or cross-jurisdictional | Full LCR/NSFR, stress testing | BNY, State Street |
| **III** | $250B-$700B | LCR/NSFR (often 85% calibration), biennial stress test | USB, PNC, TFC, COF |
| **IV** | $100B-$250B | Historically lighter (no LCR, AOCI opt-out), now heavily scrutinized post-2023 | FITB, RF, KEY, CFG, MTB |
| **<$100B** | Under $100B | Lightest touch; no stress test requirement | Most regional banks |

### Bank Secrecy Act (BSA) / AML
- KYC (Know Your Customer), CIP (Customer Identification Program), SAR filing
- **Critical:** Failure is now a kill-level event — see TD Bank 2024 ($3B fine + asset cap)

### Community Reinvestment Act (CRA)
- Banks must meet credit needs of LMI communities
- Failure blocks M&A applications and branch expansion

### Stress Testing: DFAST & CCAR
- **DFAST:** Quantitative test — capital adequacy under "Severely Adverse" scenarios
- **CCAR:** For larger banks — DFAST + qualitative assessment of capital planning. Failing CCAR blocks buybacks and dividends
- **Stress Capital Buffer (SCB):** Variable buffer determined by DFAST losses, added to minimums (2.5% floor)

## Capital Adequacy Requirements

| Requirement | Minimum | Well-Capitalized | G-SIB Addition | Notes |
|------------|---------|-----------------|----------------|-------|
| **CET1 Ratio** | 4.5% | 6.5% | +1.0% to +4.5% | Highest-quality capital / RWA |
| **Tier 1 Capital Ratio** | 6.0% | 8.0% | — | (CET1 + Additional Tier 1) / RWA |
| **Total Capital Ratio** | 8.0% | 10.0% | — | (Tier 1 + Tier 2) / RWA |
| **Tier 1 Leverage Ratio** | 4.0% | 5.0% | — | Tier 1 / Total Average Assets (no risk weighting) |
| **Supplementary Leverage Ratio (SLR)** | 3.0% | 5.0% (G-SIBs) | — | Includes off-balance sheet exposures |
| **Stress Capital Buffer** | 2.5% floor | Variable | — | Set by DFAST results, added to CET1 minimum |
| **Countercyclical Buffer** | 0% (currently) | Up to 2.5% | — | Fed discretion, never activated in US |

**To pay dividends/buybacks:** Bank must maintain Minimums + SCB + G-SIB Surcharge (if applicable) + CCyB.

**Prompt Corrective Action (PCA) triggers:** Banks breaching "Critically Undercapitalized" (<2% tangible equity/assets) face mandatory FDIC seizure.

## Enforcement Precedents (Last 10 Years)

| Date | Bank | Regulator | Action | Outcome/Impact |
|------|------|-----------|--------|----------------|
| Oct 2024 | **TD Bank** | DOJ / OCC / Fed | **Asset Cap** + $3B fine | Severe AML failures. US retail growth frozen indefinitely. |
| Jan 2024 | **NYCB** | OCC / FDIC (indirect) | Unofficial pressure / disclosure | Stock -40% in one day on unexpected CRE reserve builds and dividend cut. Required emergency $1B equity raise (Mnuchin consortium). |
| Mar 2023 | **Silicon Valley Bank** | CA DFPI / FDIC | **Seizure** | Equity wiped. $209B bank failed in 48 hours. Systemic Risk Exception invoked for uninsured depositors. |
| Mar 2023 | **Signature Bank** | NY DFS / FDIC | **Seizure** | Equity wiped. "Crisis of confidence" + crypto exposure. Systemic Risk Exception invoked. |
| May 2023 | **First Republic Bank** | CA DFPI / FDIC | **Seizure** | Equity wiped. Sold to JPMorgan. $229B in assets. |
| Oct 2020 | **Citigroup** | Fed / OCC | Consent Order + $400M fine | Required massive overhaul of data governance and risk management. Still constraining operations years later. |
| Feb 2018 | **Wells Fargo** | Fed | **Asset Cap** | Restricted from growing assets beyond end-2017 levels. Cap lasted 7+ years (removed June 2025). Estimated $4B+ in forgone profits. |
| 2016 | **Wells Fargo** | OCC / CFPB | Consent Orders + $185M fine | Fake accounts scandal. 14 simultaneous consent orders. CEO forced out. |

## Binary Regulatory Risks

Events where regulatory action alone can destroy >50% of equity value:

1. **FDIC Receivership** — Capital ratios breach "Critically Undercapitalized" OR inability to meet liquidity demands. Equity zeroed immediately. (SVB, Signature, First Republic 2023)

2. **Asset Cap Imposition** — Systemic/repeated failure of risk management. Bank cannot grow balance sheet, permanently compressing ROE. (Wells Fargo 2018-2025, TD Bank 2024)

3. **CRE Concentration MRIA** — CRE concentration >300% of capital with weak risk management. Regulators force loan sales or dilutive equity raises, triggering confidence spiral. (NYCB 2024)

4. **Criminal Indictment of Entity** — Massive money laundering or sanctions evasion. Potential loss of charter or dollar clearing capability. (Rare — usually resolved via DPA)

5. **$100B Asset Cliff** — Crossing $100B triggers Category IV requirements (enhanced capital scrutiny, potential AOCI inclusion, resolution planning). NYCB crossed $100B via Signature Bank acquisition, was forced to build CRE reserves, cut dividend 70%, stock fell 38% in one day (Jan 2024). Any regional approaching $100B faces this binary regulatory step-function.

6. **BaaS/Fintech Consent Orders** — Banks acting as middleware for fintechs face AML/KYC scrutiny. Consent orders can force exit from entire business lines. Blue Ridge Bank (Jan 2024): OCC consent order for unsafe practices in BaaS division, forced to exit fintech partnerships entirely.

7. **Stress Test Failure** — CCAR failure blocks dividends/buybacks, signals capital inadequacy to market. Can trigger depositor/investor flight. (Deutsche Bank US, Santander US 2014-2016)

## Upcoming Changes (2025-2027)

### Basel III Endgame (US Implementation)
- **Status:** Proposed July 2023, massive industry backlash. Fed Vice Chair Barr signaled re-proposal (likely watered down) in 2024/2025
- **Key change:** Extension of AOCI recognition to banks >$100B (reversing Category IV opt-out). Forces mark-to-market of unrealized securities losses
- **Impact:** Higher capital requirements for trading activities and operational risk

### Long-Term Debt (LTD) Requirement
- Regional Banks ($100B+) would need to issue LTD equal to ~3.5-6% of assets
- Creates "bail-in" buffer so bondholders absorb losses before FDIC DIF
- **Impact:** Increases cost of funds for regionals (replacing cheap deposits with expensive bonds)

### Liquidity Coverage Ratio (LCR) Recalibration
- Post-SVB: reassessing deposit outflow assumptions
- Uninsured deposits and digital-banking deposits likely treated as "hotter" (faster run speed)
- Requires banks to hold more HQLA (High-Quality Liquid Assets)

### FDIC Special Assessments
- Banks currently paying recoupment fees to refill DIF after SVB/Signature payouts
- Largest banks bear disproportionate share (~$16.3B total assessment)

### CRE Concentration Guidance
- Heightened scrutiny of banks with CRE >300% of total capital or construction >100%
- Likely formal guidance tightening in 2025-2026 given office sector stress

## Evidence Sources

Where to monitor regulatory developments:

| Source | URL | What to Monitor |
|--------|-----|----------------|
| Federal Register | federalregister.gov | Notices of Proposed Rulemaking (NPRM) |
| Fed SR Letters | federalreserve.gov/supervisionreg/srletters/ | Supervisory guidance and policy changes |
| FDIC FILs | fdic.gov/news/financial-institution-letters | Insurance, resolution, and safety guidance |
| OCC Bulletins | occ.gov/news-issuances/bulletins/ | Examination procedures and risk guidance |
| FFIEC | ffiec.gov | Call Report data (UBPR), interagency guidance |
| Fed Enforcement Actions | federalreserve.gov/supervisionreg/enforcement-actions.htm | Consent orders, cease-and-desist, CMPs |
| FDIC Enforcement | fdic.gov/bank-examinations/enforcement | FDIC-specific enforcement actions |
| OCC Enforcement | occ.gov/topics/laws-and-regulations/enforcement-actions/ | OCC-specific enforcement actions |
| Davis Polk / Sullivan & Cromwell | Law firm regulatory trackers | Plain-English summaries of complex rules |
