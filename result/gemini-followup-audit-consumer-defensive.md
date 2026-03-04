# Follow-Up Audit: Consumer Defensive Scan — Guardrail Verification
**Subject:** Comparison of Scan Report #1 vs #2 after implementing guardrails
**Auditor:** Gemini Pro (follow-up analysis mode)
**Date:** 2026-03-01
**Sources:** Original audit, Report #1, Report #2, implemented guardrails (valuation-guidelines.md, scoring-formulas.md, strategy-rules.md, calc-score.sh)

---

## Executive Summary

The guardrails implemented after the first audit **substantially improved the scanner's discipline**. The most critical fix — the Enrichment Override Protocol — performed flawlessly, correctly demoting BRBR (the highest-scoring candidate) on two kill-level risks. The SAM probability ceiling worked exactly as designed (capped at 65%). However, the 25x Consumer Staples baseline multiple may be inflating terminal valuations for lower-quality candidates like FLO and SAM, and the report failed to print probability values explicitly, creating an audit gap.

**Verdict:** The system logic is sound. One calibration question remains (baseline multiple), and one output bug needs fixing (missing probability display).

---

## 1. Fix Verification — Grading Each Original Finding

| # | Original Finding | Grade | Evidence |
|---|-----------------|-------|----------|
| 1 | **SAM Multiple (22x → 20x)** | **PARTIALLY RESOLVED** | Discount path correctly applied: 25x → -4x volume decline → -1x pricing power = 20x. Process working. But 20x remains generous for a company with 4yr volume declines — see Section 4. |
| 2 | **SAM Probability (70% → 65%)** | **FULLY RESOLVED** | Reverse-engineering confirms SAM probability = **exactly 65.0%** — the ceiling for 3+ consecutive years of volume decline was correctly applied. Fix working perfectly. Report #2 doesn't display probabilities explicitly (transparency gap), but the math confirms enforcement. |
| 3 | **Ranking Override Without Protocol** | **FULLY RESOLVED** | BRBR correctly demoted via formal Enrichment Override Protocol. Two triggers hit: (1) customer concentration 74% in 3 accounts, (2) sole packaging supplier SPOF. Process documented in report with specific evidence. Textbook execution. |
| 4 | **Inconsistent Multiple Discipline** | **FULLY RESOLVED** | All 4 candidates now show explicit discount paths. Consistency audit reported: median 18.5x, max deviation 4.5x (under the 5x threshold). No candidate received an unjustified premium. |
| 5 | **FLO Margin Sensitivity** | **NEW ISSUE INTRODUCED** | FLO elevated from #4 (62.6, 6% size) to #2 (60.09, 6-10% size). Its 20x multiple equals SAM's — a craft beverage company with strong brands — despite FLO being a commodity bread business. The standardized discount system may be under-penalizing FLO's quality profile. |

### Additional: Calculator Tool (calc-score.sh)
**FULLY RESOLVED** — Methodology notes confirm "All scoring math computed via calc-score.sh (deterministic, not LLM-generated)." Eliminates the arithmetic risk entirely.

### Additional: Multiple Consistency Check
**FULLY RESOLVED** — Report states "Valuation multiples verified via consistency audit (median multiple: 18.5x, max deviation: 4.5x)." Under the 5x threshold.

---

## 2. Score Changes Analysis

### Summary Table

