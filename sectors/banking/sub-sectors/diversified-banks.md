---
sector: Financials
industry_group: Banks
industry: Banks
fmp_industry: "Banks - Diversified"
gics_code: "40101010"
hydrated: 2026-03-01
version: 1
epistemic_stability: 3
suggested_pcs_friction: -1
typical_valuation: "P/TBV regression vs ROATCE"
fcf_multiple_baseline: "N/A — banks use P/TBV and P/E, not FCF multiples"
---

# Diversified Banks

## Overview

Diversified banks are large, geographically diverse financial institutions whose revenues derive from conventional banking operations (retail banking, corporate/commercial lending) supplemented by investment banking, trading, wealth management, and transaction services. The "Big Four" -- JPMorgan Chase, Bank of America, Wells Fargo, and Citigroup -- each hold over $1.7 trillion in consolidated assets and are classified as Global Systemically Important Banks (G-SIBs), subject to enhanced prudential standards.

Revenue splits typically run 50-65% net interest income (NII) and 35-50% non-interest income (fees, trading, advisory, wealth management). JPMorgan generates roughly half its income from retail/commercial banking and a third from CIB; Goldman Sachs and Morgan Stanley skew heavily toward investment banking and trading. Wells Fargo is the most domestically focused (95%+ US revenue). Capital intensity is extreme -- banks operate with 10-12x leverage, and return on assets (ROA) of 0.8-1.5% translates to ROE of 10-15% through this leverage. The business is inherently cyclical, with credit losses and NII both moving with interest rates and the economic cycle.

Barriers to entry are formidable: bank charters, regulatory approval, capital requirements, deposit insurance, technology infrastructure, and brand trust create an effective oligopoly among the largest institutions. Switching costs for commercial relationships are high; retail switching costs are moderate but increasing with digital integration.

## Key Metrics & KPIs

| Metric | What It Measures | Healthy Range | Red Flag |
|--------|-----------------|---------------|----------|
| CET1 Ratio | Highest-quality capital vs risk-weighted assets | >10% (regulatory min 4.5% + buffers ~7%) | <8% or declining trend |
| Tier 1 Leverage Ratio | Tier 1 capital vs total assets (non-risk-weighted) | >6% (well-capitalized = 5%) | <5% |
| Return on Equity (ROE) | Profitability relative to shareholder equity | 10-15% (excellent >15%) | <8% sustained or below cost of equity (~10%) |
| Return on Assets (ROA) | Profitability relative to total assets | 0.8-1.5% (excellent >1.2%) | <0.5% |
| Net Interest Margin (NIM) | Spread between lending and funding rates | 2.0-3.0% for large banks | <1.8% or compressing >50bps YoY |
| Efficiency Ratio | Noninterest expense / (NII + noninterest income) | 50-60% for large banks (lower = better) | >65% sustained |
| NPL Ratio | Non-performing loans / total loans | <1.5% | >3% or rising rapidly |
| Net Charge-Off Ratio | Actual loan losses / average loans | 0.3-0.8% through-cycle | >1.5% or spiking |
| Texas Ratio | (NPLs + REO) / (tangible equity + loan loss reserves) | <25% | >50% (>100% = failure risk) |
| Loan-to-Deposit Ratio | Total loans / total deposits | 70-90% | >100% (funding stress) or <60% (underearning) |
| Tangible Book Value per Share | Net tangible assets per share | Growing 5-10% annually | Declining or stagnant |
| Dividend Payout Ratio | Dividends / net income | 25-40% | >60% (unsustainable) or 0% (capital distress) |
| Supplementary Leverage Ratio (SLR) | Tier 1 capital / total leverage exposure | >5% for G-SIBs | <3.5% |
| Provision for Credit Losses (PCL) | Quarterly reserve build/release | Stable or declining | Sudden large build (signals deteriorating loan book) |
| Non-Interest Income Mix | Fee/trading income as % of total revenue | 35-50% for diversified | <25% (NII-dependent, rate-sensitive) |

## Valuation Approach

- **Primary method:** Price-to-Tangible Book Value (P/TBV), regressed against forward Return on Average Tangible Common Equity (ROATCE). A bank earning its cost of equity (~10%) trades at ~1.0x TBV; each 1% ROE above COE adds roughly 0.15-0.20x to the justified multiple.
- **Secondary method:** Price-to-Earnings (P/E) on normalized earnings. Use 10-12x for banks earning cost of equity, 12-15x for banks earning above cost of equity sustainably.
- **Why NOT FCF multiples:** Bank "free cash flow" is meaningless -- lending IS the business. Capital adequacy requirements constrain distributions, and "cash flow from operations" includes loan originations/repayments that dwarf operating income. Use earnings-based or book-value-based approaches exclusively.
- **Typical multiple range:** 0.7-2.0x TBV. JPM trades at ~2.0x (superior ROATCE); C historically at 0.5-0.7x (below-COE returns). Regional banks typically 1.0-1.5x.
- **Dividend Discount Model (DDM):** Appropriate for banks with stable payout policies. Discount projected dividends at cost of equity (typically 10-12%). Most useful for mature, well-capitalized banks.
- **Common pitfalls:** (1) Using P/E without normalizing for credit cycle position -- provisions swing earnings dramatically. (2) Ignoring unrealized losses in the securities portfolio (HTM book) that reduce economic TBV below reported TBV. (3) Comparing P/TBV across banks without adjusting for ROE differences. (4) Treating G-SIB surcharges as temporary -- they are permanent capital costs.

