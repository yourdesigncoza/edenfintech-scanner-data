# Sector Hydration Benchmark Prompts

Use these to evaluate deep research services (Perplexity, ChatGPT Deep Research, Grok, etc.).
Replace `{sub-sector}` with any sub-sector name (e.g., "Regional Banks", "Specialty Chemicals", "Medical Devices").

**Best queries for benchmarking:** Q4 (Failure Patterns) and Q6 (Turnaround Precedents) — hardest to answer, require specific companies/dates/outcomes, easy to verify accuracy.

**Baseline:** Gemini Deep Research on "Regional Banks" Q1 returned 54 cited sources in 21 minutes.

---

## Query 1 — Structure

```
Structural characteristics of {sub-sector} companies: revenue model, capital intensity,
leverage structure, typical cyclicality, margin profiles (gross/operating/FCF), competitive
dynamics, switching costs, barriers to entry. Return as structured table with columns:
Characteristic | Typical Range | Key Drivers.
```

## Query 2 — Regulatory Risk

```
Regulatory and political risk for {sub-sector}: list all relevant US regulators with
jurisdiction scope, discretion level (rules-based vs. discretionary), historical intervention
examples (with company names, dates, and outcomes), binary regulatory risks that could
materially change a company's value. Structured table format.
```

## Query 3 — Macro Sensitivity

```
Macro sensitivity of {sub-sector}: sensitivity to interest rates, credit cycles,
unemployment, liquidity conditions, inflation, yield curve shape, commodity prices,
trade policy. Classify each factor as Low/Moderate/High sensitivity with 1-line rationale
and historical example.
```

## Query 4 — Failure Patterns

```
Historical failure patterns in {sub-sector} over the last 40 years. Categorize each as
operational/liquidity/regulatory/fraud/contagion. For each: was failure gradual or binary?
What were the warning signs? Include company names, years, and outcomes. List at least
5-8 examples.
```

## Query 5 — Binary Triggers

```
Binary risk triggers specific to {sub-sector}: events that can cause sudden, dramatic
value destruction (>50% loss). Examples: regulatory shutdown, capital adequacy failure,
liquidity crisis, rating downgrade spiral, counterparty collapse, patent expiry, FDA
rejection. Rate each trigger: Rare/Occasional/Structural. Include historical examples.
```

## Query 6 — Turnaround Precedents

```
Turnaround precedent analysis for {sub-sector}: Are downturns in this sub-sector
typically cyclical and recoverable, or structurally impairing? What is the average
recovery timeline? What is the 20-year survivorship rate for distressed companies?
Provide 3-5 specific turnaround examples with: company name, period, initial situation,
actions taken, outcome (success/failure/partial), timeline to recovery, stock price
trajectory (trough to recovery).
```

## Query 7 — Epistemic Profile

```
Epistemic risk classification for {sub-sector} mapped to these 5 questions:
(1) Is risk primarily operational/modelable? (2) Is regulatory discretion minimal?
(3) Are there strong historical precedents for turnarounds? (4) Are outcomes typically
non-binary (gradient)? (5) Is macro/geopolitical exposure limited?
Answer each Yes/No with supporting evidence. Also assess: How predictable are outcomes
in this sub-sector? Rate epistemic stability 1-5 (5 = highly predictable).
```

## Query 8 — Structured Prior (JSON)

```
For the {sub-sector}, return a JSON object with these fields:
- sector: GICS sector name
- sub_sector: specific sub-sector name
- cyclicality: "low" / "moderate" / "high" / "extreme"
- regulatory_discretion: "minimal" / "moderate" / "high" / "extreme"
- binary_risk_level: "low" / "moderate" / "high"
- macro_dependency: "low" / "moderate" / "high"
- precedent_strength: "strong" / "moderate" / "weak" / "none"
- typical_valuation_method: primary valuation approach (e.g., "P/TBV", "EV/EBITDA", "P/FCF")
- fcf_multiple_baseline: typical FCF multiple range or "N/A" if not applicable
- epistemic_stability_score: 1-5
- suggested_pcs_friction: 0 / -1 / -2 with reason
- suggested_position_cap: percentage or "none"
Return ONLY the JSON, no commentary.
```
