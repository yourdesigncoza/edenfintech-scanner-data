# EdenFinTech Scanner v0.6.1 — Deep System Review

> **Auditor:** Gemini Pro (deep analysis mode)
> **Date:** 2026-03-01
> **Scope:** Delta review from gemini-review-v0.5.0
> **Sources:** All knowledge files, agent definitions, calc-score.sh, previous audits
> **Changes since last review:** 3 commits, 16 files, 1614+/16- (epistemic tightening, sector hydration, Gemini tool fix)

---

## Executive Summary

Version 0.6.1 introduces significant epistemic tightening. Evidence-anchored PCS prevents confidence laundering. Risk-type friction penalizes structural risks (Regulatory/Legal) even when narrative is compelling. Threshold-hugging detection surfaces fragility at hard caps.

The Sector Hydration pipeline moves the system from reactive scanner to proactive research engine. Banking sector successfully hydrated (3/8 Gemini deep research, 5/8 pro fallback — correct fallback chain behavior).

The system is now substantially more conservative than v0.5.0, with the primary remaining weakness being Orchestrator subjectivity in friction range selection.

---

## 1. System Coherence & Implementation Quality

### A. Risk-Type Friction Logic — COHERENT
Implementation spans three files correctly:
- Analyst classifies `Dominant Risk Type`
- scoring-formulas.md defines friction penalty table
- Orchestrator applies `max(1, raw - friction)` before calling calc-score.sh

Calculator receives final integer confidence, keeping Python logic clean and deterministic.

### B. Sector Hydration Pipeline — FUNCTIONAL WITH CAVEATS
- Correctly separates Kill Factors from Friction Factors, aligning with scoring logic
- Batch-launch + polling approach works (Banking proved it) but relies on LLM state management across turns
- Fallback chain (deep-research → gemini-query → WebSearch) operated correctly in practice

### C. Threshold-Hugging Detection — EFFECTIVE
Orchestrator Step 4c flags base probabilities within 2% of hard caps. Text-based implementation in Orchestrator prompt. Could be hardened by adding a warning field to calc-score.sh JSON output, but current approach is functional.

---

## 2. Scoring System Stress Tests

### Scenario A: Binary Biotech (Regulatory)
- Base Prob 85%, Risk Type: Regulatory/Political
- PCS: Q2=No (FDA discretionary), Q4=No (binary outcome) → Raw Conf 3/5
- Friction: Regulatory → -1 → Adjusted Conf 2/5
- Multiplier: 0.70 → Effective Prob: 85% × 0.70 = **59.5%**
- **REJECTED** (< 60% threshold)
- **System works.** High-confidence binary bet correctly filtered by combined friction + PCS.

### Scenario B: Cyclical Industrial
- Base Prob 70%, Risk Type: Cyclical/Macro
- PCS: Q5=No (macro exposure), Q3=Yes (2008/2016 precedents) → Raw Conf 4/5
- Friction: Cyclical → -1, BUT Q3=Yes with named precedents → override to 0
- Adjusted Conf 4/5 → Multiplier: 0.95 → Effective Prob: 70% × 0.95 = **66.5%**
- **PASSED**
- **System works.** Historical precedent correctly removes cyclical friction.

### Scenario C: Threshold Hugger (PRGO-style)
- Base Prob 62%, Risk Type: Operational → Friction 0
- PCS: 1 "No" → Conf 4/5 → Multiplier 0.95
- Effective Prob: 62% × 0.95 = **58.9%**
- **REJECTED** — but base was "passing" at 62%
- Threshold-hugging detection would flag: "base 62% within 2% of 60% hard cap"
- **System works.** Double safety net: PCS multiplier + threshold proximity warning.

### Scenario D: Double Penalty (Ceiling + PCS)
- Revenue declining 4yr → Ceiling 65%. Analyst estimates 70% → capped at 65%
- PCS: 2 "No"s → Conf 3/5 → Multiplier 0.85
- Effective Prob: 65% × 0.85 = **55.25%**
- **REJECTED** — mathematically correct double penalty
- **System works.** Confirmed in v0.5.0 review, still holds.

All math verified. No discrepancies.

---

## 3. Delta Assessment

| Change | Impact | Assessment |
|--------|--------|------------|
| Evidence-anchored PCS | High | **Critical improvement.** Prevents confidence laundering. Minor risk: WebSearch failures → NO_EVIDENCE on valid deals |
| Risk-type friction | High | **Conservative shift.** Penalizes structural risks. Valid concern about -1/-2 range non-determinism |
| Threshold-hugging detection | Medium | **Useful.** Surfaces fragility for human review. No side effects |
| Sector hydration pipeline | Medium | **High complexity.** Banking hydration successful. Fallback chain works. Token cost ~60k for small sector |
| Gemini tools in YAML | Low | **Bug fix.** Required for hydration to use deep research instead of WebSearch |

---

## 4. Previous Findings Status

