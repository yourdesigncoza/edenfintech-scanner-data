# Turnaround precedent analysis - US regional banks (evidence-constrained)

Executive summary
- The available, verified evidence is insufficient to support a sector-wide numerical conclusion about whether downturns in US regional banks are typically cyclical/recoverable or structurally impairing. The documented 2023 episodes include multiple rapid insolvency/resolution events (Silicon Valley Bank, Signature Bank, First Republic) that were structural in outcome (regulatory closures, FDIC receivership, purchase-and-assumption resolutions) while supervisory and ratings analyses since 2023 show peer-group capital and performance stabilization-indicating both kinds of episodes occur in the sub-sector but no dataset in the supplied findings provides the complete price/firm history needed to compute the requested averages and 20-year survivorship rates. [5], [7], [6], [2]
- Primary data needed to compute the brief’s metrics (company stock-price troughs and recoveries, long horizons of distress events, and full event histories) exist in commercial market databases (CRSP/Compustat) but are not present in the supplied evidence; therefore the report provides (a) a validated methodology, (b) sensitivity analyses and definitions that would be applied, (c) evidence-based qualitative findings, and (d) case summaries of well-documented distress episodes from the provided materials (noting that most prominent 2023 episodes ended in regulatory resolution rather than market recovery). [9], [1], [10]

Methodology, data selection rules, definitions, and assumptions
- Primary objective metrics requested:
  - Recovery timeline (primary): time from stock-price trough during the documented distress episode to recovery defined as return to the pre-distress price level (alternative operational/regulatory recovery milestone noted as an option where a public-market recovery is inapplicable).
  - Survivorship (primary): 20-year survivorship rate for banks that experience a documented distress event.
- Distress event (primary definition, per the brief): one or more of (a) regulatory enforcement action, (b) FDIC takeover/receivership, (c) bankruptcy/insolvency filing, (d) placement on a major credit watch, or (e) severe market distress signal such as an X%+ sustained stock decline. The supplied evidence confirms availability of FDIC failure lists and OCC enforcement records (authoritative registries to identify regulatory events) and literature on stock-price behavior during bank runs. [1], [15], [10]
- Data selection rules (to be implemented when the underlying time-series data are obtained):
  - Population: US banks classified as “regional” by the researcher’s classifier (not defined in the supplied evidence); operationally this requires a bank/holding company list to tag firms as regional-this is not provided in the findings and is listed under Evidence Gaps.
  - Event identification: use FDIC failed-bank list and OCC/FDIC/FRB enforcement/press-release archives to tag regulatory events; use CRSP (or equivalent) daily stock returns to detect sustained declines (e.g., 30% drawdown over 30 trading days as a candidate threshold) and to locate trough dates. The findings document CRSP as the appropriate source for historical US security prices. [1], [9], [15], [10]
  - Survivorship: define survival as “continued independent listing / not FDIC-closed / not bankruptcy” at 20 years after distress event; where regulatory resolution transfers substantially all assets and liabilities to an acquirer (purchase-and-assumption) that would be coded as failure/non-survival for the original entity. FDIC failed-bank records provide authoritative resolution events. [1], [8]
- Kaplan-Meier (nonparametric) survival estimation and event-time (time-to-recovery) distributions are the appropriate empirical tools; CRSP/Compustat provide price and accounting time series required to implement them. The supplied evidence explicitly notes CRSP/Compustat coverage availability. [9]
- Sensitivity tests to perform (data required):
  - Distress threshold sensitivity: e.g., regulatory events only vs. regulatory + enforcement actions vs. adding market signals (30%/50%/70% drawdowns). Literature indicates failing banks’ stock prices start to decline early and fall ~25% more than survivors during crises, supporting the inclusion of stock signals as informative. [10]
  - Recovery definition sensitivity: return to pre-distress price; return to a specified fraction (e.g., 75% or 100%) of pre-distress price; or attainment of a regulatory/operational milestone (e.g., capital restoration, removal from enforcement order, acquisition by a healthy bank).
  - Survivorship definition sensitivity: continued independent listing vs. survival of franchise via acquisition (count acquirer survival separately).
- Important assumption explicitly stated: no new market prices, accounting histories, or time-series beyond the supplied findings are assumed or created. Where the supplied evidence lacks the required time series or counts, the report explains gaps and the precise data items needed to compute each metric.

