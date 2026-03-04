# EdenFinTech Stock Scan — 2026-03-03

## Scan Parameters
- Universe: NYSE | Focus: Banks - Regional | Stocks scanned: 73
- Date: 2026-03-03
- API: Financial Modeling Prep
- **Special note:** Industry exclusion override — Banks are on the excluded industries list. This scan was run as a limited test per user request. All other hard rules (30% CAGR hurdle, no-catalysts = pass, probability floors, epistemic confidence) remain in full effect.

## Executive Summary
- 3 stocks survived initial screening out of 73 (broken chart + 5-check filter)
- **Zero candidates survived deep analysis.** All 3 were rejected at analysis:
  - FLG (Flagstar Financial): epistemic confidence filter (base 62% x 0.70 = 43.4%, below 60%)
  - LOB (Live Oak Bancshares): base case CAGR 24.1% fails 30% hurdle
  - FFWM (First Foundation): pending merger acquisition — not a turnaround play
- **This outcome validates the exclusion rationale.** Regional banks' structural characteristics — CRE concentration risk, rate-cycle dependency, regulatory opacity, and deposit run vulnerability — make it extremely difficult for any candidate to achieve the combination of high CAGR, high probability, and manageable epistemic uncertainty that the strategy demands.

## Ranked Candidates

**None.** No regional bank candidates survived the full analysis pipeline.

## Rejected at Analysis

### FLG (Flagstar Financial, Inc.) — Rejected: Epistemic Confidence Filter

**Pre-epistemic score:** 56.77 | **CAGR:** 30.88% | **Downside:** 33.6% | **Base Prob:** 62%

- **Thesis:** Former NYCB, nearly collapsed in 2024 due to CRE concentration. Rescued by $1B+ Mnuchin/Liberty consortium. CEO Joseph Otting (ex-OCC Comptroller) executing turnaround: CRE book reduction ($50.6B to $38.3B), returned to profitability Q4 2025 ($0.05 EPS). Guided $0.65-$0.70 EPS (2026), $1.90-$2.00 (2027). Deep discount at 0.68x P/TBV vs. peer median of 1.5x+.
- **Valuation:** P/TBV framework. TBVPS $18.70 today. Projected TBVPS growth via retained earnings: $19.38 (2026E), $21.33 (2027E), $23.93 (2028E). Target 1.2x P/TBV (well below historical median of 1.51x, deeply discounted vs. peers at 2.0-2.3x). Target price: $28.72. CAGR: 30.88% over 3 years.
  - P/TBV discount path: Peer baseline 1.5-2.5x → CRE concentration >300% -0.3x → recent losses history -0.2x → Otting credibility premium +0.2x → **1.2x**
- **Worst case:** ROTCE stays below 8%, CRE losses persist, TBVPS erodes to $17. Floor $8.50 (0.5x P/TBV). 33.6% downside.
- **Moats:** Moderate — large deposit franchise ($67B+), NYC multifamily relationships, but no switching costs or pricing power advantage vs. peers.
- **Catalysts:**
  1. CRE de-risking completion — Timeline: 2026-2027 | Impact: removes overhang, enables P/TBV re-rating
  2. NIM expansion — Timeline: ongoing, NIM rose to 2.14% in Q4 2025 | Impact: earnings recovery
  3. C&I lending pivot — Timeline: commitments up 28% | Impact: revenue diversification from CRE
  4. Holding company dissolution — Timeline: Q2-Q3 2026 | Impact: simplified structure, regulatory streamlining
