# EdenFinTech Scanner v0.8.0 — Deep System Review

> **Auditor:** Gemini Pro (deep analysis mode)
> **Date:** 2026-03-03
> **Scope:** Delta review from gemini-review-v0.6.1
> **Sources:** All knowledge files, agent definitions, calc-score.sh, previous audits
> **Changes since last review:** 5 commits, 25 files, 352+/1744-. Major: knowledge file relocation to data dir, sector hydration migrated from Gemini/OpenAI to Perplexity MCP.

---

## Executive Summary

The v0.8.0 update introduces two significant architectural improvements: (1) knowledge file relocation to a persistent data directory, fixing data loss on plugin cache refreshes, and (2) sector hydration migration to Perplexity MCP, providing citation-backed research with better fact density. The core financial logic (scoring, sizing, hard rules) is completely unchanged and remains mathematically sound. All stress test scenarios verified exactly against calc-score.sh.

The system's overall maturity has improved incrementally. The v0.6.0 epistemic tightening (evidence-anchored PCS, risk-type friction, threshold-hugging detection) was never formally reviewed and is now validated as correctly implemented. No new capital-at-risk issues identified.

**Overall System Rating: 9.0/10** (up from 8.8 in v0.5.0 review)

---

## 1. System Coherence — HIGH

### Knowledge File Relocation
- All 4 core agents + 2 sector agents now resolve `$KNOWLEDGE_DIR` dynamically via `fmp-api.sh knowledge-dir`
- Auto-bootstrapping (copy-on-missing) ensures backward compatibility
- Single source of truth for directory path prevents agent fragmentation
- **No contradictions found** between knowledge files and agent instructions
- Knowledge file CONTENT is completely unchanged — only the storage location moved

### Perplexity MCP Integration
- Phase A/B split (Perplexity search → Claude synthesis) is the correct design pattern
- Decouples fact retrieval from analytical synthesis, preventing context pollution
- Q6 turnaround precision fix correctly excludes sector-wide panic selloffs
- Hard stop prereq prevents silent fallback to hallucinated sector data
- 403 fallback (perplexity_ask with URL) handles SEC/FDIC/Fed bot blocks

### Core Logic Alignment
- strategy-rules.md, scoring-formulas.md, valuation-guidelines.md, agent prompts, and calc-score.sh remain fully consistent
- calc-score.sh correctly implements all formulas from scoring-formulas.md
- Hard breakpoints in calculator match knowledge file definitions exactly
- Orchestrator's 8-step epistemic flow correctly implements scoring-formulas.md
- Risk-type friction, threshold-hugging detection, and binary override all implemented correctly

---

## 2. Implementation Quality — HIGH

### calc-score.sh Verification
- All math uses Python3 for precision (prevents shell integer division bugs)
- JSON output enables deterministic verification
- PCS multiplier table: {5: 1.00, 4: 0.95, 3: 0.85, 2: 0.70, 1: 0.50} — matches scoring-formulas.md
- `effective-prob` correctly implements `base * multiplier`
- `score` with confidence correctly applies multiplier before scoring
- `size` correctly applies `min(score_cap, hard_cap, confidence_cap, binary_override)`
- Backward compatible — confidence and binary params are optional

### Epistemic Tightening (v0.6.0 — first formal review)
- Evidence-anchoring rule in epistemic-reviewer.md prevents "PCS laundering"
- Risk-type friction table in scoring-formulas.md correctly maps to orchestrator Step 4a.3b
- Threshold-hugging detection (Step 4a.4c) correctly flags base probabilities within 2% of hard caps
- "NO_EVIDENCE" declaration requirement is a valid honest-uncertainty mechanism

---

## 3. Delta Assessment (v0.6.1 → v0.8.0)

| Change | Assessment | Contradictions? | Fixes Prior Issues? |
|--------|-----------|-----------------|---------------------|
| Knowledge relocation to data dir | Positive — fixes data persistence bug | None | N/A (new) |
| Agent path updates ($KNOWLEDGE_DIR) | Positive — consistent resolution | None | N/A |
| Perplexity MCP migration | Positive — better citation density | None | N/A (new) |
| Hard stop prereq (sector-hydrate) | Positive — prevents silent failures | None | N/A |
| Q6 turnaround precision | Positive — reduces false precedents | None | N/A |
| 403 fallback via perplexity_ask | Positive — handles blocked sites | None | N/A |

**No new contradictions introduced.** All changes are internally consistent.

---

## 4. Previous Findings Status

