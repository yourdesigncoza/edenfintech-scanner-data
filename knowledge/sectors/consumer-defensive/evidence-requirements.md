# Consumer Defensive -- Evidence Requirements

Maps PCS Q1-Q5 to sector-specific evidence. For each question, specifies WHAT to check and WHERE to find it.

## Q1: Is Risk Primarily Operational? (Modelable)

Consumer staples risk is predominantly operational -- brand management, portfolio optimization, cost efficiency, innovation pipeline. This is generally a "Yes" for Q1 across the sector.

### Operational Data Points

| Data Point | Where to Find It | Sub-Sectors Most Relevant |
|-----------|-----------------|--------------------------|
| Organic revenue growth (volume vs price/mix decomposition) | 10-K Item 7 (MD&A); earnings call transcripts; FMP revenue endpoint | All -- volume decline masked by pricing is the #1 red flag |
| Gross margin trend (5-year) | FMP income statement (`bash scripts/fmp-api.sh income TICKER`); 10-K Item 7 | All -- signals pricing power vs input cost absorption |
| FCF margin and EBITDA-to-FCF conversion | FMP cash flow statement (`bash scripts/fmp-api.sh cashflow TICKER`); calculated | All -- cash quality determines reinvestment capacity |
| Market share in core categories | 10-K Item 7 (MD&A); Nielsen/IRI data cited in filings | Packaged Foods, HPC -- share loss is the leading indicator |
| Innovation pipeline (new products as % of revenue) | Earnings calls; 10-K Item 7 | Packaged Foods, HPC -- stale innovation = future share loss |
| Brand investment spend (advertising/promotion) | 10-K SG&A decomposition; proxy statement; earnings calls | All -- under-investment = delayed brand atrophy |
| Case/barrel volume depletion data | 10-K Item 7 (MD&A); state wholesaler reports (beverages) | Beverages -- more accurate than shipments |
| Production facility utilization | 10-K Item 2 (Properties); earnings calls | All -- overcapacity signals industry structure problem |

### When Q1 = "No" (Risk is NOT primarily operational)
- Wine/spirits companies with significant tariff exposure (tariff risk is political/macro, not operational)
- Companies facing product liability litigation from contamination events (legal risk)
- Alcohol companies facing potential demand destruction from GLP-1 drugs (novel structural risk with no operational lever)

## Q2: Is Regulatory Discretion Minimal?

For most consumer staples, regulatory discretion IS minimal. FDA, USDA, and FTC operate rules-based frameworks. This is generally a "Yes" for Q2.

### Regulatory Evidence Sources

| Data Point | Where to Find It | Sub-Sectors Most Relevant |
|-----------|-----------------|--------------------------|
| FDA warning letters and inspection history | FDA Warning Letters database: https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/compliance-actions-and-activities/warning-letters | Packaged Foods -- indicates compliance risk |
| Active recalls | FDA Recalls: https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts | All food/beverage -- active recall = immediate revenue risk |
| FTC enforcement actions on marketing claims | FTC Cases: https://www.ftc.gov/legal-library/browse/cases-proceedings | All -- "Made in USA", health claims, environmental claims |
| TTB compliance status | TTB: https://www.ttb.gov/ | Beverages (alcoholic) -- permit status, labeling compliance |
| State liquor license status | State-specific liquor control board websites | Beverages (alcoholic) -- licensing in key revenue states |
| Pending litigation (product liability) | 10-K Item 8 (Notes -- Commitments and Contingencies); PACER | All -- class actions from recalls, contamination |
| MoCRA compliance status (personal care/cosmetics) | FDA MoCRA guidance; 10-K risk factors | HPC -- new reporting requirements through 2026 |

### When Q2 = "No" (Regulatory discretion IS a factor)
- Companies with active FDA enforcement actions or facility shutdowns
- Alcoholic beverage companies facing tariff-related trade policy changes (discretionary executive/legislative action)
- Companies facing FTC investigation for deceptive practices
- MAHA Commission-driven regulatory changes targeting specific additives/ingredients

## Q3: Are There Historical Precedents?

Turnaround precedent strength varies significantly by sub-sector.

### Precedent Sources

| Data Point | Where to Find It | Sub-Sectors Most Relevant |
|-----------|-----------------|--------------------------|
| Industry turnaround case studies | Sub-sector knowledge files (Turnaround Precedents tables); `$KNOWLEDGE_DIR/sectors/consumer-defensive/precedents.md` | All -- use as base rate anchor |
| Comparable company recovery timelines | Capital IQ/Bloomberg (if available); earnings transcripts of recovered companies | All -- calibrate timeline expectations |
| M&A exit precedents | MergerMarket; press releases; 10-K Item 7 (for acquirees) | Packaged Foods, HPC -- many "turnarounds" are actually acquisitions |
| Bankruptcy/restructuring outcomes | PACER; Bankruptcy court filings; 10-K (post-emergence) | All distressed situations |
| Analyst consensus trajectory | FMP analyst estimates (if available); earnings call Q&A | All -- consensus view provides baseline for contrarian thesis |

### Sub-Sector Precedent Strength