## Turnaround Precedents

| Company | Period | Situation | Actions Taken | Outcome | Timeline | Stock Recovery |
|---------|--------|-----------|--------------|---------|----------|----------------|
| Citigroup (C) | 2008-2025 | Near-failure in GFC, $45B TARP bailout, stock fell from ~$550 to ~$10 (split-adjusted). Decades of complexity and poor risk management. | TARP repayment (2009-10), international consumer exits, Jane Fraser "Project Bora Bora" restructuring (2023-25): reduced management layers 13 to 8, eliminated 60+ committees, $2.5B cost savings. | Success (ongoing). Revenue tracking $84B in 2025 (highest since 2010). Stock up 59% in 2025. Named "Banker of the Year" 2025. | 15+ years (GFC to now, with major acceleration 2023-25) | $10 trough to ~$80+ (8x from trough, still below pre-GFC) |
| Bank of America (BAC) | 2008-2021 | Countrywide acquisition disaster, stock fell to $2.53. Net income collapsed from $21B (2006) to $4B (2008). $17B crisis settlement. | CEO Brian Moynihan's "responsible growth" strategy: shed toxic assets, simplified operations, aggressive cost management, technology investment. | Success. Net income reached $31.9B in 2021. | 12 years to full earnings recovery | $2.53 to $48+ (19x from trough) |
| Wells Fargo (WFC) | 2016-2025 | Fake accounts scandal, 14 consent orders, unprecedented Fed asset cap ($1.95T) imposed Feb 2018. Estimated $4B+ in lost profits. | CEO changes (Stumpf to Sloan to Scharf), rebuilt compliance/risk management from ground up, third-party independent review. Asset cap cost ~$4B+ in forgone profits. | Success (slow). Asset cap removed June 2025 after 7+ years. 12 of 14 consent orders cleared. | 7+ years under asset cap alone | ~$25 trough (2020) to ~$70+ |
| KeyCorp (KEY) | 2023-2025 | Regional bank crisis contagion, 36% profit drop, deposit pressure, NIM compression. | Balance sheet repositioning, deposit repricing strategy, waited for rate environment to normalize. | Partial (ongoing). Stock recovering but earnings still rebuilding. | 2+ years | ~$9 trough (2023) to ~$17 |

**Pattern:** Successful diversified bank turnarounds share three features: (1) new CEO with mandate to simplify, (2) multi-year timeline (5-15 years is normal, not 2-3), and (3) regulatory resolution as a prerequisite (not a bonus). The long timelines challenge the EdenFinTech 30% CAGR hurdle -- most bank turnarounds deliver 15-25% CAGR over extended periods rather than explosive short-term returns.

## Risk Profile

- **Default risk type:** Regulatory / Systemic
- **Cyclicality:** High -- NII moves with rates, credit losses spike in recessions, capital markets revenue is volatile
- **Regulatory discretion:** Extreme -- Fed, OCC, FDIC, CFPB, state regulators all have discretionary authority. Consent orders, asset caps, stress test failures can materially impair value
- **Macro sensitivity:**
  - Interest rates: HIGH -- NII is directly rate-sensitive; yield curve shape matters more than absolute level
  - Credit cycle: HIGH -- provisions for credit losses can swing earnings 30-50% in a downturn
  - Unemployment: HIGH -- drives consumer and SME default rates
  - Liquidity conditions: HIGH -- deposit flight risk (see SVB 2023)
  - Inflation: MODERATE -- indirect via rates and credit quality
  - Trade policy: MODERATE -- affects corporate loan demand and international operations
- **Binary trigger frequency:** Occasional but catastrophic when they occur

### Kill Factors (hard reject -- maps to enrichment override triggers)

1. **CET1 below regulatory minimum** -- Bank is in PCA (Prompt Corrective Action) territory. Historical example: Washington Mutual (2008), seized by FDIC with $307B in assets.
2. **Active FDIC consent order for unsafe/unsound practices** -- Signals fundamental operational failure. Example: Wells Fargo's 14 simultaneous consent orders made it uninvestable for years.
3. **Deposit run or liquidity crisis in progress** -- Once depositors flee, it's a death spiral. Example: SVB lost $42B in one day (March 2023), $100B queued for next morning.
4. **Fraud or material misstatement of financials** -- Destroys trust permanently for financial institutions. Example: Wells Fargo fake accounts scandal (2016).
5. **Negative tangible book value** -- For a bank, this means insolvency. No turnaround path exists without massive dilutive capital raise.

### Friction Factors (PCS modifiers -- reduce confidence, don't kill thesis)