- **Management:** Strong — Joseph Otting (ex-OCC Comptroller, 40+ years banking). Brought regulatory credibility. 5-year commitment (3 CEO + 2 chairman). Assembled new executive team including CRE workout "SWAT team."
- **Decision Score (pre-epistemic):** Downside 33.6% (adj 39.24) x 0.45 = 27.34 + Probability 62% x 0.40 = 24.80 + CAGR 30.88% x 0.15 = 4.63 = **56.77**
- **Epistemic Confidence:** 2/5 (3 "No" answers)
  - Q1 Operational risk: **No** — CRE cycle and interest rate risk dominate alongside operational execution — Evidence: Sector knowledge: NII 70-80% of revenue; CRE 381% of Tier 1+ACL
  - Q2 Regulatory discretion: **No** — CRE >300% triggers FDIC supervisory scrutiny; multiple overlapping regulators (OCC, FDIC, Fed) — Evidence: FDIC CRE Guidance (300% threshold); FLG at 381%
  - Q3 Historical precedent: **Yes** — Synovus (2009-2013) recovered from NPL >5% with TARP + new CEO; NYCB itself follows documented playbook — Evidence: Synovus trough ~$1.50 → ~$25 by 2016; banking sector precedents knowledge file
  - Q4 Non-binary outcome: **Yes** — Capital injection already occurred and deposits stabilized; remaining risk is gradient of ROTCE recovery speed, not survival — Evidence: $1B+ PE injection completed Mar 2024; Q4 2025 profitable
  - Q5 Macro/geo limited: **No** — NII is dominant revenue source tied to rate cycle; concentrated in NYC multifamily CRE market — Evidence: FMP income data: interest income $4.5B of $4.7B total revenue
  - Risk-type friction: Cyclical/Macro → -1, BUT Q3=Yes with named precedents (Synovus, Regions, Western Alliance) → override to 0. Adjusted confidence remains 2/5.
  - Effective probability: 62% x 0.70 = **43.4%**
  - Confidence cap: 5% max position
  - **REJECTED: effective probability 43.4% below 60% threshold**
- **Probability Sensitivity (using base probability, pre-epistemic):**

  | Probability | Score | Size Band |
  |-------------|-------|-----------|
  | 55% | 53.97 | 0% — fails 60% hard cap |
  | 60% | 55.97 | 6-10% |
  | 65% | 57.97 | 6-10% |
  | 70% | 59.97 | 6-10% |
  | 75% | 61.97 | 6-10% |

- **Structural Diagnosis:**
  - **Role:** Watchlist — interesting turnaround with credible CEO, but epistemic uncertainty is too high
  - **What upgrades to 70+ score?** CRE concentration below 250%, two consecutive profitable quarters with ROTCE >8%, and Fed rate cuts reducing deposit funding costs — all three simultaneously
  - **What breaks the thesis?** NYC multifamily CRE credit cascade causing provisions to exceed PPNR, forcing dilutive capital raise; or deposit confidence shock similar to 2023 bank runs

### LOB (Live Oak Bancshares, Inc.) — Rejected: CAGR Below 30% Hurdle

- **Thesis:** #1 SBA 7(a) lender in the US with $2.8B originated in 2025 (7.7% market share). Record $6.21B total loan production. Unique fintech banking model. Revenue grew from $378M (2020) to $1,041M (2025) — 22.4% 5yr CAGR.
- **Why rejected:** Despite strong fundamentals, LOB is not cheap enough. P/TBV of 1.32x with current 8.7% ROE means the market already prices in improvement. Even with optimistic assumptions (12% ROE, 1.8x P/TBV, 12% TBVPS growth), base case CAGR is only 24.1%. The 30% hurdle requires management's aspirational 15% ROE target AND 2.2x P/TBV multiple, which are bull case, not base case assumptions.
- **Base case CAGR:** 24.1% (TBVPS $38.26 x 1.8x P/TBV = $68.87 target vs. $36.05 current over 3yr)
- **Additional concern:** CEO James Mahan has been selling 20,000 shares regularly (multiple sales in Feb-Mar 2026), which is a negative signal for insider conviction.

### FFWM (First Foundation Inc.) — Rejected: Pending Merger Acquisition

- **Thesis (now moot):** FFWM is being acquired by FirstSun Capital Bancorp (FSUN) in an all-stock merger at 0.16083 FSUN shares per FFWM share. OCC approved the bank merger on Feb 24, 2026. Shareholder vote scheduled for Feb 27, 2026. Closing expected early Q2 2026.
- **Why rejected:** At FSUN price of ~$37.44, the implied FFWM value is ~$6.02 per share vs. current $5.93. This is a ~1.5% merger arb spread closing in weeks — not a turnaround investment opportunity. CAGR is effectively 0% annualized as there is no turnaround to play.

