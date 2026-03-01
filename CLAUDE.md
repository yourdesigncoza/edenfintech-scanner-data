# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

Data repository for the EdenFinTech stock scanner plugin (`edenfintech-scanner`). Stores all scanner outputs: FMP API cache, scan reports, sector knowledge, and deep research. No application code — this is a pure data/content repo.

## Repository Structure

```
cache/              FMP API response cache (JSON), organized by endpoint
  screener/         NYSE stock screener results (by exchange-sector)
  profile/          Company profiles (by ticker)
  price-history/    Historical prices (by ticker)
  income/           Income statements
  balance/          Balance sheets
  cashflow/         Cash flow statements
  ratios/           Financial ratios
  metrics/          Key metrics
  ev/               Enterprise value
  peers/            Peer comparisons
  risk-factors/     10-K risk factor extractions

scans/              Final scan report markdown files
                    Naming: YYYY-MM-DD-{sector}-scan-report[-NN].md

sectors/            Hydrated sector knowledge (consumed by scanner agents)
  {sector}/
    _meta.md        Frontmatter registry: sub-sectors, FMP industry mapping, GICS codes
    overview.md     Sector map, cross-cutting themes, macro context
    regulation.md   Regulatory landscape
    valuation.md    Sector-specific valuation methods (may override standard FCF model)
    evidence-requirements.md   PCS Q1-Q5 mapped to sector-specific data sources
    precedents.md   Turnaround precedent compilation
    sub-sectors/    Per-sub-sector deep analysis with frontmatter metadata

research/           Raw deep research outputs (Gemini, web search)
  sectors/{sector}/{sub-sector}/
    q1-q8 files     Individual research question outputs
    fmp-screener-raw.json   Raw FMP screener data
```

## Key Conventions

- **Sector knowledge `_meta.md` frontmatter** is the source of truth for sub-sector definitions, FMP industry names, and GICS codes. Always read `_meta.md` first when working with a sector.
- **Sub-sector files use YAML frontmatter** with fields: `fmp_industry`, `gics_code`, `epistemic_stability`, `suggested_pcs_friction`, `typical_valuation`, `fcf_multiple_baseline`.
- **Banking (and potentially other financial sectors) override the standard FCF valuation model** — they use P/TBV regression vs ROTCE instead. Check `valuation.md` before assuming FCF multiples apply.
- **Scan reports follow a strict format**: Executive Summary > Ranked Candidates > Demotions > Filter Funnel. Each candidate includes: thesis, valuation formula, worst case, moats, catalysts, management, suggested size, confidence flags, and 10-K risk factors.
- **Cache files are raw FMP API JSON responses** — arrays of objects keyed by ticker symbol. Not manually edited.

## API Keys

Stored in `.env` (gitignored):
- `FMP_API_KEY` — Financial Modeling Prep API
- `MASSIVE_API_KEY` — Massive.com (10-K risk factor extraction)

## Related Plugin

The scanner logic lives in the Claude Code plugin at `~/.claude/plugins/marketplaces/edenfintech-scanner/`. Key agents: orchestrator, screener, analyst, epistemic-reviewer, sector-coordinator, sector-researcher. Knowledge files there define strategy rules, scoring formulas, valuation guidelines, excluded industries, and current portfolio.
