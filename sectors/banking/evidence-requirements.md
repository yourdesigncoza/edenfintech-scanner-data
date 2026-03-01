# Banking Sector — Evidence Requirements

Maps PCS Q1-Q5 to banking-specific evidence. For each question, specifies WHAT data to examine and WHERE to find it.

## Q1: Is Risk Primarily Operational (Modelable)?

Banking risk is partially modelable — credit and interest rate risk have mature frameworks, but deposit behavior and regulatory discretion introduce unmodelable uncertainty.

### Operational / Modelable Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Net Interest Margin (NIM) + trend | 10-K Item 7 (MD&A), FMP metrics endpoint | Rate sensitivity and revenue quality. Modelable via rate scenarios. |
| Loan composition by type | 10-K Item 7 or 8, FDIC Call Reports (FFIEC CDR) | CRE, C&I, consumer, mortgage mix. Each has different credit risk profiles. |
| NPL ratio + NCO rate (quarterly) | 10-K Item 8, 10-Q, FDIC Call Reports | Credit quality trend. Modelable via historical loss rates and economic scenarios. |
| Provision for Credit Losses (quarterly) | 10-Q, FMP income statement | Management's forward credit outlook. Leading indicator. |
| Interest rate sensitivity disclosure | 10-K Item 7A (Market Risk), earnings call slides | Banks disclose NII impact of +/-100/200bps rate changes. Directly modelable. |
| Duration of securities portfolio | 10-K Item 8 notes on investments | Duration mismatch risk (the SVB mechanism). Modelable. |

### Non-Modelable / Judgment-Required Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Deposit behavior during stress | Earnings calls, FDIC quarterly banking profile | Post-2023, deposit "stickiness" is no longer reliably modelable. |
| Regulatory enforcement pipeline | Fed/OCC/FDIC enforcement databases | Consent order resolution timeline is discretionary, not modelable. |
| Management credibility | Earnings calls, proxy statement, CEO track record | Turnaround execution quality is judgment-based. |

**PCS Q1 typical answer for banking:** Partial Yes (diversified banks) / Partial Yes (regionals). Core metrics are modelable but deposit behavior and regulatory outcomes are not.

## Q2: Is Regulatory Discretion Minimal?

No. Banking faces extreme regulatory discretion from multiple overlapping regulators.

### Regulatory Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Active consent orders | Fed enforcement: federalreserve.gov/supervisionreg/enforcement-actions.htm | Number, severity, and age of outstanding orders. More orders = longer resolution timeline. |
| | OCC enforcement: occ.gov/topics/laws-and-regulations/enforcement-actions/ | |
| | FDIC enforcement: fdic.gov/bank-examinations/enforcement | |
| Stress test results (DFAST/CCAR) | Federal Reserve website (published annually, June) | Regulatory view of downside capital adequacy. Failing = blocked dividends/buybacks. |
| Asset cap status | Fed enforcement actions, earnings calls | Asset cap = growth frozen = permanent ROE compression until resolved. |
| Regulatory category (I-IV) | 10-K Item 1, earnings call slides | Determines capital requirements, stress test obligations, AOCI treatment. |
| Matters Requiring Attention (MRA/MRIA) | Not publicly disclosed — infer from earnings calls, proxy | Informal regulatory warnings. MRIA = serious concern, potential precursor to consent order. |
| CRA rating | FFIEC CRA ratings database | Poor CRA rating blocks M&A and branch expansion. |
| Upcoming rule changes | Federal Register (NPRM), Fed SR Letters, FDIC FILs | Basel III Endgame, LTD requirements, LCR recalibration — all pending. |

**PCS Q2 typical answer for banking:** No. Extreme discretion from Fed, OCC, FDIC, CFPB, and state regulators.

## Q3: Are There Historical Precedents for Turnarounds?

Mixed. Strong precedent base for credit-cycle turnarounds. Weak precedent for liquidity crises (usually end in seizure or forced sale).

### Precedent Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Historical bank turnaround cases | See precedents.md for compiled table | Pattern matching: does current situation resemble BAC (success), RF (success), or NCC (failure)? |
| FDIC failed bank list | fdic.gov/bank/individual/failed/banklist.html | Historical failure rate and survivorship data. |
| Previous crisis recoveries at THIS bank | 10-K Business section, investor presentations | Has the specific bank navigated a prior crisis? What was the playbook? |
| CEO tenure and turnaround track record | Proxy statement, press releases | New CEO with turnaround mandate (positive) vs entrenched management (negative). |
| M&A comparable transactions | Bank Director M&A database, S&P Global | Recent acquisition multiples for similar banks. Establishes floor value. |