1. **Multiple overlapping consent orders** -- suggested friction: -1 to -2, rationale: each order adds uncertainty about timeline and cost of remediation. Resolution is discretionary.
2. **Earnings below cost of equity for 3+ years** -- suggested friction: -1, rationale: market will not re-rate P/TBV until ROE sustainably exceeds COE. Turnaround timeline is extended.
3. **Unrealized losses in securities portfolio > 20% of tangible equity** -- suggested friction: -1, rationale: economic TBV is materially lower than reported TBV. Risk of forced realization.
4. **G-SIB surcharge increase pending** -- suggested friction: -1, rationale: higher required capital reduces distributable earnings and justified P/TBV.
5. **CEO tenure < 2 years at a bank with structural problems** -- suggested friction: -1, rationale: bank turnarounds take 5-15 years; early-stage CEO lacks track record at scale.

## Thesis-Breaking Patterns

- **Regulatory escalation spiral:** Initial consent order leads to remediation costs, which impair earnings, which attract more scrutiny, which leads to more orders. Gradual. Example: Wells Fargo (2016-2025), Citigroup consent orders.
- **Credit cycle timing trap:** Bank appears cheap at cycle peak when provisions are low and earnings are high. True cost becomes apparent in downturn. Gradual then sudden. Example: Citigroup 2006-2008, many regional banks 2006-2009.
- **Deposit franchise erosion:** Digital competition or reputation damage causes slow deposit outflow, raising funding costs and compressing NIM. Gradual (unless it triggers a run). Example: Community banks losing deposits to fintech/high-yield savings.
- **Contagion and confidence crisis:** Even well-run banks can be dragged down by sector-wide panic. Binary. Example: First Republic Bank (2023) -- fundamentally sound but destroyed by contagion from SVB.

## Evidence Requirements

### Must-Have Data Points

| Data Point | Where to Find It | Why It Matters |
|-----------|-----------------|----------------|
| CET1 Ratio (current + trend) | 10-K Item 8 (Notes to Financial Statements), 10-Q, FMP ratios endpoint | Capital adequacy is existential for banks |
| Tangible Book Value per Share | 10-K Item 8, FMP metrics endpoint (tangibleBookValuePerShare) | Primary valuation anchor |
| Net Interest Margin | 10-K Item 7 (MD&A), FMP metrics endpoint | Revenue quality and rate sensitivity |
| Efficiency Ratio | 10-K Item 7 (MD&A), calculate from FMP income statement | Operating leverage and cost discipline |
| NPL Ratio and NCO Rate | 10-K Item 8, FDIC Call Reports (FFIEC CDR) | Credit quality -- the key earnings driver |
| Provision for Credit Losses (quarterly trend) | 10-Q, FMP income statement endpoint | Leading indicator of management's credit outlook |
| Unrealized gains/losses on securities | 10-K Item 8 Note on investments, OCI in equity statement | Hidden balance sheet risk (SVB's killer) |
| Stress test results (DFAST/CCAR) | Federal Reserve website (annual, June) | Regulatory view of downside risk |
| Consent orders / enforcement actions | Fed, OCC, FDIC enforcement action databases | Regulatory overhang assessment |
| Loan composition by type | 10-K Item 7 or Item 8, FDIC Call Reports | CRE concentration risk, sector exposure |
| Deposit composition (insured vs uninsured) | 10-K Item 8, FDIC Call Reports | Liquidity risk -- uninsured deposits are flight risk |
| ROE vs Cost of Equity | Calculate from 10-K data; COE typically 10-12% for banks | Determines whether bank creates or destroys value |

### Red Flags If Missing

- If CET1 or TBV per share data is unavailable, analyst cannot reliably assess solvency or valuation
- If unrealized securities losses are not disclosed, the SVB-style risk is unquantifiable
- If consent order status is unclear, regulatory timeline cannot be assessed

## Epistemic Profile

| PCS Question | Typical Answer | Rationale |
|-------------|---------------|-----------|
| Q1: Operational risk? | No | Risk is regulatory + systemic, not primarily operational. Bank execution risk exists but is dominated by macro and regulatory factors. |
| Q2: Regulatory minimal? | No | Extreme regulatory discretion -- Fed, OCC, FDIC, CFPB all have authority. Consent orders, stress test failures, asset caps are discretionary. |
| Q3: Historical precedent? | Yes | Strong turnaround precedent base: BAC, C, WFC all recovered from existential crises. Recovery patterns well-documented. |
| Q4: Non-binary outcome? | Mixed | Gradient outcomes exist (slow NIM recovery, gradual credit normalization) but binary triggers also exist (deposit runs, regulatory seizure). |
| Q5: Macro/geo limited? | No | Banks are macro-sensitive by definition: rates, credit cycle, unemployment, liquidity conditions all material. |

**Epistemic stability:** 3/5 -- Bank fundamentals are well-documented and extensively analyzed, but regulatory discretion and macro sensitivity introduce substantial unpredictability. The 2023 bank crisis demonstrated that even well-capitalized banks can be destroyed by contagion.
**Suggested PCS friction:** -1 -- Regulatory risk dominates. Unless a specific bank has clear regulatory runway (no consent orders, strong stress test results), apply -1 friction as default.