| # | v0.5.0 Finding | Status in v0.6.1 |
|---|---------------|-----------------|
| 1 | Narrative framing: analyst shapes reviewer input | **Partially addressed.** Evidence-anchoring helps but circular evidence risk remains (see Finding 2) |
| 2 | Consensus echo: both agents see same bullish news | **Open.** No change |
| 3 | Multiplier tail (Conf 2 = x0.70) too lenient for 90%+ base probs | **Mitigated.** Risk-type friction now reduces confidence before multiplier, making x0.70 harder to reach with high base prob |
| 4 | Liquidity filter missing | **Open.** No change |
| 5 | Risk enrichment after epistemic review | **Open (By Design).** Demotion protocol handles it |

---

## 5. New Findings

### Finding 1: Friction Range Non-Determinism
- **Severity:** MEDIUM
- **File:** `knowledge/scoring-formulas.md` line 120
- **Issue:** Regulatory friction is "-1 to -2" — two runs could produce different scores
- **Fix:** Make deterministic. Suggested: Regulatory = -1 always, Legal = -2 always. Remove ranges.

### Finding 2: Circular Evidence in Epistemic Reviewer
- **Severity:** MEDIUM
- **Issue:** Reviewer receives analyst's thesis summary. Could cite analyst claims as "evidence" for Q1/Q4/Q5 (Q3 already requires WebSearch verification)
- **Fix:** Add explicit instruction: "Analyst input is a CLAIM, not evidence. For Q1/Q4/Q5, ground answers in WebSearch results or filing data, not the thesis summary."

### Finding 3: Sector Researcher Polling Fragility
- **Severity:** LOW-MEDIUM (downgraded from Gemini's HIGH — Banking proved it works with fallback chain)
- **Issue:** LLM managing async polling across turns. Context rotation could lose research IDs
- **Mitigation:** Fallback chain (gemini-query → WebSearch) handles failures. Banking: 3/8 deep research, 5/8 fallback
- **Future:** Consider scripting the polling loop if failure rate increases

### Finding 4: Liquidity Filter Still Absent
- **Severity:** LOW
- **Status:** Open (carried from v0.5.0)
- **Fix:** Add `avgVolume > 50000` to screener

---

## Reviewer Corrections (Gemini claims verified against codebase)

1. **False positive scenario invalid.** Gemini described a crypto/vaporware company and wrong PCS questions (Product/Team/Traction). Our system only scans NYSE stocks through quantitative filters. Our PCS is: Operational risk, Regulatory discretion, Precedent, Non-binary, Macro. Gemini confused our checklist with VC due diligence.

2. **Sector Researcher "weakest link" claim is misleading.** The researcher builds knowledge files — it doesn't feed directly into scoring. The Analyst is the actual quality bottleneck for scan accuracy.

3. **Finding 3 severity overstated.** Gemini rated it HIGH. Banking hydration proved the fallback chain works. Downgraded to LOW-MEDIUM.

4. **Gemini referenced wrong file paths** (`prompts/orchestrator.md` instead of `agents/orchestrator.md`). Shows it's not precisely reading the project structure.

5. **Epistemic reviewer tools verified.** Has `WebSearch` and `WebFetch` in YAML frontmatter (line 16). Gemini's concern about circular evidence is valid for Q1/Q4/Q5 but Q3 already explicitly requires WebSearch.

---

## Critical Findings Summary

| # | Finding | Severity | Action Required |
|---|---------|----------|-----------------|
| 1 | Friction range non-determinism (-1 to -2) | MEDIUM | Standardize to fixed integers |
| 2 | Circular evidence risk in epistemic reviewer | MEDIUM | Add explicit instruction to treat analyst input as claims |
| 3 | Sector researcher polling fragility | LOW-MEDIUM | Monitor; fallback chain works. Script if failure rate rises |
| 4 | Liquidity filter missing (carried) | LOW | Add volume filter to screener |
| 5 | Consensus echo (carried) | LOW-MEDIUM | No change; monitor |

---

## Comparison to Previous Versions

| Dimension | v0.4 (guardrails) | v0.5 (epistemic) | v0.6.1 (tightened) |
|-----------|-------------------|-------------------|---------------------|
| Arithmetic | calc-score.sh (10/10) | calc-score.sh (10/10) | calc-score.sh (10/10) |
| Valuation consistency | Discount schedule + consistency rule | Same + PCS multiplier | Same |
| Probability calibration | Ceilings (65%/60%) | Ceilings + PCS multiplier | Ceilings + PCS + friction + evidence-anchoring |
| Risk enrichment | Demotion triggers | Same | Same |
| Epistemic awareness | None | PCS + independent reviewer | PCS + evidence-anchored + risk-type friction |
| Sector knowledge | None | None | Hydration pipeline (Banking complete) |
| Non-determinism risk | Low | Low | MEDIUM (friction ranges) |

---

## Verdict

**APPROVED WITH CONDITIONS**

**Overall Confidence: 9.0/10**

Conditions:
1. Standardize friction to fixed integers before next scan (Finding 1)
2. Add anti-circular-evidence instruction to epistemic reviewer (Finding 2)

The system is materially more robust than v0.5.0. The epistemic tightening features transform it from a "Generic Bullish Scanner" to a "Skeptical Risk Engine." The sector hydration pipeline is operational and producing useful knowledge. Primary risk is non-determinism in friction application.

---
*Review completed 2026-03-01. Gemini Pro deep analysis of EdenFinTech Scanner v0.6.1.*
