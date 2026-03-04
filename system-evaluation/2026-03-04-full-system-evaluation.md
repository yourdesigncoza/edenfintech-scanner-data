# EdenFinTech Scanner — Full System Evaluation

**Date:** 2026-03-04
**Scope:** Complete strategy-to-implementation fidelity review
**Source:** All 8 strategy documents (edenfintech-system/00-08), all 6 agent files, calc-score.sh, scan-stocks skill, 5 knowledge files

---

## Strategy-to-Scanner Fidelity: Step by Step

| Strategy Step | Scanner Component | Verdict |
|---|---|---|
| **Step 1** — Broken chart (60%+ off ATH), industry exclusions, secular decline check, quality sniff, double-plus potential | Screener agent — all 5 sub-checks implemented with correct thresholds | Faithful |
| **Step 2** — 5 Checks (solvency, dilution, revenue, ROIC, valuation) | Screener agent — each check matches strategy logic including borderline flags, SBC-to-pay-debt immediate DQ, cyclical ROIC exception, normalized P/FCF | Faithful |
| **Step 3** — Competitor comparison with quality priority ranking | Analyst agent — structured table, balance sheet > niches > risk-adjusted return ordering, permanent pass for 5yr declining margins | Faithful |
| **Step 4** — 5 qualitative questions (moats, leadership, issues, comp, catalysts) | Analyst agent — all 5 with ratings, HARD RULE on no catalysts = automatic pass enforced | Faithful |
| **Step 5** — 4-input valuation (Rev x FCF Margin x Multiple / Shares) | Analyst agent + calc-score.sh — deterministic math, industry baselines, discount schedule, worst case, gut check, heroic assumptions test | Faithful + Enhanced |
| **Step 5b** — Risk factor enrichment, demotion triggers | Orchestrator Step 5b — Massive.com integration, manual approval, all 4 demotion triggers matched exactly | Faithful |
| **Step 6** — Decision scoring (45/40/15 weights, non-linear downside) | calc-score.sh `score` command — exact formula, penalty curve, probability ceilings, PCS layer | Faithful + Enhanced |
| **Step 7** — Position sizing (score bands, hard breakpoints, portfolio rules) | calc-score.sh `size` command — all breakpoints (CAGR<30%, prob<60%, downside caps), score-to-size bands, 12-position max, 50% theme cap | Faithful + Enhanced |
| **Step 8** — Monitoring & sell triggers | strategy-rules.md reference — scanner is a buy-side tool, correctly doesn't try to be a portfolio manager | Appropriate scope |

**Bottom line: Every step of John's strategy is faithfully implemented. Not one rule is missing or softened.**

---

## Layers Added Beyond the Strategy

These aren't in John's original system but strengthen it materially:

### 1. Epistemic Confidence Layer (PCS)

The strategy's biggest weakness is that probability estimates are subjective. The independent 5-question reviewer with evidence-anchoring, plus the multiplier on probability, adds a systematic "how confident are we in the confidence" layer. This is genuinely valuable.

- 5-question checklist (operational risk, regulatory discretion, precedent, binary outcome, macro exposure)
- Independent reviewer agent — never sees the analyst's probability or score
- Evidence-anchoring rule — each answer must cite a source or declare NO_EVIDENCE
- Multiplier table: confidence 5 = x1.00, 4 = x0.95, 3 = x0.85, 2 = x0.70, 1 = x0.50
- Confidence-based size caps: 5 = no cap, 4 = 12%, 3 = 8%, 2 = 5%, 1 = 0% (watchlist)
- Binary outcome override: Q4=No + confidence ≤3 → max 5%

### 2. Risk-Type Friction

Systematizes the intuition that regulatory/legal risks are harder to model than operational risks. The friction table is well-calibrated:

| Dominant Risk Type | Friction |
|--------------------|----------|
| Operational / Financial | 0 (default) |
| Cyclical / Macro | -1 |
| Regulatory / Political | -1 to -2 |
| Legal / Investigation | -2 |
| Structural fragility (SPOF) | -1 |

Friction does NOT stack with PCS answers — prevents double-counting.

### 3. Probability Ceilings

Hard caps that prevent overconfidence in specific situations:

| Condition | Max Probability |
|-----------|----------------|
| Revenue/volume declined 3+ consecutive years | 65% |
| Negative equity (not from spinoff leverage) | 60% |
| CEO tenure < 1 year | 65% |

### 4. Threshold-Hugging Detection

Catches when probability lands suspiciously close to a hard cap (within 2%), surfacing potential anchoring bias. Warning only — doesn't reject, but surfaces fragility for human scrutiny.

### 5. Deterministic Scoring (calc-score.sh)

