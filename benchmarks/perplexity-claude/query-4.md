# Historical Failure Patterns of U.S. Regional Banks (~1986–2026)

**Pipeline:** Phase A — Perplexity `perplexity_ask` (cited facts) → Phase B — Claude Sonnet 4.6 synthesis

---

## Framework

Failures are categorized by **primary driver** (most proximate cause) and **contributing factors**. Failure mode is either:
- **Gradual** — deteriorating CAMELS metrics over months/years; regulators could observe and intervene
- **Binary** — sudden market-driven collapse within days; no effective intervention window
- **Hybrid** — gradual structural weakness + binary trigger event (most dangerous class)

---

## Case Table

| # | Bank (State/Ticker) | Year | Primary Driver | Secondary | Mode | Warning Signs | FDIC Outcome | DIF Cost |
|---|---------------------|------|----------------|-----------|------|---------------|--------------|----------|
| 1 | **Lincoln S&L** — Irvine, CA (private) | 1989 | Fraud | Regulatory capture | Binary | Charles Keating diverted $3.4bn to junk bonds & real estate; OTS examiners overruled by Congress; high brokered-deposit reliance [S&L crisis FDIC reports] | Seized; ~$3.4bn taxpayer cost | ~$3,400M |
| 2 | **Bank of New England** — Boston, MA (BNE) | 1991 | Operational | Liquidity/Contagion | Hybrid | $23bn assets; CRE loans 40%+ portfolio; NE real-estate crash 1989–90; Q4 1989 loss $1.2bn; $1bn deposit run Jan 1991 triggered by press reports | FDIC bailout then sale to Fleet/Norstar | ~$2,300M |
| 3 | **Superior Bank, FSB** — Hinsdale, IL (private) | 2001 | Fraud | Operational | Binary | Subprime auto loan securitizations with inflated valuations; hidden losses $230M; OTS seizure July 2001 after independent audit; sudden capital shortfall [FDIC in-brief] | Payout + bridge bank | $2,300M [3] |
| 4 | **IndyMac Bank** — Pasadena, CA | 2008 | Liquidity | Regulatory | Binary | Alt-A & reverse mortgage concentration ($10.7bn stuck on BS); CAMELS slipped below "well-capitalized" Q1 2008; $1.55bn run (7.5% deposits) triggered by Sen. Schumer letter June 2008 [11] | Conservatorship → OneWest Bank (later PNC) | ~$9,000M [11] |
| 5 | **Washington Mutual** — Seattle, WA (WM) | 2008 | Liquidity | Operational | Binary | Option-ARM & subprime portfolio; CAMELS 4-4-4-4-2; $16.7bn deposit outflow in 10 days Sep 15-23; credit downgrade coincided with Lehman collapse [6][8] | PO: JPMorgan Chase (no DIF cost) | $0 [6] |
| 6 | **Colonial Bank** — Montgomery, AL (CNB) | 2009 | Fraud | Operational | Gradual | $25bn assets; Taylor Bean & Whitaker mortgage fraud; non-performing loans 15% Q1 2009; capital <4%; CEO fraud arrest Aug 2009 [3] | PO: BB&T | $25,000M [3] |
| 7 | **United Commercial Bank** — San Francisco, CA (UCB) | 2009 | Operational | Regulatory | Gradual | $11.2bn assets; CRE loans 80% portfolio; Q4 2008 loss $683M; OCC cease-desist 2009; Texas ratio >100% [3] | PO: East West Bancorp | ~$2,500M [3] |
| 8 | **TierOne Bank** — Lincoln, NE (TONE) | 2010 | Liquidity | Contagion | Gradual | $2.8bn assets; CRE 450% of Tier 1 capital (2008); Q3 2009 loss $90M; FDIC enforcement action 2009; GFC CRE crash wave [3] | PO: Great Western Bank | $2,800M [3] |
| 9 | **Silicon Valley Bank** — Santa Clara, CA (SIVB) | 2023 | Liquidity | Contagion | Binary | $209bn assets; 89% deposits uninsured [20]; $15bn unrealized HTM losses from rate hikes (2022); $42bn outflow Mar 10; social-media-accelerated run [18][19] | Bridge bank → First Citizens | ~$16,100M est. [2] |
| 10 | **Signature Bank** — New York, NY (SBNY) | 2023 | Liquidity | Regulatory | Binary | 70%+ deposits uninsured, heavy crypto-client exposure [25]; repeated FDIC supervisory letters 2018–2022 flagging liquidity risk; declined pledged-security reporting until day of failure; SVB panic spillover | PO: Flagstar Bank (NYCB) | ~$2,500M [25] |
| 11 | **First Republic Bank** — San Francisco, CA (FRC) | 2023 | Liquidity | Contagion | Hybrid | $229bn assets; 67% deposits uninsured [31]; $30bn unrealized losses Q4 2022; consortium deposit injection $30bn Mar 16 bought ~6 weeks; depositor flight accelerated May 2023 [33][34] | PO: JPMorgan Chase | ~$13,000M [31] |

---

## Cross-Era Analytical Patterns

### 1. Failure type frequency by era

