# EdenFinTech Scanner v0.8.0 (Post-Todos) — Deep System Review

> **Auditor:** Gemini Pro (deep analysis mode)
> **Date:** 2026-03-04
> **Scope:** Delta review from gemini-review-v0.8.0
> **Sources:** All knowledge files, agent definitions, calc-score.sh, previous audits
> **Changes since last review:** 5 files, 202+/21- (3 todos: Phase A.5, probability banding, 20% CAGR exception gate)

---

## Executive Summary

Version 0.8.0 post-todo adds three features: (1) Phase A.5 research audit for sector researcher with gap detection/remediation, (2) probability calibration with 50/60/70/80 banding and base-rate anchoring from sector Q6 data, (3) 20% CAGR exception candidates routed to human review table instead of auto-approval.

The Phase A.5 implementation is robust — `CONFIRMED_ABSENCE`, audit-patch.md, and the follow-up cap are well-designed. The probability banding introduces intentional conservatism that limits throughput at low confidence levels. The exception gate correctly prevents LLM auto-approval of borderline hurdle cases.

One genuine design tension exists around the no-sector-knowledge default (50% band), which is restrictive but arguably correct. No critical implementation bugs found.

---

## 1. System Coherence

All three changes are internally consistent across files:
- **Banding**: scoring-formulas.md defines bands → analyst.md enforces them with output format → orchestrator.md validates (step 4d) and rounds non-compliant values
- **Exception**: strategy-rules.md defines human gate → analyst.md labels candidates → orchestrator.md routes to three buckets → report template includes Pending Human Review section
- **Phase A.5**: sector-researcher.md defines audit → coordinator.md passes current_date → knowledge files unchanged (no contradictions)

**No contradictions found** between knowledge files and agent instructions.

## 2. Implementation Quality

### Phase A.5: Research Audit — STRONG
- `CONFIRMED_ABSENCE` prevents hallucination of missing data
- Audit-patch.md keeps Phase B context lean
- Follow-up cap (3 for sub-sector, 2 for regulatory) prevents infinite loops
- Context-injection requirement prevents duplicate source returns

### Probability Banding — FUNCTIONAL WITH KNOWN TRADEOFFS
- Bands force discrete choices, eliminating fake precision (67% → 70%)
- Base-rate anchoring from sector Q6 grounds estimates in empirical data
- Likert modifiers provide structured adjustment (+10/0/-10 per factor)
- Orchestrator step 4d catches non-compliant values

### 20% CAGR Exception Gate — CORRECT
- Full analysis still runs for exception candidates
- Three-bucket routing (Ranked / Exception / Rejected) is clean
- Report template includes all data human needs to decide

## 3. Delta Assessment

### calc-score.sh vs Exception Workflow
Gemini flagged this as CRITICAL — **downgraded to LOW**. The script correctly outputs `size=0%` for CAGR<30%. Exception candidates are routed by the orchestrator based on the analyst's `EXCEPTION CANDIDATE` label, not the size output. The human review table displays Score/CAGR/Downside/Prob; size is irrelevant until human approves. No code change needed.

### No-Sector-Knowledge Default Band
Gemini flagged as HIGH — **downgraded to MEDIUM**. The default 50% band applies only when no sector Q6 data exists AND no precedents found. Likert modifiers still apply: default 50% + Strong management (+10%) = 60% band. Only fails if all three modifiers are Neutral, which correctly signals "no positive evidence." This is conservative by design, not a bug.

### Banding Clipping Discontinuities
**MEDIUM — accepted tradeoff.** A 1% difference in raw estimate (64% vs 66%) maps to different bands (60 vs 70). This is the deliberate cost of eliminating fake precision. The stress test confirms:
- At confidence 3/5 (multiplier 0.85), only the 80% band passes the 60% effective probability threshold
- This means high epistemic uncertainty (2 "No" answers) requires near-certainty in the base case — intentionally conservative

## 4. Previous Findings Status

