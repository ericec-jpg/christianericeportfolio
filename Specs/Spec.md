# FX Hedge Model – Stage 2 Quantitative Specification (Reusable Template)

**Created by:** [Name]  
**Updated by:** [Name]  
**Date Created:** [YYYY-MM-DD]  
**Date Updated:** [YYYY-MM-DD]  
**Version:** [1.0]  
**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO / Director of Treasury

**Purpose:** Define a clear, reproducible analytical plan for building and evaluating FX hedge alternatives for a foreign-currency receivable/payable. Keep formulas conceptual (no cell refs). Another analyst—or an AI assistant—should be able to implement this directly.

---

## 1) Problem Statement
**Business context (fill in):**  
- **Exposure type:** [Receivable / Payable]  
- **Foreign currency & notional:** [e.g., EUR, JPY, GBP; amount TBD]  
- **Timing:** [Valuation date, settlement date, tenor]  
- **Objective:** [Protect USD value / reduce cashflow variance / preserve upside]  
- **Decision lens:** Corporate Treasury risk policy; budget certainty vs. optionality.

> This section restates the exposure and the goal in professional language: “We will quantify and compare hedge structures to stabilize domestic-currency proceeds while documenting trade-offs among certainty, optionality, and cost.” :contentReference[oaicite:0]{index=0}

---

## 2) Inputs (Known Variables)
Create a clean input table (labels become named ranges / prompt parameters later). :contentReference[oaicite:1]{index=1}

| Variable     | Description                            | Unit        | Example/Placeholder | Source            |
|--------------|----------------------------------------|-------------|---------------------|-------------------|
| `FC_AMT`     | Foreign-currency exposure               | FC units    | [TBD]               | Internal contract |
| `S0`         | Spot rate (DC/FC)                      | DC per FC   | [TBD]               | Market data       |
| `F0_T`       | Forward rate for tenor T               | DC per FC   | [TBD]               | Market data       |
| `r_DC_T`     | Domestic rate for tenor T              | % (annual)  | [TBD]               | Market data       |
| `r_FC_T`     | Foreign rate for tenor T               | % (annual)  | [TBD]               | Market data       |
| `t`          | Time to maturity                        | years       | [TBD]               | Derived           |
| `K_put`      | FX put strike (on FC)                  | DC per FC   | [TBD]               | Analyst choice    |
| `K_call`     | FX call strike (on FC)                 | DC per FC   | [TBD]               | Analyst choice    |
| `Prem_put`   | Put premium (per FC unit)              | DC per FC   | [TBD]               | Dealer quote      |
| `Prem_call`  | Call premium (per FC unit)             | DC per FC   | [TBD]               | Dealer quote      |
| `Txn_costs`  | Estimated transaction costs (if used)  | DC          | [Optional]          | Policy/assumption |

**Data sourcing protocol:** identify vendor (ECB/FED/reuters/bloomberg), timestamp, and quote basis (bid/mid/ask).

---

## 3) Assumptions & Constraints
Document conventions to ensure reproducibility. :contentReference[oaicite:2]{index=2}  
- Quotation basis: **DC per FC** (e.g., USD per EUR).  
- Interest rates annualized on a [simple/ACT-360/ACT-365] basis; tenor aligned to settlement.  
- Premiums paid upfront in DC; time value ignored beyond premium payment unless noted.  
- Transaction costs, credit charges, and accounting/tax impacts **excluded** (unless specified).  
- Hedge sized to 100% of exposure unless a partial hedge policy is noted.  
- All scenarios evaluated at maturity \(S_T\); interim MtM not part of Stage 2 scope.

---

## 4) Calculation Flow (Logic & Sequence, not cell formulas)
Describe order of operations so any analyst/AI can implement the model. :contentReference[oaicite:3]{index=3}

**A. Forward Hedge**  
1. Confirm tenor and size vs. `FC_AMT`.  
2. Compute locked DC proceeds at `F0_T` (certainty benchmark).  
3. Note credit usage / collateral, but exclude from Stage 2 numerics.