Synthesis of evidence on whether downturns are cyclical/recoverable or structural
- Structural failures with rapid resolution by regulators are documented in 2023: Silicon Valley Bank (SVB) failed and FDIC was appointed to dispose of SVB’s assets; Signature Bank failed in March 2023 and was resolved with portions sold or placed in receivership; First Republic was seized and sold to JPMorgan Chase under a purchase-and-assumption agreement-these outcomes are structural (regulatory closure / receivership) rather than cyclical recoveries. The Federal Reserve’s post-mortem on SVB documents concentration of securities and deposits that contributed to loss of liquidity and rapid failure. [4], [7], [6], [5]
- Market contagion and steep, rapid share-price declines at regional banks occurred in March-May 2023: major regional bank indices and individual regional bank stocks experienced large, abrupt drops and sector market-value losses exceeding $100 billion over two days following SVB’s collapse. This pattern is consistent with panic-style runs and severe market distress episodes that can precipitate structural regulatory outcomes. [4], [3]
- Countervailing evidence (stabilization and capitalization): supervisory and ratings analyses in 2023-2025 indicate that many regional banks showed improving capital metrics (median CET1 ratios and tangible-equity ratios improved according to Fitch’s peer reviews) and Fitch’s reviews expected impaired-loan and net charge-off stabilization through 2026 for the peer group-this indicates that after the 2023 episode, at least for the rated peer group, asset-quality and capital positions were expected to stabilize rather than enter ongoing structural decline. The Fitch analyses therefore point toward recoverability at the peer-group level for many institutions, though individual outcomes depend on idiosyncratic exposures and funding profiles. [17], [18], [2]
- Synthesis statement (evidence-anchored): The supplied evidence documents both types of downturns in recent history: episodes that were structural and ended in regulatory closure (SVB, Signature, First Republic) and a subsequent supervisory/rating view of stabilization across a defined regional peer group. The evidence therefore supports the conclusion that some distress episodes in the US regional-bank sub-sector are structural and terminal for the affected institutions, while other banks in the peer group can and did stabilize (per supervisory/rating assessments). The materials supplied do not permit quantifying the frequency of each outcome across a multi-decade sample. [5], [7], [6], [17]

Quantitative metrics requested - data availability and why direct calculation is not possible from supplied evidence
- Recovery timeline (average time from stock-price trough to recovery): Not computable from the supplied findings because the findings do not include firm-level historical stock-price time series (trough dates, trough prices, or subsequent recovery dates) for a population sample. The findings do note that CRSP provides the necessary historical market data that would be used to compute these metrics; therefore CRSP is the correct source to obtain daily stock prices to implement the time-to-recovery calculation. A straightforward operational implementation would be:
  1. Identify distress date and trough date (minimum price during the distress window) via CRSP/price series.
  2. Record pre-distress price (e.g., price 30 trading days prior to distress) and measure days from trough until closing price first equals or exceeds that pre-distress price (or an alternate milestone).
  3. Apply censoring for firms that never recover within the observation window and use Kaplan-Meier to estimate average and median recovery times and confidence intervals.
  The CRSP/Compustat coverage needed to do this is documented but the actual price data are not provided in the supplied evidence; therefore no numeric recovery timeline can be reported here. [9]
- 20-year survivorship rate for distressed banks: Not computable from the supplied findings. The FDIC failed-bank list and American Banker/Bankrate reporting provide individual failure events and lists for recent years (including the 2023 failures and a count of small failures in 2024-2025), but the required panel identifying all banks that experienced a distress event and their survival status 20 years later is not present. The FDIC failed-bank lists supply authoritative failure/resolution dates that would be used to determine survival/non-survival, but the 20-year survivorship calculation requires constructing a historical cohort (e.g., distress events between 2005-2006 and following each through 2025-2026) from comprehensive source data (FDIC, OCC, CRSP) that are not included in the supplied findings. [1], [8], [11]
- Sensitivity analyses: The supplied literature (NBER) supports inclusion of stock-price signals because failing banks’ stock prices markedly underperform and begin to decline early in run episodes; therefore alternative distress definitions that add stock-price thresholds are conceptually supported. However, without the price series, specific threshold testing (e.g., 30% vs. 50% drawdown) cannot be executed with the supplied evidence. [10]