| # | Finding | Severity | Prior Status | Current Status |
|---|---------|----------|-------------|---------------|
| 1 | Narrative framing: analyst shapes reviewer input | MEDIUM | OPEN | OPEN — unchanged |
| 2 | Scoring formula dual-location (md + sh) | MEDIUM | NEW | OPEN — still dual-location, not resolved |
| 3 | No ADV filter in screener | LOW | OPEN | OPEN — unchanged |
| 4 | Consensus echo risk | LOW-MEDIUM | PARTIALLY MITIGATED | FURTHER MITIGATED — Phase A.5 breaks search bubbles |
| 5 | Multiplier tail (Conf 2 = x0.70) | LOW | ACCEPTED | ACCEPTED |

## 5. New Findings

| # | Finding | Severity | Action Required |
|---|---------|----------|-----------------|
| 6 | Banding clipping creates 10% discontinuities at band boundaries | MEDIUM | Accepted tradeoff — document in methodology notes |
| 7 | No-sector-knowledge path requires strong Likert signals to pass | MEDIUM | Document in orchestrator's "proceed without" warning |
| 8 | Exception candidate label relies on string matching | LOW | Standardize label format; orchestrator already validates |
| 9 | Phase A.5 follow-up cap (3) might be tight for complex sectors | LOW | Monitor in practice; easy to adjust later |

## Reviewer Corrections

Gemini's initial review contained these inaccuracies:
1. **Finding 1 rated CRITICAL** — Gemini claimed calc-score.sh creates a "deadlock" for exception candidates. Incorrect: the orchestrator routes based on analyst labels, not calc-score.sh size output. The 0% size is intentionally correct for these candidates. **Corrected to LOW.**
2. **Finding 2 rated HIGH** — Gemini missed that Likert modifiers apply before banding. A stock with one Strong modifier escapes the 50% default. Only truly undifferentiated stocks (all Neutral) get trapped. **Corrected to MEDIUM.**
3. **Prior Finding #2 "RESOLVED"** — Gemini incorrectly claimed scoring formula dual-location was resolved. Nothing changed; formulas still exist in both scoring-formulas.md and calc-score.sh. **Corrected to OPEN.**

## 6. Scoring System Stress Tests

### Test 1: Exception candidate (CAGR 25%, strong thesis)
- Downside: 30%, Probability: 70% (banded), CAGR: 25%
- calc-score.sh score: adj_downside=34.5, risk=29.48, prob=28.0, return=3.75 → **Score: 61.23**
- calc-score.sh size: 0% (CAGR < 30% hard cap) — CORRECT, goes to human review table

### Test 2: No sector knowledge, strong stock
- Default band: 50%, Likert: Management Strong (+10), Balance Strong (+10), Market Neutral (0)
- Net: 70% → 70% band. Confidence 4/5 → multiplier 0.95
- Effective: 70 * 0.95 = 66.5% → PASSES 60% threshold
- System works correctly even without sector hydration when stock has clear positives

### Test 3: Band boundary sensitivity
- Analyst A: raw 64% → 60% band. Confidence 3/5 → effective 51% → REJECTED
- Analyst B: raw 66% → 70% band. Confidence 3/5 → effective 59.5% → REJECTED
- Analyst C: raw 76% → 80% band. Confidence 3/5 → effective 68% → PASSED
- Observation: At confidence 3/5, only 80% band passes. This is intentional — high epistemic uncertainty should demand high base-case conviction.

### Test 4: Maximum conservatism stack
- No sector knowledge, default 50% band, all Likert Neutral, confidence 2/5
- Effective: 50 * 0.70 = 35% → REJECTED (as expected — maximum uncertainty = no investment)

### Test 5: Probability ceiling interaction with banding
- Raw estimate: 80% band, but 3yr decline ceiling caps at 65%
- Ceiling applied: 65% (overrides band). Confidence 4/5 → effective 61.75% → PASSES barely
- Shows ceilings correctly override bands when applicable

## 7. Comparison to Previous Version

