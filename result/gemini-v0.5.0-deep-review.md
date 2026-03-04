# EdenFinTech Scanner v0.5.0 — Deep System Review

> **Auditor:** Gemini Pro (deep analysis mode)
> **Date:** 2026-02-28
> **Scope:** Full system audit with focus on Epistemic Confidence Layer (PCS)
> **Sources:** All knowledge files, agent definitions, calc-score.sh, previous Gemini audits

---

## Executive Summary

The EdenFinTech Scanner v0.5.0 represents a significant leap in maturity. The introduction of the **Epistemic Confidence Layer (PCS)** and the **Information Barrier** between the Analyst and Reviewer effectively mitigates the "hallucinated certainty" problem common in LLM-based financial analysis.

The system is now **structurally conservative**. The mathematical interplay between Confidence Multipliers and the Hard Probability Floor (60%) creates a rigorous filter that will reject most technically valid "value" picks due to epistemic uncertainty. This aligns with the "Discipline beats talent" philosophy.

**All 5 recommendations from the previous audit are implemented and effective.** The SAM false positive scenario from the consumer defensive scan would be caught by multiple overlapping guardrails (discount schedule, consistency rule, probability ceilings, and now PCS).

**Overall System Rating: 8.8/10** (up from ~6/10 pre-guardrails)

---

## 1. Epistemic Layer Assessment — HIGH INTEGRITY

The 5-question PCS framework is sound. It correctly targets specific areas where LLMs struggle: distinguishing between *risk* (modelable) and *uncertainty* (Knightian/unmodelable).

### Multiplier Calibration

| Confidence | "No" Count | Multiplier | Effect on 70% base prob |
|------------|-----------|------------|-------------------------|
| 5 | 0 | x1.00 | 70% → survives |
| 4 | 1 | x0.95 | 66.5% → survives |
| 3 | 2 | x0.85 | 59.5% → **killed** (below 60%) |
| 2 | 3 | x0.70 | 49% → **killed** |
| 1 | 4-5 | x0.50 | 35% → **killed** |

**Key insight:** Confidence 3 (x0.85) is the "killer" tier. A standard high-conviction turnaround (base prob 70%) with two epistemic "No" answers becomes 59.5% — just below the 60% hard floor. This correctly forces analysts to find opportunities where *both* the thesis is strong (prob > 75%) *and* the structure is knowable (conf > 3).

### Information Barrier — Effective

The architecture forces the Reviewer to judge the *quality of the argument*, not the *conclusion*. By stripping score and probability, it prevents anchoring bias. The Reviewer has WebSearch to independently verify claims (especially precedents for Q3).

### Multiplier Curve Discussion — MEDIUM

Gemini recommended steepening the tail (changing Conf 2 from x0.70 to x0.50). Analysis:

- **Current**: Conf 2 (x0.70) still allows a 90% base prob to exit at 63% (above 60% threshold)
- **Proposed**: x0.50 would collapse Conf 2 and Conf 1 into the same multiplier — loses granularity
- **Assessment**: The current x0.70 is defensible because Conf 2 already has a hard size cap of 5%. Even if a stock leaks through the 60% floor at confidence 2, it's capped at a tiny position. The size cap is the real safety net here, not the probability multiplier alone.
- **Verdict**: Keep current multipliers. Monitor for false positives at Conf 2 in practice.

---

## 2. System Coherence — MEDIUM (One Sequencing Note)

### Sequencing: Risk Enrichment vs. Epistemic Review

**Observation:** The orchestrator runs epistemic review (Step 4a) before risk enrichment (Step 5b).

**Gemini's recommendation:** Move enrichment before epistemic review.

**Counter-analysis:** This is BY DESIGN. Risk enrichment is optional (requires Massive API key + user approval), only applies to top 2-4 candidates, and happens after ranking is established. Moving it earlier would break the flow because enrichment requires knowing who the top candidates are.

**The real gap:** If enrichment reveals a binary risk (e.g., pending lawsuit) that wasn't in the analyst's original thesis, the epistemic confidence score was computed without this information. However, the enrichment demotion protocol handles this separately — it can demote candidates regardless of their confidence score.