| Sub-Sector | Precedent Strength | Base Rate | Default Band |
|-----------|-------------------|-----------|--------------|
| Packaged Foods | Strong | ~40% (2 of 5 distress cases recovered) | 50% |
| Beverages - Alcoholic | Weak | ~33% (partial recoveries only) | 50% |
| Beverages - Wineries & Distilleries | Weak | ~33% (1 of 3, via exit not turnaround) | 50% |
| Household & Personal Products | Very Weak | ~25% (most distressed HPC firms fail or are absorbed) | 50% |

## Q4: Is Outcome Non-Binary?

Consumer staples generally exhibit gradient outcomes -- this is typically a "Yes" for Q4.

### Gradient vs Binary Evidence

| Data Point | Where to Find It | Sub-Sectors Most Relevant |
|-----------|-----------------|--------------------------|
| Revenue trajectory (gradual decline vs cliff) | FMP income statement (multi-year); 10-K Item 7 trend analysis | All -- gradual = non-binary; cliff = binary |
| Debt maturity schedule | 10-K Item 8 (Notes -- Long-term Debt); FMP balance sheet | All leveraged companies -- near-term maturities = binary refinancing risk |
| Customer concentration | 10-K Item 1A (Risk Factors) | All -- single customer >25% = quasi-binary (loss = catastrophic) |
| Product recall scope | FDA recall database; 10-K contingencies | Packaged Foods -- major contamination can be binary for small companies |
| Tariff exposure quantification | 10-K Item 1A; earnings calls | Beverages -- tariff imposition can be binary for import-dependent producers |
| Patent/IP expiration schedule | 10-K Item 1 (Intellectual Property) | HPC (razors, personal care technology) -- patent cliff can be binary |

### When Q4 = "No" (Outcome IS binary)
- Company with >70% revenue from single customer (loss of customer = existential)
- Distillery with 100% of revenue from single spirit category facing tariff exclusion
- Company in active FDA enforcement with facility shutdown risk
- Company with debt maturity within 12 months and insufficient refinancing capacity

## Q5: Is Macro/Geopolitical Exposure Limited?

Consumer staples are generally low macro sensitivity -- this is typically a "Yes" for Q5. Exception: alcoholic beverages with tariff exposure.

### Macro/Geo Evidence Sources

| Data Point | Where to Find It | Sub-Sectors Most Relevant |
|-----------|-----------------|--------------------------|
| Revenue by geography | 10-K Item 1 (Business); segment reporting | All with international exposure |
| FX impact on reported results | 10-K Item 7 (MD&A); earnings calls | Companies with international operations |
| Commodity input hedge position | 10-K Item 7A (Quantitative and Qualitative Disclosures about Market Risk) | All -- wheat, corn, soy, aluminum, petrochemicals |
| Tariff exposure quantification | 10-K Item 1A (Risk Factors); earnings calls; trade policy announcements | Beverages (alcoholic) -- Mexican agave, EU retaliatory, aluminum |
| Consumer spending trends | BLS Consumer Expenditure Survey; Fed Consumer Credit reports; Deloitte consumer pulse | All -- macro spending slowdown impacts trade-down behavior |
| Interest rate sensitivity | 10-K Item 7A; FMP ratios (debt/equity, interest coverage) | Leveraged companies -- rate increases affect refinancing costs |
| GLP-1 drug adoption data | Prescription data (IQVIA); earnings calls (management commentary) | Packaged Foods (snacking), Beverages (alcoholic) |

### When Q5 = "No" (Macro/geo exposure IS significant)
- Wine/spirits companies with material tariff exposure (Mexico, EU, China)
- Companies with >30% international revenue (FX sensitivity)
- Commodity food producers without hedging programs
- Alcoholic beverage companies in a GLP-1-sensitive consumption category

## Quick-Reference: PCS Evidence Lookup by Sub-Sector

| PCS Question | Packaged Foods | Beverages (Alcoholic) | Wineries & Distilleries | HPC |
|-------------|---------------|----------------------|------------------------|-----|
| Q1 (Operational?) | Yes (brand/portfolio mgmt) | Mostly Yes (volume/mix) | Partial (structural decline + tariffs) | Yes (brand/category mgmt) |
| Q2 (Regulatory minimal?) | Yes (rules-based FDA) | Mostly Yes (TTB predictable) | Mostly Yes (TTB; tariffs are political) | Yes (FDA rules-based) |
| Q3 (Precedent exists?) | Yes (40% base rate) | Partial (33%, low confidence) | Weak (33%, via exit) | Mixed (25%, very low for distress) |
| Q4 (Non-binary?) | Yes (gradient typical) | Yes (gradient typical) | Mostly Yes (gradient typical) | Yes (gradient typical) |
| Q5 (Macro limited?) | Yes (domestic, low FX) | Mostly Yes (domestic) | No (tariffs, FX, structural decline) | Yes (domestic, non-discretionary) |
| **Typical "No" count** | **0-1** | **1-2** | **2-3** | **0-1** |
| **Expected PCS confidence** | **4-5** | **3-4** | **2-3** | **4-5** |
| **Suggested friction** | **0** | **-1** | **-1** | **0** |
