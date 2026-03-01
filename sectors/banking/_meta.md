---
sector: Financials
fmp_sector: "Financial Services"
scope: "Banks only — Diversified + Regional"
hydrated: 2026-03-01
version: 1
sub_sectors:
  - name: "Diversified Banks"
    fmp_industry: "Banks - Diversified"
    gics_code: "40101010"
    file: "sub-sectors/diversified-banks.md"
  - name: "Regional Banks"
    fmp_industry: "Banks - Regional"
    gics_code: "40101015"
    file: "sub-sectors/regional-banks.md"
---

# Banking — Sector Knowledge

Hydrated: 2026-03-01 | Version: 1 | Sub-sectors: 2

## Scope

This knowledge base covers the **Banks** industry group within FMP's "Financial Services" sector, narrowed to:
- **Diversified Banks** (20 NYSE-listed) — JPM, BAC, C, WFC, USB, PNC, etc.
- **Regional Banks** (79 NYSE-listed) — RF, CFG, FITB, KEY, MTB, HBAN, etc.

Excluded from scope: Insurance, Asset Management, Capital Markets, Credit Services, Mortgages, Conglomerates, Data/Exchanges, REITs, Shell Companies.

## File Structure

```
banking/
  _meta.md              ← this file
  overview.md           ← sector map, cross-cutting themes, macro context
  regulation.md         ← US banking regulatory landscape
  valuation.md          ← banking-specific valuation methods
  evidence-requirements.md  ← PCS Q1-Q5 mapped to banking data
  precedents.md         ← turnaround precedent compilation
  sub-sectors/
    diversified-banks.md    ← 40101010 full analysis
    regional-banks.md       ← 40101015 full analysis
```