**Verdict:** Current sequence is acceptable. The demotion protocol is the correct mechanism for post-enrichment risk handling, not confidence re-assessment.

### All Other Components Align

- Strategy rules, scoring formulas, valuation guidelines, agent prompts, and calc-score.sh are consistent
- No contradictions found between knowledge files and agent instructions
- The calc-score.sh correctly implements all formulas from scoring-formulas.md
- Hard breakpoints in the calculator match the knowledge file definitions exactly

---

## 3. Implementation Quality — HIGH

### calc-score.sh
- All math uses Python3 for precision (prevents shell integer division bugs)
- JSON output enables deterministic verification
- Backward compatible — confidence params are optional
- `effective-prob` command correctly implements `base * multiplier`
- `score` command with confidence correctly applies multiplier before scoring
- `size` command correctly applies min(score_cap, hard_cap, confidence_cap, binary_override)

### Orchestrator Epistemic Flow
The 8-step epistemic flow in the orchestrator (Step 4a) correctly implements what scoring-formulas.md defines:
1. Extract epistemic input — strips probability and score ✓
2. Spawn reviewer — passes only thesis/risks/catalysts/moat ✓
3. Receive confidence scores ✓
4. Compute effective probability via calc-score.sh ✓
5. Filter on effective probability < 60% ✓
6. Recompute score with effective probability ✓
7. Recompute position size with confidence cap ✓
8. Apply binary outcome override ✓

---

## 4. Previous Recommendations — ALL IMPLEMENTED

| Recommendation | Status | Implementation |
|---------------|--------|----------------|
| Calculator tool | **FIXED** | calc-score.sh — deterministic Python math |
| Multiple calibration rules | **FIXED** | Discount Schedule in valuation-guidelines.md |
| Probability guardrails | **FIXED** | Probability Ceilings in scoring-formulas.md |
| Enrichment override protocol | **FIXED** | Step 5b demotion triggers in strategy-rules.md |
| Multiple consistency check | **FIXED** | Step 4b in orchestrator (median ±5x rule) |

Healthcare scan validated: 8.5/10 score, all guardrails effective across sectors.

---

## 5. New Weaknesses & Attack Surfaces

### 5a. Narrative Framing Risk — MEDIUM

**The risk:** The analyst prepares the "Epistemic Input" section for the reviewer. While the information barrier protects against anchoring on probability/score, the analyst's framing of risks and catalysts could subtly influence the reviewer's assessment.

**Current mitigations:**
- Analyst prompt says "Think like a skeptic — your job is to find reasons NOT to invest"
- Reviewer has WebSearch for independent verification
- Reviewer answers guidelines are specific (e.g., Q3 requires citing actual precedents)

**Additional mitigation proposed by Gemini:** "Adversarial Premise Injection" — force the reviewer to search for three contradicting facts before scoring. This would harden the review but adds latency and API cost.

**Verdict:** Monitor. If future scans show the reviewer consistently giving high confidence to stocks the analyst favored, consider adding adversarial search.

### 5b. Consensus Echo — LOW-MEDIUM

**The risk:** Both analyst and reviewer use WebSearch. If recent news is uniformly bullish, both agents see the same hype cycle. The system validates popularity, not quality.

**Current mitigation:** The analyst is prompted to "find reasons NOT to invest." The reviewer's questions are structural (operational/regulatory/precedent/binary/macro), not sentiment-based.

**Proposed hardening:** In the reviewer's WebSearch for Q3 (precedent), add a time range to look for bear cases from >6 months ago. This surfaces structural issues that persist despite recent optimism.

### 5c. Jargon Mirror (Edge Case) — LOW

**The risk:** For highly technical industries, the analyst might use plausible-sounding jargon that the reviewer can't effectively evaluate.

**Current mitigation:** The excluded industries list removes most technical/opaque sectors (Biotech, Pure AI, Banks, Insurance, Most Software). The remaining investable universe is generally understandable (consumer goods, industrials, healthcare devices, auto parts).

**Verdict:** Low risk given the exclusion list. Only a concern if exceptions are expanded.