| Dimension | v0.8.0 (pre-todo) | v0.8.0 (post-todo) |
|-----------|-------------------|---------------------|
| Probability precision | 0-100% continuous | 50/60/70/80 banded |
| Base-rate source | Analyst judgment | Sector Q6 empirical data |
| 20% CAGR exception | Auto-approved by analyst | Human gate required |
| Sector research quality | Single-pass Perplexity | Phase A.5 audit + remediation |
| Throughput | Higher (any probability) | Lower (banding + confidence filter) |
| False positive risk | Higher | Lower |

## Verdict

**APPROVED WITH CONDITIONS.**

The three features are well-implemented and internally consistent. No critical bugs. The probability banding will reduce scan throughput (by design), but the tradeoff is appropriate for the strategy's conservative philosophy.

**Conditions:**
1. Document the banding clipping tradeoff in methodology notes (finding #6)
2. Update orchestrator's "proceed without sector knowledge" warning to note Likert modifier dependency (finding #7)

**Overall Confidence: 8.5/10**

The 0.5 drop from the prior 9.0 reflects the added complexity of banding + exception routing, which creates more surfaces for LLM interpretation variance. The core scoring math remains deterministic and correct.

---

## 8. Follow-Up Deep Dive (Gemini Pro, high reasoning)

### Fix Specifics for MEDIUM+ Findings

**Finding #1 (Narrative framing):** Gemini suggests decoupling epistemic reviewer input from analyst narrative — feed raw data + sector researcher audit log instead of analyst's synthesis. **Reviewer note:** The current design intentionally feeds analyst-curated thesis/risks/catalysts (not the full narrative). The epistemic reviewer has WebSearch for independent verification and evidence-anchoring rules requiring cited sources or `NO_EVIDENCE`. Partial fix already in place; full decoupling would require restructuring the orchestrator's data flow between agents. Severity remains MEDIUM — monitor for drift rather than restructure.

**Finding #2 (Dual-location):** Gemini suggests migrating calc-score.sh to Python or auto-generating docs from code. Both are valid long-term approaches. **Practical fix:** Add a version comment to both files (e.g., `# Scoring v0.8.0 — must match scoring-formulas.md`) and include a manual diff step in the `/gemini-review` skill. Low effort, reduces drift risk.

**Finding #6 (Banding clipping):** Gemini suggests adding 5% interim bands (55/65/75). **Rejected** — this contradicts the design goal. The 10% jumps are intentional: they force analysts to commit to discrete confidence levels rather than splitting hairs. The interaction with PCS multipliers is the designed conservatism filter.

**Finding #7 (No-sector-knowledge default):** Gemini suggests a "Generalist Premium" (base rate 55% if Net Cash > 0 and ROIC > 15%). **Interesting but premature** — would add complexity for an edge case. Current design: 50% default + Likert modifiers is sufficient for quality stocks. Document the Likert escape path in orchestrator's "proceed without sector knowledge" warning.

### Independent Math Verification

All 5 stress test scenarios independently verified. **No discrepancies found.**

| Test | Reported | Verified | Match |
|------|----------|----------|-------|
| 1: Exception candidate | Score 61.23, size 0% | 29.475 + 28.0 + 3.75 = 61.225 ✓ | Yes |
| 2: No sector, 2 Strong | Effective 66.5%, PASSES | 70 × 0.95 = 66.5 ✓ | Yes |
| 3: Band boundary (Conf 3) | Only 80% passes | 60×0.85=51, 70×0.85=59.5, 80×0.85=68 ✓ | Yes |
| 4: Max conservatism | Effective 35%, REJECTED | 50 × 0.70 = 35 ✓ | Yes |
| 5: Ceiling + banding | Effective 61.75%, PASSES | 65 × 0.95 = 61.75 ✓ | Yes |

### Most Likely False Positive Scenario

Gemini identifies a "Semantic Drift / Friction Bypass" where the analyst misclassifies a Legal risk as Operational to avoid the -2 confidence friction penalty, then bumps a Likert modifier to cross a threshold.

**Reviewer assessment:** The risk is real but mitigated by two existing constraints:
1. Analyst.md scoring discipline: "Estimate your 3 inputs ONCE. Do NOT revise inputs to produce a 'better' score"
2. The epistemic reviewer independently answers Q1 ("Is risk primarily operational?") — if legal risk is visible, the reviewer would answer "No" regardless of analyst classification

The real vulnerability is subtler: an analyst could sincerely misclassify ambiguous risk (e.g., "regulatory compliance costs" as operational rather than regulatory). This is inherent to any classification system and is partially addressed by the epistemic reviewer's independence. **No code fix available** — this is an irreducible judgment call.

### Agent Prompt Quality Ratings

| Agent | Gemini Rating | Adjusted Rating | Notes |
|-------|--------------|-----------------|-------|
| Orchestrator | 8/10 | **8/10** | Agree — strong routing logic, boolean-flag-based |
| Screener | 5/10 | **6/10** | ADV missing is known/accepted (LOW). Otherwise solid quantitative filter chain |
| Analyst | 6/10 | **7/10** | Complex but well-constrained. Scoring discipline + banding + output format template reduce drift. Likert subjectivity is the main weakness |
| Epistemic Reviewer | 6/10 | **7/10** | Gemini underrates it. Evidence-anchoring rule + WebSearch + `NO_EVIDENCE` declaration are strong anti-drift mechanisms |
| Sector Researcher | 7/10 | **7/10** | Agree — Phase A.5 is well-designed. Follow-up cap is pragmatic |
| Sector Coordinator | — | **7/10** | Not rated by Gemini. Clean orchestration with date passthrough |

**Weakest link:** Analyst (Likert subjectivity + risk classification judgment). Screener is #2 due to missing ADV, but that's a feature gap not a prompt quality issue.

### Delta Assessment — Interaction Effects

Gemini flags a potential interaction between banding and PCS multipliers: at confidence 3/5, only the 80% band passes the 60% effective probability threshold. This is **intentionally conservative** — it means stocks with meaningful epistemic uncertainty need near-certainty in the base case to receive capital. This is the system's design philosophy, not a bug.

**CONFIRMED_ABSENCE:** Gemini claims it acts as a "get out of jail free" card. **Incorrect** — it's a transparent label that appears in the audit-patch.md, visible in the final report. It acknowledges missing data rather than hallucinating it. The analyst still decides how to weight the gap.

**String matching for EXCEPTION CANDIDATE:** Valid LOW concern. The orchestrator already validates this (step 3b routing logic). Could be hardened with regex but low priority given single-format enforcement in analyst.md.

## Follow-Up Reviewer Corrections

1. **File paths wrong** — Gemini references `prompts/` directory (should be `agents/`) and `docs/scoring-formulas.md` (should be `knowledge/scoring-formulas.md`). No such directories exist.
2. **Banding rated "FAILURE"** — Overstated. Gemini's 5% increment suggestion contradicts the deliberate design goal of eliminating fake precision. The conservatism is the feature, not a bug.
3. **Epistemic reviewer rated 6/10 "rubber stamp"** — Underrated. The agent has evidence-anchoring rules, `NO_EVIDENCE` declaration requirement, and independent WebSearch capability. It's not a rubber stamp.
4. **CONFIRMED_ABSENCE as "get out of jail free"** — Overstated. It's a transparent gap acknowledgment label, not a neutral-scoring mechanism. Visible in audit output and final report.
5. **Screener rated 5/10** — Slightly harsh. ADV is a known LOW finding (not critical for the strategy's low-turnover, concentrated approach). Prompt quality is otherwise solid.

---

*Follow-up deep dive completed 2026-03-04. Gemini Pro (high reasoning) with reviewer corrections.*

---

*Review completed 2026-03-04. Gemini Pro deep analysis of EdenFinTech Scanner v0.8.0 (post-todos).*