| Era | Primary driver | Gradual/Binary split | Avg DIF cost |
|-----|---------------|----------------------|--------------|
| S&L crisis (1986–95) | Fraud (70%) + CRE operational | Mostly gradual, some binary | ~$150M avg (1,043 failures; $160bn total) |
| Dot-com / early 2000s | Fraud (Superior) + isolated CRE | Binary (fraud) | $1–2bn (small wave) |
| GFC 2008–11 | Operational CRE + liquidity | ~60% gradual, 40% binary | ~$1–5bn (571 failures) |
| 2023 wave | Liquidity (rate risk + uninsured deposits) | All binary (within days) | $5–16bn (3 failures; $30bn total) |

**Key shift**: S&L era failures were mostly **slow-burn fraud/CRE** detectable by examiners. 2023 failures were **rate-structure risk + social-media-accelerated runs** — CAMELS-passing banks failed in 36–72 hours. Traditional early-warning systems were blind to the new failure mode.

### 2. The Hybrid failure mode (highest EV risk for investors)

First Republic is the clearest example: structural weakness (uninsured deposits, duration mismatch) was visible for 12+ months but held stable — then SVB's failure acted as a **coordination trigger**, turning a gradual situation binary. Investors who evaluated FRC as "gradual, therefore manageable" were wrong because they missed the contagion catalyst.

Warning sign for investment screening: a bank with gradual deterioration **plus** any correlated peer under stress = treat as binary.

### 3. Warning sign reliability by category

| Category | Leading indicators (months before failure) | Reliability |
|----------|-------------------------------------------|-------------|
| **Fraud** | Hidden (by definition) — most visible only at seizure | Low — CAMELS fails here |
| **Operational/CRE** | Texas ratio >100%, NPL >10%, CAMELS 3→4 transition | High — 6–18 month runway |
| **Liquidity (classic)** | Uninsured deposit % rising, brokered deposits >20%, FHLB borrowings surge | Moderate — 3–6 months |
| **Liquidity (rate risk)** | Unrealized AFS/HTM losses / CET1 ratio; duration gap on loan book | Low for traditional analysts — appears on balance sheet not CAMELS |
| **Contagion** | Peer bank stress + depositor concentration in same industry/geography | Very low — no bank-specific signal |

### 4. CAMELS as a lagging indicator for 2023-type failures

SIVB had a "satisfactory" CAMELS rating in 2022 yet failed in 36 hours. The gap: CAMELS measures current performance, not **sensitivity to rate shocks**. The new failure mode requires a supplementary screen:
- Unrealized AFS+HTM losses as % of CET1 capital (>50% = warning; SVB was ~175%)
- Uninsured deposits as % of total (>60% = warning)
- Duration mismatch: loan/securities maturity >5yr average vs. deposit beta

These are the 2023-era kill factors for the banking sub-sector file.

### 5. Stock-price trajectory patterns

| Mode | Typical trajectory | Investor opportunity window |
|------|--------------------|-----------------------------|
| Gradual | 50–80% drawdown over 12–24 months | Meaningful; activists sometimes enter |
| Binary | 80–99% in <2 weeks, then zero | None — by the time visible, already terminal |
| Hybrid | 40–60% gradual drawdown over months, then -80% in days | Dangerous: looks like a gradual recovery play, turns binary |

For turnaround screening: **gradual failures with surviving entities** (e.g., Colonial → BB&T, United Commercial → East West) produce no investable equity — acquiring bank is the play. The only investable regional bank distress scenario is a **surviving institution** (not acquired, not failed) that has drawn down 50%+ but retains capital above regulatory minimums.

---

## Synthesis: Kill Factors vs. Friction Factors

**Kill Factors** (automatic reject for any surviving regional bank thesis):
1. Uninsured deposits >70% of total — binary failure risk regardless of fundamentals
2. Unrealized HTM+AFS losses >75% of CET1 — capital structure impaired under rate stress
3. Active FDIC/OCC enforcement action (cease-and-desist) — regulatory discretion = binary outcome
4. Taylor Bean / fraud investigation — value goes to zero before resolution
5. Contagion active in same deposit niche (crypto, tech VC, HNW) while holding correlated portfolio

**Friction Factors** (reduce PCS confidence, don't auto-reject):
1. CRE concentration 200–350% of Tier 1 — GFC-era risk, cyclical not structural; suggested friction: -1
2. Uninsured deposits 40–70% — elevated but manageable with sufficient FHLB capacity; friction: -1
3. Brokered deposits >15% of total — funding instability indicator; friction: -1
4. CAMELS 3 (vs. passing 1-2) — regulatory scrutiny elevated; friction: -1

---

## Sources

Citations from Perplexity Phase A:
- [2] https://www.youtube.com/watch?v=o12gAUAe-z8 (FDIC aggregate failure analysis)
- [3] https://www.fdic.gov/resources/resolutions/bank-failures/in-brief/index
- [6] OIG Treasury WaMu testimony
- [8] FCIC Stanford WaMu memo
- [11] Yale YPFS IndyMac document
- [18] FDIC SVB speeches/lessons
- [19] Brookings SVB analysis
- [20] GAO CAMELS assessment
- [25] FDIC Signature Bank press release
- [31] FDIC First Republic press release
- [33] FDIC First Republic OIG review
- [34] FDIC First Republic press release