Eliminates LLM arithmetic errors. Commands: `score`, `cagr`, `valuation`, `size`, `effective-prob`. All math is JSON-output, verifiable, traceable. Combined with "score once, no revisions" discipline in the analyst — prevents score-shopping.

### 6. Heroic Assumptions Test + Consistency Rule

Systematic valuation sanity checks:
- Revenue growth required is 3x industry average → heroic
- FCF margin exceeds company's 10-year peak → heroic
- FCF multiple exceeds historical median by >50% → heroic
- Any heroic flag → valuation fails
- No FCF multiple may deviate >5x from scan median without written justification (consistency rule)

### 7. Sector Knowledge Pipeline

Perplexity-powered research with structured templates:
- 8-query coverage per sub-sector (structure, regulatory, macro, failures, binary triggers, turnarounds, epistemic, valuation)
- Phase A.5 audit catches gaps, contradictions, and citation vacuums before synthesis
- Evidence requirements mapped to PCS questions
- Kill Factors separated from Friction Factors
- On-demand hydration triggered by scan survivors (not pre-loaded)
- 6-month staleness tracking via `hydration-status.json`

---

## Architecture Summary

```
/scan-stocks (skill entry point)
    → Orchestrator (coordinator)
        → Step 3b: Sector Knowledge Check (on-demand hydration)
            → Sector Coordinator → parallel Sector Researchers (Perplexity MCP)
        → Screener (Phase 1: quantitative, Steps 1-2)
        → Analyst agents (Phase 2: deep analysis, Steps 3-6, parallel per cluster)
        → Epistemic Reviewer (independent confidence assessment)
        → Consistency audit + threshold detection
        → Risk factor enrichment (Massive.com, manual approval)
    → Final ranked report
```

**Data flow:** Agents communicate via Task tool prompt/response. Orchestrator strips probability/score before passing to epistemic reviewer (breaks self-assessment loop).

**Deterministic math:** All scoring, CAGR, valuation, and sizing computed by calc-score.sh — not LLM-generated.

**Knowledge pipeline:** FMP API (financial data) + Perplexity MCP (sector research) + Massive.com (10-K risk factors).

---

## Honest Assessment of Gaps

### 1. "Pure AI" Exclusion is Unmapped

The excluded-industries list says "Pure AI" but there's no FMP industry string for it. Relies on screener judgment. Low risk since few NYSE pure-AI companies would pass the 60%-off-ATH filter anyway.

**Severity:** Low
**Action:** Consider adding specific FMP industry strings or company-level exclusion list.

### 2. "Most Software" is Fuzzy

The ">15x P/S with no profitability path" threshold is a judgment call. The screener can apply it, but different runs might produce inconsistent results for borderline software companies.

**Severity:** Medium
**Action:** Could add explicit FMP industry strings for "always exclude" software sub-sectors vs. "judgment required" ones.

### 3. The 20% CAGR Exception is Hard to Police

"Top-tier CEO + 6yr+ runway" is inherently subjective. An LLM might apply it too liberally. Consider whether this should remain an analyst decision or require human confirmation.

**Severity:** Medium
**Action:** Could add a mandatory flag that routes these to human review rather than letting the analyst auto-proceed.

### 4. No Portfolio Monitoring

The scanner finds buy candidates. It doesn't track whether existing catalysts are on schedule, whether to sell, or whether to rebalance. This is by design and the right scope, but a companion monitoring tool would complete the investment lifecycle.

**Severity:** Low (scope limitation, not a bug)
**Action:** Future project — not scanner scope.

---

## Verdict

The EdenFinTech Scanner is a genuinely solid multi-tiered system. The architecture is sound:

- **Screener** — ruthlessly quantitative, most stocks fail here (as they should)
- **Analyst** — qualitative heavy lifting with hard guardrails (no catalysts = pass, heroic assumptions = fail, one-shot scoring)
- **Epistemic Reviewer** — breaks the self-assessment loop (biggest innovation over the base strategy)
- **Orchestrator** — ties it all together with consistency audits, threshold detection, deployment scenario analysis
- **calc-score.sh** — makes the math trustworthy and verifiable
- **Sector hydration** — gives analysts real context with on-demand triggering and staleness tracking

The system is:
- **Disciplined** where it matters (hard rules never bypassed)
- **Flexible** where it should be (qualitative judgment in moat/management assessment)
- **Honest** about what it can't do (human judgment flags, confidence scores, "Insufficient data" rather than fabrication)

**The main risk isn't in the system — it's in overriding it when the system says "pass" on a stock you like.**

---

*Evaluation conducted 2026-03-04. Reviewed against strategy source documents at `/home/laudes/zoot/projects/strategy_EdenFinTech/edenfintech-system/` and scanner implementation at `/home/laudes/zoot/projects/edenfintech-scanner/`.*