---

## 6. Methodology Maturity

### Comparison to Institutional Risk Management

**Strengths (institutional-grade):**
- Separation of "Upside Analysis" (Analyst) and "Uncertainty Pricing" (Reviewer) mirrors Portfolio Manager / Risk Desk interaction at hedge funds
- Deterministic calculator prevents the "mark your own homework" problem
- Hard breakpoints function like institutional risk limits
- Theme concentration caps (50%) provide basic correlation management

**Gaps vs. institutional practice:**

| Gap | Severity | Notes |
|-----|----------|-------|
| **Correlation risk** | LOW | Theme caps partially address this, but no explicit macro factor correlation check. Acceptable for 12-position portfolio. |
| **Liquidity risk** | LOW | No explicit Average Daily Volume (ADV) filter. The 60% ATH drop + $50M market cap floor implicitly excludes the most illiquid names, but a mid-cap with thin volume could slip through. |
| **Scenario analysis** | MEDIUM | The system models base case + worst case but lacks explicit bull case or scenario weighting. The probability sensitivity table partially addresses this. |
| **Drawdown monitoring** | N/A | Steps 7-8 (monitoring/sell) are manual, which is appropriate for a scanner tool. |

---

## 7. Hard Rules Audit

### Fully Enforceable (Deterministic)

| Rule | Enforcement |
|------|-------------|
| CAGR < 30% → size 0% | calc-score.sh (hard-coded) |
| Probability < 60% → size 0% | calc-score.sh (applies to effective prob) |
| Downside 80-99% → max 5% | calc-score.sh |
| Downside 100% → max 3% | calc-score.sh |
| Score < 45 → no investment | calc-score.sh |
| 60%+ off ATH | Screener (data-driven check) |
| Excluded industries | Screener (list-based check) |

### Partially Enforceable (Agent Judgment Required)

| Rule | Risk | Mitigation |
|------|------|------------|
| "Must be understandable" | Subjective — agent can claim understanding | Low risk: excluded industries remove most opaque sectors |
| "Not in secular decline" | Agents may confuse cyclical downturn with secular decline | Analyst Step 3 margin trend check (5yr) partially enforces |
| No catalysts = pass | LLMs may accept vague "management plans to improve" as catalysts | Analyst prompt requires specific timelines and impact |
| Heroic assumptions test | Requires comparing to 10yr historical data (which may not be available) | calc-score.sh can verify CAGR math, but margin/multiple checks rely on agent data gathering |
| Max 12 positions / 50% theme cap | Portfolio rules enforced by orchestrator reading current-portfolio.md | Dependent on file being up-to-date |

---

## 8. Scoring System Stress Test

### Scenario A: Perfect Unicorn
- **Input:** Downside 0%, Prob 100%, CAGR 100%, Confidence 5 (x1.00)
- **Effective prob:** 100%
- **Adj downside:** 0 × (1 + 0/200) = 0
- **Score:** (100 - 0) × 0.45 + 100 × 0.40 + 100 × 0.15 = 45 + 40 + 15 = **100**
- **Size:** 15-20% (score 75+), no caps triggered
- **Verdict:** Correct. Maximum score, maximum position.

### Scenario B: High Risk + Low Confidence
- **Input:** Downside 80%, Prob 60%, CAGR 30%, Confidence 2 (x0.70)
- **Effective prob:** 60 × 0.70 = **42%**
- **Hard breakpoint:** Effective prob 42% < 60% → **Position size = 0% (KILL)**
- **Score not even computed — killed at probability gate**
- **Verdict:** SYSTEM SUCCESS. Low confidence correctly kills a borderline trade.

### Scenario C: The Heartbreaker
- **Input:** Downside 30%, Prob 70%, CAGR 50%, Confidence 3 (x0.85)
- **Effective prob:** 70 × 0.85 = **59.5%**
- **Hard breakpoint:** Effective prob 59.5% < 60% → **Position size = 0% (KILL)**
- **Verdict:** SYSTEM SUCCESS. The ruthlessness of the math: a 70% probability trade is rejected because of 2 epistemic "No" answers. Forces the analyst to find only opportunities where both the thesis is strong AND the structure is knowable.