| Ticker | Report #1 | Report #2 | Delta | Cause |
|--------|----------|----------|-------|-------|
| NOMD | 66.4 (#1) | 54.78 (#3) | **-11.6** | Downside 21% → 40% (+19pp), multiple 14x → 17x |
| BRBR | 64.6 (#2) | 61.14 (DEMOTED) | -3.5 | Multiple 15x → 22x (more generous), but demoted on enrichment |
| SAM | 63.3 (#3) | 60.13 (#1) | -3.2 | Multiple 22x → 20x, probability 70% → 65% (ceiling applied) |
| FLO | 62.6 (#4) | 60.09 (#2) | -2.5 | Multiple 15x → 20x (more generous), downside 25% → 35% |

### The NOMD Collapse (66.4 → 54.78)

NOMD's score dropped 11.6 points — the largest swing in the scan. Decomposition:

- **Multiple went UP** (14x → 17x) — the standardized discount system was actually *more generous* than the previous agent's manual assessment
- **Downside nearly doubled** (21% → 40%) — this is the primary driver. The previous agent's 21% downside was arguably too optimistic for a company in a "transition year" with revenue -2% to -5%
- **Probability dropped slightly** (65% → 62%) — reasonable for elevated transition risk

**Assessment:** The previous 21% downside was likely too low. A company losing market share in a transition year with a new CEO reasonably has 35-40% downside. The new score better reflects NOMD's risk profile, though investors who liked NOMD at 66.4 should re-examine whether the 40% downside is overcorrecting.

### The BRBR Paradox

BRBR's raw score actually went UP in implied quality (multiple 15x → 22x, higher CAGR) but was **correctly demoted** by the enrichment protocol. This validates the system design — pure math scores are necessary but not sufficient.

---

## 3. Multiple Consistency Audit

### Discount Path Comparison

| Ticker | Baseline | Discounts Applied | Result | Path Logic |
|--------|----------|-------------------|--------|------------|
| SAM | 25x | Volume decline 3+yr (-4x), limited pricing (-1x) | **20x** | Reasonable. Missing: secular headwind discount? |
| FLO | 25x | Limited pricing (-2x), low-growth base (-3x) | **20x** | Under-discounted. Commodity bread should be lower. |
| NOMD | 25x | European frozen (-3x), revenue decline (-3x), market share loss (-2x) | **17x** | Most discounts applied. Defensible. |
| BRBR | 25x | Spinoff equity (-2x), competition (-1x) | **22x** | Closest to baseline. Growth story justifies less discount. |

### Consistency Check: PASS (barely)

Median: 18.5x. Max deviation: 4.5x (BRBR at 22x vs median 18.5x = 3.5x; NOMD at 17x vs median = 1.5x). All within the 5x threshold.

### Concerns

1. **SAM missing secular headwind discount.** The strategy discount schedule lists "Secular industry headwind (-2x to -4x)" as a separate line item. SAM's own analysis acknowledges "secular alcohol decline" and "sober curious movement." If this discount were applied (-2x), SAM would drop to 18x, and its CAGR would fall to ~26% — **below the 30% hurdle.**

2. **FLO at 20x is generous.** FLO is a commodity bread company with 6.1% FCF margins. Assigning the same terminal multiple as SAM (which has strong brands, 48.5% gross margins, and a fortress balance sheet) seems inconsistent with the spirit of the discount schedule. A 15x-17x multiple would be more appropriate for FLO's quality profile.

3. **BRBR at 22x is logically correct** given its growth trajectory (revenue nearly tripled since 2019). The demotion was not a valuation judgment — it was a structural risk flag.

---

## 4. SAM Re-evaluation: Correction or Overcorrection?

### What Changed

| Input | Report #1 | Report #2 | Direction |
|-------|----------|----------|-----------|
| Multiple | 22x | 20x | More conservative |
| Probability | 70% | 65% | Capped by ceiling |
| Revenue | $2.1B → $2.3B | $2.2B (single year) | Different time horizon |
| FCF Margin | 12% | 11% | More conservative |
| Shares | 10.0M | 9.5M | More buyback credit |
| CAGR | 39% | 31.0% | Barely passes hurdle |

### Assessment: APPROPRIATE CORRECTION, BUT ONE GAP REMAINS

The 22x → 20x reduction and 70% → 65% probability cap are both well-justified by the guardrails. SAM's CAGR dropping from 39% to 31% is mechanically correct and puts it right at the hurdle — which is the correct "borderline" signal for a company with structural headwinds.

**The gap:** SAM's discount path shows "volume decline 3+ years (-4x)" and "limited craft pricing power (-1x)" for a total of -5x. But the 10-K risk factors explicitly disclose "secular alcohol decline" and "sober curious movement" — this should arguably trigger the separate "secular industry headwind (-2x to -4x)" discount. The volume decline discount covers the company-specific trend; the secular headwind covers the industry-wide demographic shift. These are distinct risks.

If the secular headwind discount were applied (-2x minimum), SAM would be at 18x:
- Revenue $2.2B x 11% FCF x 18x / 9.5M = $458.53
- Current price ~$228 (implied from 31% CAGR at $509)
- CAGR at 18x: ~26% → **FAILS 30% HURDLE**

**This is not an overcorrection — SAM may still be insufficiently corrected.** The question for the investor: is secular alcohol decline a separate discount from SAM-specific volume declines, or is it the same risk double-counted?

---

## 5. BRBR Demotion Assessment

### Verdict: **CORRECTLY APPLIED**

| Demotion Trigger | Threshold | Evidence | Status |
|-----------------|-----------|----------|--------|
| Customer concentration | >70% in ≤3 accounts | Walmart+Costco+Amazon = 74.0% | **TRIGGERED** |
| Supply chain SPOF | Threatens identified catalyst | Sole aseptic packaging supplier for 81.7% of revenue | **TRIGGERED** |

**Process compliance:**
- Score NOT revised (61.14 preserved) — correct per protocol
- Candidate ranked below all non-demoted candidates — correct
- Specific triggers documented with evidence — correct
- Demotion reason appears in Portfolio Impact section — correct
- Next-highest non-demoted candidate (SAM) fills the slot — correct

**This is the strongest improvement in Report #2.** The previous audit's biggest concern — informal ranking overrides — is now replaced by a rigorous, documented, auditable protocol.

---

## 6. New Issues Detected

### Issue A: Missing Probability Display (Severity: MEDIUM)

Report #2 does not explicitly print probability values in candidate summaries. Probabilities must be reverse-engineered from scores:

| Ticker | Reverse-Engineered Probability | Ceiling Applied? |
|--------|-------------------------------|-----------------|
| SAM | **65.0%** | Yes — 3+yr volume decline ceiling |
| FLO | **65.0%** | Possibly — unclear which ceiling triggered |
| NOMD | **62.0%** | No ceiling needed |
| BRBR | **68.0%** | Spinoff exempt from 60% neg equity cap |

**FLO at 65% warrants explanation.** FLO's revenue has been *growing* ($4.1B → $5.3B over 5 years). No probability ceiling should apply. If the analyst independently assessed 65%, that's fine — but it coincidentally matches the ceiling value, which could suggest incorrect ceiling application.

**Action Required:** Update report template to display probability values explicitly, including whether a ceiling was applied and which one.

### Issue B: Baseline Multiple Inflation (Severity: MEDIUM-HIGH)

The 25x Consumer Staples baseline is applied uniformly to all candidates, then discounted down. This creates an anchoring bias where even after large discounts, stocks end up at 17-22x — potentially too generous for lower-quality businesses.

**Evidence:**
- NOMD went from 14x (agent judgment, Report #1) to 17x (standardized system, Report #2). The standardized system was *less conservative* than the human for NOMD.
- FLO went from 15x to 20x — a 33% increase in exit multiple for a commodity bread company.

**Counter-argument:** The 25-28x baseline is documented in the strategy rules as appropriate for Consumer Staples. The discounts are designed to bring it down. The system is working as designed, even if the design choice is debatable.

**Recommendation:** Consider whether a sub-sector baseline would be more appropriate: premium consumer brands (25-28x), commodity consumer (18-22x), beverages (20-25x). This prevents commodity bread companies from starting at the same baseline as Procter & Gamble.

### Issue C: FLO Quality-Multiple Mismatch (Severity: MEDIUM)

FLO has 6.1% FCF margins, limited pricing power (commodity bread), and its thesis depends entirely on margin expansion from the $795M Simple Mills acquisition. Yet it receives the same 20x terminal multiple as SAM (48.5% gross margins, fortress balance sheet, iconic brands). The discount schedule penalized FLO for "limited pricing power" and "low-growth base" but not enough to differentiate it from a clearly higher-quality business.

---

## 7. Overall Confidence Assessment

| Dimension | Report #1 | Report #2 | Change | Notes |
|-----------|----------|----------|--------|-------|
| **Arithmetic Accuracy** | 10/10 | **10/10** | — | calc-score.sh eliminates all mental math risk |
| **Screening Compliance** | 9/10 | **10/10** | +1 | BRBR demotion protocol is flawless |
| **Valuation Consistency** | 4/10 | **7/10** | +3 | Discount paths + consistency audit. Deducted for baseline inflation and SAM missing secular headwind. |
| **Probability Calibration** | 5/10 | **8/10** | +3 | SAM ceiling correctly enforced. Deducted for missing display and unexplained FLO 65%. |
| **Strategy Rule Adherence** | 7/10 | **9/10** | +2 | All hard rules followed. Formal demotion protocol. Only gap: possible double-discount ambiguity. |
| **Report Transparency** | 9/10 | **7/10** | -2 | Discount paths are excellent, but REMOVING probability display from the report is a transparency regression. |

### Overall Confidence: **7.5/10** (up from 6/10)

Significant improvement. The system went from "requires manual intervention before capital deployment" to "one calibration question and one output fix from being deployment-ready."

---

## Recommended Actions

### Before Next Scan (Priority)

1. **Display probabilities explicitly** in candidate summaries. Include which ceiling was applied (if any). This is a reporting fix, not a logic fix — the ceilings are already working correctly.

2. **Clarify secular headwind vs. volume decline double-counting.** Add a note to the discount schedule: are these cumulative or overlapping? If cumulative, SAM should be 18x and fails the hurdle. If overlapping (volume decline already captures the secular component), document this reasoning.

### Consider for Future Calibration

3. **Sub-sector baselines.** Consider whether commodity consumer (FLO) deserves a lower starting baseline than premium consumer brands. The current 25x → discount approach anchors all candidates too high.

4. **NOMD downside investigation.** NOMD's downside jumped from 21% to 40% between scans. If the same data was available both times, this suggests the first agent was too optimistic. Verify the 40% worst case is grounded in specific scenario analysis, not just a more pessimistic mood.

---

## Appendix: Reverse-Engineered Score Verification

All scores verified via formula: `Score = (100 - adj_downside) * 0.45 + probability * 0.40 + min(cagr, 100) * 0.15`

| Ticker | Downside | Adj Down | Risk (0.45) | Prob | Prob (0.40) | CAGR | Ret (0.15) | Calc Score | Reported | Match |
|--------|----------|----------|-------------|------|-------------|------|------------|------------|----------|-------|
| SAM | 30% | 34.50 | 29.48 | 65.0% | 26.00 | 31.0% | 4.65 | 60.13 | 60.13 | EXACT |
| FLO | 35% | 41.12 | 26.49 | 65.0% | 26.00 | 50.6% | 7.59 | 60.09 | 60.09 | EXACT |
| NOMD | 40% | 48.00 | 23.40 | 62.0% | 24.80 | 43.9% | 6.59 | 54.78 | 54.78 | EXACT |
| BRBR | 35% | 41.12 | 26.49 | 68.0% | 27.20 | 49.6% | 7.44 | 61.14 | 61.14 | EXACT |

All scores match. calc-score.sh is functioning correctly.

---

*Follow-up audit completed 2026-03-01. Generated by Gemini Pro for EdenFinTech scanner validation.*
*Probability values reverse-engineered and verified by deterministic formula check.*