## Portfolio Impact
- Current positions: 10/12 | Available slots: 2
- Catalyst concentration: No regional bank exposure in current portfolio. Adding one would create new theme exposure.
- vs. Weakest holding: TCMD (medical devices) at ~4% weight is the smallest position. No regional bank candidate scored high enough to warrant replacing any existing holding.
- Deployment recommendation: **Scenario 1 applies (cash available for 2 slots).** No regional bank candidate merits deployment. The 2 available slots should be reserved for higher-conviction opportunities from non-excluded sectors. This scan validates the original exclusion decision.

## Rejected at Screening (notable near-misses)
| Ticker | Market Cap | % Off ATH | Failed At | Reason |
|--------|-----------|-----------|-----------|--------|
| SUPV | $0.82B | 55.3% | Broken chart | Argentine bank, 55.3% off ATH — below 60% threshold; also extreme macro/FX/political risk |
| AVAL | $4.88B | 46.6% | Broken chart | Colombian banking group, 46.6% off ATH — well below threshold |
| BBAR | $3.06B | 41.1% | Broken chart | Argentine bank, 41.1% off ATH — below threshold + sovereign risk |
| AMTB | $0.90B | 40.1% | Broken chart | Amerant Bancorp, 40.1% off ATH — below threshold |
| BMA | $4.93B | 36.6% | Broken chart | Argentine bank, 36.6% off ATH — below threshold |
| KEY | $22.86B | 23.8% | Broken chart | KeyCorp, only 23.8% off ATH — market has largely recovered |
| TFC | $63.08B | 26.5% | Broken chart | Truist Financial, 26.5% off ATH — insufficient dislocation |
| USB | $85.00B | 13.5% | Broken chart | US Bancorp, 13.5% off ATH — minimal dislocation |
| DB | $67.67B | 18.0% | Broken chart | Deutsche Bank, 18.0% off ATH — insufficient but notable recovery story |
| WAL | $8.84B | N/A | Broken chart | Western Alliance, recovered from 2023 crisis — no longer broken chart |

## Why Banks Are Excluded: Lessons From This Scan

This test scan confirms the strategic rationale for excluding banks:

1. **Valuation opacity:** Banks use P/TBV, not FCF multiples. The standard EdenFinTech valuation model does not apply. ROIC/ROCE metrics return null from FMP for banks. This creates a fundamental analytical disadvantage.

2. **Epistemic uncertainty is structural, not temporary:** Regional banks face 3-4 out of 5 PCS "No" answers by default (regulatory discretion, macro exposure, CRE cycle risk). Even the most promising turnaround (FLG with an ex-OCC Comptroller CEO) gets crushed by the epistemic confidence filter.

3. **Binary risk is inherent:** Deposit runs can destroy a bank in days (SVB: 2 days from run to seizure). This creates a permanent floor on uncertainty that the strategy's probability framework cannot adequately compensate for.

4. **CAGR hurdle is hard to meet:** Most regional banks trade near 1.0-1.5x P/TBV. Even a deeply discounted bank at 0.5-0.7x P/TBV requires significant multiple re-rating AND earnings recovery to hit 30% CAGR. The math is structurally difficult.

5. **Dilution risk in turnarounds:** Both FLG (168% dilution) and FFWM (47% dilution) required equity raises to survive. This dilutes existing shareholders and reduces per-share recovery.

## Methodology Notes
- Qualitative assessments (moats, management, probability) are LLM estimates — review critically
- Bank valuation uses P/TBV framework, not FCF multiples (per banking valuation guidelines)
- Valuation multiples involve judgment — verify reasoning matches your own assessment
- Catalyst timelines are estimates based on public information as of scan date
- All scoring math computed via calc-score.sh (deterministic, not LLM-generated)
- Epistemic confidence assessed independently — reviewer never sees analyst probability or score
- PCS answers are evidence-anchored — each answer cites a source or declares NO_EVIDENCE
- Risk-type friction applied to PCS confidence where applicable (see scoring-formulas.md)
- Industry exclusion was overridden for this test scan per explicit user request
- Banking-specific sector knowledge from hydrated knowledge base (Banking sector, hydrated 2026-03-03) informed the analysis

---
*Scan completed 2026-03-03 using EdenFinTech deep value turnaround methodology*scan