Case studies (well-documented distress episodes from the supplied evidence)
Note: each case below is constructed solely from the verified findings. Where the supplied facts show regulatory closure or receivership, the outcome is classified accordingly; the supplied evidence does not supply post-trough stock-price recovery series or dates of market-price recovery, so “timeline to recovery” is either inapplicable (no recovery) or marked as “not computable from supplied evidence.”

1) Silicon Valley Bank (SVB)
- Distress period / resolution date: Failure announced March 10, 2023. [4]
- Initial situation / key metrics (supplied): In Q4 2022 SVB Financial Group (SVBFG) had ~ $212 billion in total assets and its securities represented 55% of total assets, with 78% of securities classified as held-to-maturity; total deposits were 89% of total liabilities and uninsured deposits were 94% of total deposits-these concentrations and asset-liability mismatches were central to its rapid failure. SVBFG’s CET1 ratio was 12% in Q4 2022, but its business exhibited large concentration and liquidity vulnerabilities relative to peers. [5]
- Actions taken: The Federal Deposit Insurance Corporation (FDIC) was appointed to dispose of SVB’s assets following closure; regulators and market participants intervened in related markets. The supplied evidence documents FDIC appointment to dispose of SVB’s assets. [4], [5]
- Outcome classification: Failure / regulatory closure (FDIC receivership). [4]
- Timeline to recovery (defined metric): Not applicable - SVB was closed and assets placed for disposition; no pre-distress stock recovery to pre-distress price is reported in the supplied evidence. [4], [5]
- Stock-price trajectory from trough to recovery: The supplied findings document large, abrupt declines in regional bank market value in early March 2023 and that SVB’s collapse precipitated sector losses exceeding $100 billion in two days, but they do not provide the daily price series or trough-to-recovery dates needed to plot or tabulate the requested trajectory. [4], [3]

2) Signature Bank
- Distress period / resolution date: Failure on March 12, 2023 (regulatory closure and FDIC resolution actions in March 2023). [7]
- Initial situation / key metrics (supplied): Signature grew rapidly from $43 billion in assets at year-end 2017 to $110 billion at year-end 2022; uninsured deposits were ~90% of total deposits at year-end 2022; total loans were ~$74 billion with ~$33 billion in commercial real estate and significant multifamily and fund-banking exposures. [7], [79-88 in findings]
- Actions taken: The FDIC effected a resolution that included sale/purchase arrangements; as part of the resolution the FDIC obtained equity appreciation rights in New York Community Bancorp common stock (potential value up to $300 million), and transactions included purchases of Signature Bridge assets with discounts described in the FDIC account. [7], [89-91 in findings]
- Outcome classification: Failure / regulatory closure (assets sold; significant portions remain in receivership). [7]
- Timeline to recovery: Not applicable (closed/resolved). [7]
- Stock-price trajectory from trough to recovery: Not provided in the supplied evidence. The available facts document the bank’s balance-sheet concentrations and the FDIC’s resolution terms but no market price recovery path. [7]

3) First Republic Bank
- Distress period / resolution date: FDIC closed First Republic and appointed itself receiver on May 1, 2023; a purchase-and-assumption agreement with JPMorgan Chase Bank assumed all deposits and substantially all assets. [6], [107 in findings]
- Initial situation / key metrics (supplied): First Republic faced liquidity strains and depositor confidence loss in March 2023 amid significant unrealized fair-value losses, large shares of uninsured deposits, and asset/liability mismatches during a rising interest-rate environment. Prior to failure the bank reported significant loan and deposit growth in 2022 (loan growth 23.6%, deposit growth 12.9%), a business model with ~60% single-family residence loans or home-equity lines, and uninsured deposits representing a large share of funding. [6], [101-105, 108 in findings]
- Actions taken: Management attempted liquidity management in March 2023; regulators closed the bank and arranged a purchase-and-assumption sale to JPMorgan Chase Bank with FDIC as receiver. [6], [107 in findings]
- Outcome classification: Failure / regulatory closure (purchase-and-assumption). [6]
- Timeline to recovery: Not applicable for the original entity (closed and assets assumed by JPMorgan). [6]
- Stock-price trajectory from trough to recovery: The supplied evidence documents stock declines during March-May 2023 and that the firm experienced rapid depositor outflows and unrealized losses, but no firm-level recovery price series are present in the supplied materials. [6], [3]