### Scenario D: Ceiling + PCS Double Penalty
- **Input:** 3+ yr revenue decline (ceiling 65%), Confidence 3 (x0.85)
- **Effective prob:** 65 × 0.85 = **55.25%**
- **Hard breakpoint:** 55.25% < 60% → **Position size = 0% (KILL)**
- **Is this over-penalizing?** NO. Two orthogonal risks are being modeled:
  1. Fundamental risk (ceiling): the business is objectively shrinking
  2. Epistemic risk (PCS): the analysis has structural uncertainty
  - A shrinking business with imperfect data clarity should never be a Buy
- **Verdict:** Correct double-penalty. The system demands BOTH strong fundamentals AND clear epistemic foundations.

### Scenario E: Binary Outcome Override
- **Input:** Downside 20%, Prob 85%, CAGR 50%, Q4=No (binary), Confidence 3
- **Effective prob:** 85 × 0.85 = **72.25%** (above 60%)
- **Adj downside:** 20 × 1.10 = 22
- **Score:** (100-22) × 0.45 + 72.25 × 0.40 + 50 × 0.15 = 35.1 + 28.9 + 7.5 = **71.5**
- **Score-based size:** 65-74 band → 10-15%
- **Confidence cap:** Conf 3 → max 8%
- **Binary override:** Q4=No AND Conf ≤ 3 → max **5%**
- **Final size:** min(10-15%, 8%, 5%) = **5%**
- **Verdict:** Correct. A stock with a binary outcome and uncertain analysis gets a tiny position despite a good score. The binary override caps below the confidence cap — functioning as designed.

---

## Critical Findings Summary

| # | Finding | Severity | Action Required |
|---|---------|----------|-----------------|
| 1 | Narrative framing: analyst shapes reviewer input | MEDIUM | Monitor; consider adversarial search injection if pattern emerges |
| 2 | Consensus echo: both agents may see same bullish news | LOW-MEDIUM | Add time-range diversification to reviewer's WebSearch |
| 3 | Multiplier tail (Conf 2 = x0.70) may be too lenient for 90%+ base probs | LOW | Size cap at 5% provides sufficient safety net; monitor |
| 4 | Liquidity filter missing | LOW | Consider ADV > $1M or Market Cap > $300M filter in screener |
| 5 | Risk enrichment happens after epistemic review | LOW (By Design) | Demotion protocol handles this; no change needed |

---

## Comparison to Previous System (pre-v0.5.0)

| Dimension | v0.3 (pre-guardrails) | v0.4 (post-guardrails) | v0.5 (epistemic layer) |
|-----------|----------------------|------------------------|------------------------|
| Arithmetic accuracy | LLM-dependent (risky) | calc-score.sh (10/10) | calc-score.sh (10/10) |
| Valuation consistency | Agent discretion (SAM drift) | Discount schedule + consistency rule | Same + PCS multiplier |
| Probability calibration | Unconstrained (SAM 70% for declining biz) | Ceilings (65%/60%) | Ceilings + PCS multiplier (double filter) |
| Risk enrichment handling | No protocol | Demotion triggers | Same |
| Epistemic awareness | None | None | PCS + independent reviewer |
| Position sizing guardrails | Score bands only | Score + hard breakpoints + downside caps | Score + hard breakpoints + downside caps + confidence caps + binary override |

---

## Verdict

**APPROVED FOR DEPLOYMENT.**

The system is structurally conservative — likely too conservative for some investors. It will reject many genuine opportunities due to epistemic uncertainty. This is a feature, not a bug, for the stated philosophy ("Discipline beats talent. Patience is an edge.").

The only finding above LOW-MEDIUM severity is the narrative framing risk, which is inherent to any multi-agent pipeline and is partially mitigated by existing prompt engineering. No capital-at-risk issues identified.

**Overall Confidence: 8.8/10**

---

*Review completed 2026-02-28. Gemini Pro deep analysis of EdenFinTech Scanner v0.5.0.*