| # | Finding (v0.5.0) | Severity | Status in v0.8.0 | Notes |
|---|---------|----------|-------------------|-------|
| 1 | Narrative framing: analyst shapes reviewer input | MEDIUM | **OPEN** | Analyst still prepares Epistemic Input section. Mitigated by evidence-anchoring rule (v0.6.0) and reviewer's independent WebSearch. Monitor. |
| 2 | Consensus echo: both agents see same news | LOW-MEDIUM | **PARTIALLY MITIGATED** | Perplexity uses different search indices than WebSearch, providing some source diversity. Evidence-anchoring rule forces citing specific sources. |
| 3 | Multiplier tail (Conf 2 = x0.70) | LOW | **ACCEPTED** | Size cap at 5% provides sufficient safety net. No false positives observed in practice. |
| 4 | Liquidity filter missing | LOW | **PARTIALLY ADDRESSED** | Screener has `market cap > $50M` filter (line 57). No ADV filter. $50M floor excludes most penny stocks but a mid-cap with thin volume could slip through. |
| 5 | Risk enrichment after epistemic review | LOW (By Design) | **CLOSED** | Demotion protocol handles post-scoring risks correctly. |

---

## 5. New Findings

### Finding 1: Scoring Formula Dual-Location Risk
**Severity:** MEDIUM (downgraded from Gemini's HIGH)
**Type:** Maintainability

The scoring formulas exist in both `scoring-formulas.md` (human reference) and `calc-score.sh` (executable). If one is updated without the other, a desync could occur.

**Why downgraded from HIGH:** The analyst prompt explicitly says "Use the calculator for ALL math in Steps 5-6" and "Show the command AND its JSON output." The agent never computes scores from the markdown description — it always calls calc-score.sh. The markdown is conceptual context, not computation instructions. The risk is a developer maintenance concern, not an active false-positive vector.

**Recommendation:** Add a version comment header to calc-score.sh: `# Implements scoring-formulas.md as of v0.8.0 — 2026-03-03`. Low priority.

### Finding 2: Sector Researcher JSON Construction
**Severity:** LOW (downgraded from Gemini's MEDIUM)
**Type:** Implementation

The sector-researcher constructs a JSON "structured prior" from synthesized Perplexity outputs. Risk of malformed JSON.

**Why downgraded:** The v0.8.0 researcher prompt explicitly says "YOU construct the JSON structured prior yourself — do not rely on Perplexity to generate JSON." Claude constructs the JSON during synthesis, not by parsing Perplexity text. Claude is highly reliable at JSON generation from structured analysis. The prior is also a sector knowledge artifact, not a scoring input — malformed JSON doesn't affect scan results.

**Recommendation:** No action needed. Monitor.

### Finding 3: No ADV (Average Daily Volume) Filter
**Severity:** LOW
**Type:** Gap

The screener filters by `market cap > $50M` but not by trading volume. A stock could theoretically pass screening despite thin daily volume, making it difficult to build a position at portfolio scale.

**Current mitigation:** The $50M market cap floor excludes the most illiquid names. The 12-position max portfolio with 3-20% sizing means even a 3% position in a $1B portfolio is $30M — well above the $50M market cap floor, which would flag obvious mismatches. Additionally, the target universe (NYSE-listed) inherently excludes the most illiquid names.

**Recommendation:** Consider adding `ADV > $500K` as a soft filter (flag, don't reject) in the screener. Low priority.

### Finding 4: Narrative Framing Remains Open
**Severity:** MEDIUM (carried forward)
**Type:** Structural

The analyst still prepares the "Epistemic Input" section that the reviewer receives. While the information barrier (no probability/score) and evidence-anchoring rule (v0.6.0) mitigate anchoring bias, the analyst's framing of risks and catalysts could subtly influence the reviewer.

**Current mitigations (strengthened since v0.5.0):**
- Evidence-anchoring rule forces reviewer to cite evidence source or declare NO_EVIDENCE
- Reviewer has independent WebSearch for verification
- Reviewer answers guidelines are specific (Q3 requires citing actual precedents)
- Risk-type friction adds an independent penalty layer

**Recommendation:** Monitor. If future scans show reviewer consistently giving high confidence to analyst-favored stocks, consider "adversarial premise injection" (force reviewer to search for 3 contradicting facts before scoring).

---

## 6. Hard Rules Audit

### Fully Enforceable (Deterministic)

| Rule | Enforcement | Robustness |
|------|-------------|------------|
| CAGR < 30% → size 0% | calc-score.sh | Unbreakable |
| Effective probability < 60% → size 0% | calc-score.sh | Unbreakable |
| Downside 80-99% → max 5% | calc-score.sh | Unbreakable |
| Downside 100% → max 3% | calc-score.sh | Unbreakable |
| Score < 45 → no investment | calc-score.sh | Unbreakable |
| PCS multiplier application | calc-score.sh | Unbreakable |
| Confidence-based size caps | calc-score.sh | Unbreakable |
| Binary outcome override | calc-score.sh | Unbreakable |
| 60%+ off ATH | Screener (data-driven) | High |
| Excluded industries | Screener (list-based) | High |
| Market cap > $50M | Screener (data-driven) | High |

### Partially Enforceable (Agent Judgment)

| Rule | Risk | Mitigation |
|------|------|------------|
| "Must be understandable" | Subjective | Low risk: excluded industries remove most opaque sectors |
| "Not in secular decline" | Agents may confuse cyclical with secular | Analyst Step 3 margin trend check (5yr) partially enforces |
| No catalysts = pass | LLMs may accept vague plans as catalysts | Analyst prompt requires specific timelines and impact |
| Heroic assumptions test | Requires comparing to 10yr historical data | calc-score.sh verifies CAGR math; margin/multiple checks rely on agent |
| Max 12 positions / 50% theme cap | Portfolio rules in orchestrator | Dependent on current-portfolio.md being up-to-date |
| Probability ceilings (65%/60%) | Agent must check conditions | Conditions are data-driven (revenue decline, negative equity, CEO tenure) |
| Risk-type friction | Orchestrator applies after PCS | Orchestrator uses judgment for confirmatory vs. additive friction |

---

## 7. Scoring System Stress Tests

All scenarios verified against actual calc-score.sh output.

### Scenario A: Safe Bore (Low Return)
- **Input:** Downside 10%, Prob 90%, CAGR 12%
- **Adj downside:** 10 * 1.05 = 10.5
- **Score:** (100-10.5)*0.45 + 90*0.40 + 12*0.15 = 40.27 + 36.0 + 1.8 = **78.07**
- **calc-score.sh output:** `total_score: 78.07` -- MATCH
- **Outcome:** REJECTED (CAGR 12% < 30% hurdle)
- **Verdict:** System correctly filters low-return safety plays despite high score.

### Scenario B: Binary Coin Flip
- **Input:** Downside 100%, Prob 50%, CAGR 100%
- **Adj downside:** 100 * 1.50 = 150
- **Score:** (100-150)*0.45 + 50*0.40 + 100*0.15 = -22.5 + 20.0 + 15.0 = **12.5**
- **calc-score.sh output:** `total_score: 12.5` -- MATCH
- **Outcome:** REJECTED (Score < 45, also Prob < 60%)
- **Verdict:** Non-linear penalty curve devastates total-loss scenarios. Even 100% CAGR can't save it.

### Scenario C: Ideal Turnaround
- **Input:** Downside 25%, Prob 75%, CAGR 40%
- **Adj downside:** 25 * 1.125 = 28.12
- **Score:** (100-28.12)*0.45 + 75*0.40 + 40*0.15 = 32.35 + 30.0 + 6.0 = **68.35**
- **calc-score.sh output:** `total_score: 68.35` -- MATCH
- **Outcome:** DEPLOY (65-74 band → 10-15% size)
- **Verdict:** This is the "sweet spot" profile the strategy targets.

### Scenario D: Heartbreaker with PCS (from v0.5.0 review)
- **Input:** Downside 30%, Prob 70%, CAGR 50%, Confidence 3 (x0.85)
- **Effective prob:** 70 * 0.85 = 59.5%
- **Outcome:** REJECTED (effective prob 59.5% < 60% hard floor)
- **Verdict:** Confidence 3 is the "killer" tier — a standard 70% probability trade is rejected with 2 epistemic "No" answers.

### Scenario E: Ceiling + PCS Double Penalty
- **Input:** 3yr+ revenue decline (ceiling 65%), Confidence 3 (x0.85)
- **Effective prob:** 65 * 0.85 = 55.25%
- **Outcome:** REJECTED (effective prob 55.25% < 60%)
- **Verdict:** Correct double-penalty. Shrinking business + imperfect epistemic clarity = no investment.

---

## 8. Agent Prompt Quality Assessment

| Agent | Clarity | Completeness | Drift Resistance | Overall | Notes |
|-------|---------|-------------|------------------|---------|-------|
| Orchestrator | 9 | 10 | 9 | **9.3** | Extremely detailed flow with numbered steps. Risk-type friction, threshold-hugging detection, sensitivity tables all specified. |
| Screener | 8 | 8 | 9 | **8.3** | Clear pass/fail criteria. Binary nature limits drift. Missing ADV filter. |
| Analyst | 7 | 9 | 7 | **7.7** | Most complex prompt — bears burden of converting qualitative research to quantitative inputs. "SCORING DISCIPLINE" section mitigates score-shopping but probability estimation remains subjective. |
| Epistemic Reviewer | 8 | 9 | 8 | **8.3** | Evidence-anchoring rule (v0.6.0) significantly improved rigor. Information barrier well-maintained. |
| Sector Coordinator | 8 | 8 | 8 | **8.0** | Clean orchestration. Perplexity migration well-specified. |
| Sector Researcher | 7 | 8 | 7 | **7.3** | 8-query structure is well-defined. Q6 turnaround precision fix is good. Relies on Perplexity output quality. |

**Weakest link:** Analyst — not because its prompt is poor (it's comprehensive), but because it carries the heaviest subjective burden. The probability estimate is the single most impactful input in the system, and it relies on analyst judgment. All other guardrails (PCS, ceilings, friction) are downstream corrections, not replacements.

---

## Reviewer Corrections

Gemini made several claims that were verified against the actual codebase:

| Gemini Claim | Actual Finding | Correction |
|-------------|---------------|------------|
| "No liquidity filter exists" — rated CRITICAL | Screener has `market cap > $50M` filter (screener.md line 57) | Downgraded to LOW. Missing ADV, but market cap floor exists. |
| "Logic Desynchronization" — rated HIGH | Analyst is explicitly instructed to use calc-score.sh for ALL math, never compute from markdown | Downgraded to MEDIUM (maintainability concern, not active risk). |
| "Perplexity JSON Fragility" — rated MEDIUM | Researcher prompt says "YOU construct the JSON structured prior yourself" — Claude generates JSON, not parsed from Perplexity text | Downgraded to LOW. |
| Gemini referenced file paths like `prompts/analyst/scoring-formulas.md` and `agents/orchestrator/pipeline.py` | These paths don't exist. System uses markdown agent definitions, not Python scripts. | Incorrect path references ignored. |
| Gemini's "false positive scenario" involved a crypto miner with 50% weekly momentum | The screener requires 60%+ DOWN from ATH, not momentum. Excluded industries would also filter most crypto/AI plays. | Scenario is unrealistic under current system rules. |
| Gemini recommended removing math from scoring-formulas.md | The analyst needs conceptual understanding to estimate inputs (probability, downside). The markdown is reference context, not computation instructions. | Recommendation rejected. |

---

## Critical Findings Summary

| # | Finding | Severity | Status | Action Required |
|---|---------|----------|--------|-----------------|
| 1 | Narrative framing: analyst shapes reviewer input | MEDIUM | OPEN (carried from v0.5.0) | Monitor; evidence-anchoring rule (v0.6.0) mitigates |
| 2 | Scoring formula dual-location (md + sh) | MEDIUM | NEW | Add version sync comment to calc-score.sh. Low priority. |
| 3 | No ADV filter in screener | LOW | OPEN (carried from v0.5.0) | Consider soft ADV > $500K filter. Low priority. |
| 4 | Consensus echo risk | LOW-MEDIUM | PARTIALLY MITIGATED | Perplexity + WebSearch source diversity helps |
| 5 | Multiplier tail (Conf 2 = x0.70) | LOW | ACCEPTED | Size cap at 5% is sufficient safety net |

---

## Comparison to Previous Versions

| Dimension | v0.5.0 (epistemic layer) | v0.6.0 (epistemic tightening) | v0.8.0 (current) |
|-----------|-------------------------|-------------------------------|-------------------|
| Arithmetic accuracy | calc-score.sh (10/10) | Same | Same |
| Valuation consistency | Discount schedule + consistency rule | Same | Same |
| Probability calibration | Ceilings + PCS multiplier | + Evidence anchoring + risk-type friction + threshold-hugging | Same |
| Epistemic rigor | PCS + independent reviewer | + NO_EVIDENCE declaration + friction modifiers | Same |
| Sector knowledge | Manual/ad-hoc | Same | Structured pipeline via Perplexity MCP |
| Data persistence | Plugin cache (fragile) | Same | Data dir (persistent) |
| Research quality | WebSearch only | Same | Perplexity MCP with citations + WebSearch fallback |

---

## Verdict

**APPROVED FOR DEPLOYMENT.**

The v0.8.0 system is the most architecturally mature version to date. The knowledge relocation fixes a real data persistence vulnerability, and the Perplexity migration improves research citation quality. The core scoring logic is unchanged and remains mathematically sound — all stress tests pass exactly.

No CRITICAL or HIGH findings. The two MEDIUM findings (narrative framing and formula dual-location) are maintainability/monitoring concerns, not active capital-at-risk issues.

The system remains structurally conservative — it will reject many genuine opportunities due to epistemic uncertainty. This is by design: "Discipline beats talent. Patience is an edge."

**Overall Confidence: 9.0/10**

---

*Review completed 2026-03-03. Gemini Pro deep analysis of EdenFinTech Scanner v0.8.0.*