4) Washington Mutual (selected historical example)
- Distress period / key metrics (supplied): Material deposit outflows began September 15, 2008, with net deposit losses culminating in September 2008; metrics reported include Tier 1 capital to average total assets 7.76% on June 30, 2008, total assets $307.02 billion on June 30, 2008, and large holdings of single-family loans and subprime exposure. [13], [139-150 in findings]
- Actions taken and outcome: The supplied evidence documents catastrophic deposit outflows in mid-September 2008 leading to failure (as described in the historical manuscript), indicating structural failure rather than a market recovery for the original firm. [13]
- Outcome classification: Failure / regulatory closure in 2008 (documented). [13]
- Timeline to recovery and stock-price trajectory: Not computable from supplied evidence (no time-series prices provided). [13]

5) IndyMac (selected historical example)
- Distress period / key metrics (supplied): IndyMac grew rapidly earlier in the 2000s, with assets ~$32.01 billion at closure and deposits ~$19.06 billion; the FDIC prepared to reopen IndyMac on July 14, 2008 per the supplied historical notes. [14], [156-161 in findings]
- Actions taken and outcome: The supplied evidence describes IndyMac’s rapid asset growth and subsequent closure process in 2008; outcome is historical failure. [14]
- Outcome classification: Failure / regulatory closure (documented). [14]
- Timeline to recovery and stock-price trajectory: Not computable from supplied evidence. [14]

Data appendix - what the supplied findings include and what is missing
- Included (from the supplied evidence):
  - Authoritative registries of FDIC failures and failure locations/closure dates for many banks (FDIC failed-bank list). [1]
  - Representative regulatory press releases describing specific 2023 closures and purchase-and-assumption terms (FDIC First Republic press release; FDIC statements on Signature resolution). [6], [7]
  - Federal Reserve post-mortem on Silicon Valley Bank documenting balance-sheet concentrations and deposit structure and summary metrics (assets, securities share, held-to-maturity share, uninsured deposit shares, CET1). [5]
  - Contemporary market reports documenting sector market-value losses and steep share drops in March-May 2023. [4], [3]
  - Ratings-agency and peer-review findings (Fitch) noting peer-group CET1 and other capital metrics and forward expectations for stabilization through 2025-2026 for rated groups. [17], [18], [2]
  - Documentation that CRSP and Compustat contain the market and accounting histories necessary to implement event-time and survivorship calculations. [9]
  - Historical failure case detail sources for Washington Mutual and IndyMac. [13], [14]
  - OCC enforcement-action archives and search tools exist to identify enforcement events. [15], [16]
- Missing (evidence gaps that preclude producing the requested numerical outputs from the supplied findings):
  1. Firm-level daily or monthly stock-price series (CRSP or Bloomberg extracts) for a defined sample of regional banks tied to distress event dates - required to identify trough dates and compute time-to-recovery to pre-distress prices.
  2. A complete, labeled cohort of regional banks and a full event history (regulatory enforcement actions, watch placements, credit-watch dates) spanning at least 20 years to compute 20-year survivorship for distressed cohorts.
  3. Firm-level post-distress accounting outcomes (capital restoration dates, removal from enforcement orders) to support alternative operational/regulatory recovery milestones for institutions that did not recover in the market.
  4. A replicable list mapping public bank tickers to FDIC/charter IDs for the full sample period (essential to merge CRSP prices, Compustat accounting, and FDIC event dates).
  5. Daily stock-price trough and recovery dates for the case studies (not present in the supplied findings), which prevents plotting trough-to-recovery trajectories or computing days-to-recovery.
- Because these items are not present among the verified findings, numerical computation of the average recovery timeline, survivorship rates, and case-study price-trajectory charts cannot be produced here without obtaining the enumerated datasets.

Proposed empirical implementation (what would be done once data are obtained)
- Data assembly:
  1. Acquire CRSP daily (or monthly) price series for all publicly listed US bank holding companies / banks in the regional classification for the relevant sample period (e.g., 2000-2025). [9]
  2. Acquire FDIC failed-bank list and OCC/FDIC enforcement action datasets and extract event dates. [1], [15], [16], [8]
  3. Merge Compustat accounting series for capital ratios and balance-sheet exposures to support operational recovery milestone definitions. [9]