**B. Money-Market (Synthetic Forward) Hedge**  
4. Present parity check: convert via spot today, invest/borrow at `r_FC_T`/`r_DC_T` to maturity; compare implied synthetic forward to `F0_T`.  
5. Compute DC proceeds from MM hedge at maturity; reconcile to forward economics (expect near-parity under clean assumptions).

**C. Options (e.g., Protective Put or Collar on FC)**  
6. For a **put**: compute payoff at maturity across \(S_T\) grid; net of `Prem_put`.  
7. For a **collar**: long put `K_put`, short call `K_call`; net premiums `Prem_put` – `Prem_call`; cap upside above `K_call`.  
8. Translate option payoffs into DC proceeds for the exposure (receivable/payable mapping).  
9. Summarize trade-offs: certainty (forward/MM) vs. optionality (options) vs. cost (premiums).

**D. Comparison & Summary**  
10. Build a comparison table at the **base case** \(S_T = S0\) and across the scenario grid (see Sensitivity).  
11. Identify which hedge best aligns with objective and constraints.

---

## 5) Outputs (What the model should produce)
List outputs to appear in the spreadsheet and your Stage 5 discussion. :contentReference[oaicite:4]{index=4}

| Output          | Description                               | Format         | Purpose                         |
|-----------------|-------------------------------------------|----------------|---------------------------------|
| `USD_forward`   | DC proceeds under forward                  | Scalar         | Certainty benchmark             |
| `USD_mm`        | DC proceeds under money-market             | Scalar         | Parity cross-check              |
| `USD_put`       | DC proceeds under protective put           | Table (grid)   | Downside protection view        |
| `USD_collar`    | DC proceeds under collar                   | Table (grid)   | Cost-controlled optionality     |
| `Chart_outcomes`| Outcomes vs. \(S_T\) for all hedges        | Line chart     | Visual comparison               |
| `Summary_note`  | 1–2 paragraph takeaway (business-ready)    | Text           | Exec brief for CFO              |

---

## 6) Sensitivity Plan
Define how you will stress test and visualize the hedges. :contentReference[oaicite:5]{index=5}  
- **Spot path:** vary \(S_T\) from **0.95×S0 to 1.05×S0** in 0.01 increments; compute DC proceeds for each hedge at each step.  
- **(Optional) Rate shift:** bump `r_DC_T` and `r_FC_T` by ±50 bps to show forward/MM sensitivity.  
- **Deliverables:** comparison table + single overlay line chart of outcomes by hedge; highlight break-evens and floors/caps.  
> Sensitivity evidences robustness and supports a defensible recommendation. :contentReference[oaicite:6]{index=6}

---

## 7) Limitations & Next Steps
Call out scope boundaries and set up Stage 3. :contentReference[oaicite:7]{index=7}  
**Limitations:** ignores bid/ask spreads, funding basis, volatility smiles, counterparty credit, hedge accounting and tax.  
**Next Steps (Stage 3 handoff):**  
1. Implement this spec in Excel with named inputs/outputs matching section 2 & 5.  
2. Build scenario grid and charts per section 6.  
3. Validate MM parity vs. dealer forward.  
4. Prepare to draft AI prompt using the **Calculation Flow** as instruction blocks.

---

## Appendix A – Variable Dictionary (for consistency)
- **DC** = Domestic currency; **FC** = Foreign currency.  
- Use short, standardized variable names across model, prompt, and memo (e.g., `S0`, `F0_T`, `r_DC_T`, `r_FC_T`). :contentReference[oaicite:8]{index=8}

## Appendix B – Stage Alignment (Why this spec matters)
- **Stage 3:** Inputs/outputs map to spreadsheet fields.  
- **Stage 4:** Calculation Flow becomes AI prompt steps.  
- **Stage 5:** Outputs power the final recommendation. :contentReference[oaicite:9]{index=9}

> Write like a professional: clear, consistent, reproducible, executive-relevant. :contentReference[oaicite:10]{index=10}