**PCS Q3 typical answer for banking:** Yes for diversified banks (BAC, C, WFC all recovered from existential crises). Mixed for regionals (credit-cycle turnarounds work; liquidity crises usually fail independently).

## Q4: Are Outcomes Non-Binary?

No. Banking has structural binary risk via FDIC receivership.

### Binary vs Gradient Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Uninsured deposit ratio | 10-K Item 8, FDIC Call Reports, earnings calls | >50% = elevated run risk. >75% = structural binary trigger. SVB was 94%. |
| CET1 buffer above PCA trigger | 10-K/Q capital ratios | How much capital cushion exists before mandatory seizure. <200bps buffer = danger zone. |
| Liquidity Coverage Ratio (LCR) | 10-K Item 7A, stress test disclosures (Cat III/IV) | Days of survival under deposit outflow. Low LCR + high uninsured = binary risk. |
| Deposit insurance status | FDIC BankFind | Confirms FDIC-insured status and primary regulator. |
| FHLB borrowing capacity | 10-K Item 8 notes, earnings calls | Backup liquidity source. Maxed-out FHLB borrowings = limited emergency buffer. |
| Fed discount window access | Not directly disclosed | Banks that have pre-positioned collateral can borrow from Fed as last resort. |

**PCS Q4 typical answer for banking:** No (regionals — binary seizure risk). Mixed (diversified banks — G-SIBs have implicit TBTF protection providing gradient outcomes).

## Q5: Is Macro/Geopolitical Exposure Limited?

Partially. Domestic-focused but heavily macro-sensitive through rates and credit cycles.

### Macro Exposure Evidence

| Data Point | Where to Find It | What It Tells You |
|-----------|-----------------|-------------------|
| Geographic revenue concentration | 10-K Item 1 or Item 7, segment disclosures | Regionals: near-100% US. Diversified: C has ~40% international; WFC is 95%+ US. |
| Interest rate sensitivity | 10-K Item 7A, earnings call rate sensitivity tables | NII impact of +/-100/200bps. Both sub-sectors are rate-sensitive. |
| CRE exposure by property type and geography | 10-K supplemental tables, FDIC Call Reports | Office vs multifamily vs retail. Geographic concentration in distressed markets. |
| Sector loan concentration | 10-K Item 7 credit risk section | Energy, agriculture, tech — sector-specific loan books create macro correlation. |
| International operations (diversified only) | 10-K segment disclosures | C, JPM, GS have material international exposure (FX, sovereign, geopolitical). |

**PCS Q5 typical answer for banking:** Partial Yes (regionals — domestic but rate/credit-cycle dependent). No (diversified G-SIBs with significant international operations).

## Summary: Evidence Checklist for Banking Candidates

Before an analyst can assign a probability estimate to a banking turnaround thesis, ALL of the following must be examined:

### Tier 1 (Must-Have — Cannot Assess Without)
- [ ] CET1 ratio and trend (solvency)
- [ ] Tangible Book Value per share (valuation anchor)
- [ ] ROTCE or ROE (earnings power vs COE)
- [ ] NPL ratio and NCO rate (credit quality)
- [ ] Unrealized securities losses — AFS and HTM (economic TBV)
- [ ] Uninsured deposit ratio (run risk)
- [ ] Active consent orders / enforcement actions (regulatory overhang)

### Tier 2 (Important — Significantly Improves Confidence)
- [ ] NIM and efficiency ratio trends
- [ ] CRE concentration (% of capital) and composition (office vs other)
- [ ] Provision for Credit Losses quarterly trend
- [ ] Stress test results (if applicable)
- [ ] Loan-to-deposit ratio
- [ ] Deposit cost trajectory
- [ ] CEO tenure and turnaround mandate

### Tier 3 (Supplementary — Adds Nuance)
- [ ] Dividend payout ratio and capital return capacity
- [ ] FHLB borrowing capacity
- [ ] CRA rating
- [ ] Peer comparison (P/TBV vs ROTCE regression)
- [ ] M&A comparable transactions

### Red Flags If Missing
- CRE concentration not disclosed by loan type (office/multifamily/retail) -- primary risk unquantifiable
- Uninsured deposit ratio unavailable -- 2023-style run risk unassessable
- Unrealized securities losses not broken out (AFS vs HTM) -- SVB-style risk hidden
- Consent order status unclear -- regulatory timeline unassessable
- ROTCE or TBV per share not calculable -- valuation impossible