- Event and sample construction:
  - Define distress events per the brief (regulatory enforcement, FDIC takeover, bankruptcy, major credit-watch placement, or market drawdown threshold). Use NBER findings on stock behavior to justify inclusion of market thresholds. [10]
- Estimation:
  - For recovery time: for each event, compute trough price date during the distress window and date of first closing price ≥ pre-distress price (or alternate milestone). Use Kaplan-Meier / cumulative incidence to compute median/mean days to recovery and confidence intervals; report censored observations (no recovery during observation window).
  - For survivorship: construct cohorts by distress year and compute 20-year survival via Kaplan-Meier using regulator closure / bankruptcy / delisting as failure events.
  - Sensitivity: re-compute using alternative drawdown thresholds and alternative recovery milestones (regulatory removal from enforcement, capital ratio crossing thresholds).
- Diagnostics: report number of events, right-censoring share, distribution of event severities, and provide survival curves and summary tables.

Evidence gaps and limitations (concise)
- The supplied evidence documents many individual failures and supervisory assessments but does not include the firm-level historical market prices, the merged event/cohort panel, or the 20-year follow-up needed to compute the requested numerical metrics. The absence of CRSP price extracts and a labeled regional-bank cohort is the critical missing element. [9], [1], [8]
- Consequently, the brief’s requested quantitative outputs (average recovery timeline, a computed 20-year survivorship rate, and trough-to-recovery stock-price charts for the turnaround cases) cannot be produced from the provided findings alone.

Concluding assessment (evidence-only)
- The supplied evidence shows that: (a) regional banks can experience both panic/market runs and idiosyncratic structural failures leading to regulatory closure (documented in 2023: SVB, Signature, First Republic), and (b) ratings-agency and supervisory peer reviews after 2023 saw signs of stabilization and improved capital metrics for a defined regional peer group-implying that while some episodes are terminal, others are recoverable at the peer level. However, the evidence does not contain the market and cohort data necessary to quantify average recovery timelines or to calculate a 20-year survivorship rate for distressed banks. [5], [4], [7], [6], [17], [18]
- Recommendation: to produce the precise quantitative answers requested, obtain (or grant access to) CRSP daily price series and Compustat accounting for a defined universe of regional banks, merge with FDIC/OCC enforcement and FDIC failed-bank lists to identify distress events, and implement the event-time and survival analysis described above. [9], [1]

References (numbered sources used above)
[1] https://www.fdic.gov/bank-failures/failed-bank-list
[2] https://www.fitchratings.com/research/banks/fitch-completes-review-of-major-us-regional-banks-09-10-2025
[3] https://www.cnbc.com/2023/05/04/regional-banks-fall-pacwest-down-40percent.html
[4] https://www.reuters.com/business/finance/us-bank-stocks-add-losses-regulators-shutter-svb-financial-2023-03-10/
[5] https://www.federalreserve.gov/publications/2023-April-SVB-Evolution-of-Silicon-Valley-Bank.htm
[6] https://www.fdic.gov/news/press-releases/2023/pr23073a.pdf
[7] https://www.fdic.gov/news/speeches/2023/spmar2723.html
[8] https://www.americanbanker.com/list/15-most-recent-bank-failures
[9] https://wrds-www.wharton.upenn.edu/pages/about/data-vendors/center-for-research-in-security-prices-crsp/
[10] https://www.nber.org/system/files/working_papers/w29753/w29753.pdf
[11] https://www.bankrate.com/banking/list-of-failed-banks/
[12] https://www.sec.gov/Archives/edgar/data/1212545/000121254523000109/earningsrelease0404final004.htm
[13] https://www.aabri.com/manuscripts/243786.pdf
[14] https://elischolar.library.yale.edu/cgi/viewcontent.cgi?article=5089&context=ypfs-documents
[15] https://www.occ.gov/news-issuances/news-releases/2025/nr-occ-2025-5.html
[16] https://www.occ.gov/news-issuances/news-releases/2025/nr-occ-2025-46.html
[17] https://www.fitchratings.com/research/banks/fitch-completes-review-of-15-regional-banks-23-04-2025
[18] https://www.fitchratings.com/research/banks/fitch-ratings-completes-peer-review-of-13-us-regional-banks-03-05-2024
[19] https://en.wikipedia.org/wiki/2023_United_States_banking_crisis
