# Banking Sector — Valuation Methods

## Critical: FCF Multiples Do NOT Apply to Banks

The EdenFinTech strategy's standard 4-input valuation model (`Revenue x FCF Margin x FCF Multiple / Shares = Price Target`) is **not applicable** to banks. Bank "free cash flow" is meaningless because:
- Lending IS the business — loan originations/repayments dwarf operating income in cash flow statements
- Capital adequacy requirements constrain distributions (you cannot distribute "free cash flow" freely)
- "Cash flow from operations" for a bank is a regulatory/accounting construct, not an economic reality

**The analyst must use earnings-based or book-value-based approaches exclusively.**

## Primary Method: P/TBV Regression vs ROTCE

The workhorse valuation method for both diversified and regional banks.

### Concept
A bank's justified Price-to-Tangible Book Value multiple is a function of its Return on Tangible Common Equity (ROTCE) relative to its cost of equity (COE).

```
Justified P/TBV = (ROTCE - growth) / (COE - growth)
```

**Simplified rule of thumb:**
- Bank earning COE (~10-11%) = ~1.0x TBV
- Each 1% ROTCE above COE adds ~0.10-0.20x to justified P/TBV

### Typical Ranges

| Sub-sector | P/TBV Range | Context |
|-----------|-------------|---------|
| Diversified Banks (G-SIBs) | 0.7-2.5x | JPM ~2.0x (superior ROTCE), C historically 0.5-0.7x (below-COE returns) |
| Regional Banks | 0.5-1.8x | Strong performers (FITB, MTB) at 1.2-1.8x; distressed at 0.5-0.8x |
| M&A premium | 1.5-2.0x | For well-run franchises with attractive deposit bases |

### Adjustments

**Adjust P/TBV UP for:**
- ROTCE sustainably >15% (superior returns)
- Fee income diversification >35% of revenue
- Deposit franchise strength (high % insured, low cost of deposits)
- Clean regulatory record (no consent orders)
- Attractive M&A geography

**Adjust P/TBV DOWN for:**
- ROTCE <10% (below cost of equity = value destruction)
- CRE concentration >200% of capital
- Unrealized securities losses >15% of tangible equity (economic TBV < reported TBV)
- Active consent orders or regulatory restrictions
- Elevated NPLs or rising provision trends
- Uninsured deposit concentration >50%

### Economic TBV Adjustment
**Critical post-2023:** Reported TBV may overstate economic TBV if the bank holds significant unrealized losses in its securities portfolio (particularly HTM securities not marked to market). Always calculate:

```
Economic TBV = Reported TBV - After-tax unrealized HTM losses
```

This was the core mechanism that destroyed SVB and First Republic.

## Secondary Method: P/E on Normalized Earnings

Useful as a cross-check, particularly for banks with stable through-cycle earnings.

| Sub-sector | P/E Range | When Applicable |
|-----------|-----------|-----------------|
| Diversified Banks earning >COE | 12-15x | Stable, above-COE earners with strong fee income |
| Diversified Banks earning ~COE | 10-12x | At cost of equity, limited growth premium |
| Regional Banks earning >COE | 10-13x | Stable regional with growth franchise |
| Regional Banks earning ~COE | 8-10x | At or below COE, limited premium |
| Distressed/turnaround | 5-8x (if earnings exist) | Often meaningless — use P/TBV instead |

### Normalization Requirements
- **Credit cycle:** Normalize provisions to through-cycle average (0.3-0.5% NCOs for diversified, 0.2-0.6% for regionals)
- **Rate environment:** Consider NIM sustainability if current rates are unusually high/low
- **One-time items:** Strip out litigation charges, restructuring costs, MSR/CVA adjustments
- **Securities gains/losses:** Exclude unrealized mark-to-market noise

## Tertiary Method: Dividend Discount Model (DDM)

Appropriate for mature banks with stable payout policies.

```
Value = D1 / (COE - g)
```

Where:
- D1 = Expected next-year dividend per share
- COE = Cost of equity (typically 10-12% for banks)
- g = Sustainable dividend growth rate (typically 3-7%)

**Best for:** Well-capitalized banks with 25-40% payout ratios and predictable earnings
**Not useful for:** Turnaround candidates (dividends cut or suspended), banks under regulatory restrictions on capital return

## Cross-Reference with EdenFinTech Valuation Guidelines

The standard EdenFinTech discount schedule needs sector-specific translation:

| EdenFinTech Discount Condition | Banking Translation |
|-------------------------------|-------------------|
| Revenue declining 2+ years | NII or total revenue declining (often rate-driven, not operational) |
| Above-average leverage vs peers | N/A — all banks are highly leveraged by design. Use CET1 ratio vs peers instead. |
| Regulatory/structural risk | Consent orders, asset caps, pending Basel III Endgame impact |
| Limited pricing power | Deposit franchise weakness (high beta deposits, losing share to fintech) |
| Secular industry headwind | CRE structural decline (office), fintech competition, crypto disruption |

### Heroic Assumptions Test (Banking Version)
A banking valuation is "heroic" if ANY of:
- ROTCE assumption exceeds bank's 10-year peak by >20%
- NIM assumption exceeds 10-year peak
- P/TBV multiple exceeds 2.0x for a regional or 2.5x for a diversified bank without explicit justification
- Credit loss assumption is below the 10-year trough (assuming best-case credit environment)

## Common Valuation Pitfalls in Banking

1. **Using P/E without normalizing for credit cycle** — Provisions swing earnings 30-50% in downturns. A bank can look cheap on P/E at cycle peak when provisions are artificially low.

2. **Ignoring unrealized HTM losses** — Economic TBV may be significantly lower than reported TBV. This was SVB's killer.

3. **Comparing P/TBV across banks without adjusting for ROTCE** — A bank at 0.8x TBV with 7% ROTCE is more expensive than a bank at 1.5x TBV with 18% ROTCE.

4. **Treating G-SIB surcharges as temporary** — They are permanent capital costs that reduce distributable earnings.

5. **Confusing "cheap on P/TBV" with "good turnaround candidate"** — Banks trading below 1.0x TBV are often there for good reasons (below-COE returns, CRE risk, regulatory overhang). Cheapness alone is not a catalyst.

6. **Ignoring deposit cost trajectory** — Rising deposit costs can silently destroy NIM even as loan yields appear stable.

7. **Underestimating regulatory timeline** — Consent orders and asset caps operate on regulatory time (years), not market time (quarters). Wells Fargo's asset cap lasted 7+ years.
