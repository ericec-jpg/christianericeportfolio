# Stage 2 – FX Hedge Model Technical Specification (ERICE)

**Created by:** Christian Erice  
**Updated by:** Christian Erice  
**Date Created:** 2025-11-07  
**Date Updated:** 2025-11-07  
**Version:** 1.0  
**LLM Support (if used):** GPT-5 (assistive drafting only)

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO, Director of Treasury  

**Purpose:** Provide a clear, reproducible quantitative plan to build an Excel model that evaluates hedge alternatives for our EUR receivable and supports a Stage 5 recommendation.

---

## 1) Problem Statement

We expect to receive **€11,494,253** from a European enterprise client on **25 Oct 2026** (12-month horizon). Translating at today’s **EUR/USD spot 1.0875** supports our USD cash-flow target of ~$12.5mm. FX volatility and policy divergence (Fed vs. ECB) introduce downside risk to USD proceeds if the dollar strengthens.  
**Objective:** design and implement a model that **quantifies and compares** three hedge families (Forward, Options, Money-Market) to (i) **stabilize USD cash inflows** around plan, (ii) **preserve upside selectively**, and (iii) **minimize balance-sheet and liquidity frictions**.

**Decision context:** Corporate treasury; outputs will inform CFO guidance and quarterly cash planning.

---

## 2) Inputs (Known Variables)

| Variable | Description | Unit | Example (from Stage 1) | Source |
|---|---|---:|---:|---|
| `FC_AMT` | Foreign-currency receivable | EUR | 11,494,253 | Contract/AR |
| `S0` | Spot EUR/USD | USD per EUR | 1.0875 | Market (ECB/Reuters) |
| `F0_1Y` | 12-mo forward EUR/USD | USD per EUR | 1.0910 | Market |
| `r_USD_12M` | USD 12-mo rate (proxy: OIS) | % p.a. | 4.85% | Market |
| `r_EUR_12M` | EUR 12-mo rate (proxy: Euribor) | % p.a. | 3.15% | Market |
| `t` | Time to maturity | years | 1.00 | Derived |
| `K_put` | EUR put strike | USD/EUR | 1.0900 | Analyst set |
| `K_call` | EUR call strike | USD/EUR | 1.1300 | Analyst set |
| `Prem_put` | Put premium (per EUR) | USD/EUR | 0.0170 | Dealer quote |
| `Prem_call` | Call premium (per EUR) | USD/EUR | 0.0120 (recv) | Dealer quote |
| `Txn_costs` | Est. round-trip costs | bps | 2–5 | Policy/ops |
| `Acct_rules` | Hedge accounting policy flag | text | CF hedge | Accounting |
| `Credit_line` | Available hedge capacity | USD | [input] | Treasury |
| `Plan_USD` | Budget anchor | USD | 12,500,000 | FP&A |

**Conventions** (naming & units): all FX quotes in **USD per EUR**; rates **annualized simple** unless noted; premiums paid/received **up-front in USD**.

---

## 3) Assumptions & Constraints

- Rates reflect current market levels; **no intra-period resets**.  
- **No default/credit events**; counterparty is investment grade.  
- **Transaction costs excluded** from base case; tested in sensitivity.  
- **No basis or cross-currency basis** assumed in base case.  
- **Day-count**: ACT/360 for money-market checks (document in model header).  
- **Hedge accounting** feasibility to be confirmed separately (qualitative flag only in Stage 2).  
- **Premium timing**: options premiums paid today (t=0) in USD.

---

## 4) Calculation Flow (logic, not cell math)

**A. Base Data & Sanity Checks**  
1. Load inputs (`FC_AMT`, `S0`, `F0_1Y`, `r_USD_12M`, `r_EUR_12M`, `t`).  
2. **Covered Interest Parity (CIP) check**: compare observed `F0_1Y` vs. `S0*(1+r_USD_12M)/(1+r_EUR_12M)`; report forward basis delta (bps).  
3. Record **Plan_USD** for variance analysis (target anchoring).

**B. Hedge 1 – Forward Contract**  
4. Compute **locked USD**: `USD_forward = FC_AMT * F0_1Y`.  
5. Report **variance to plan**: `USD_forward – Plan_USD`.  
6. Note credit usage and settlement cash-flow timing (no premium).

**C. Hedge 2 – Money-Market (Synthetic Forward)**  
7. EUR present value: `EUR_PV = FC_AMT / (1 + r_EUR_12M*t)`.  
8. Convert to USD today at `S0`; fund via **USD borrowing** at `r_USD_12M`.  
9. USD at maturity: `USD_mm = EUR_PV * S0 * (1 + r_USD_12M*t)`.  
10. Compare `USD_mm` to `USD_forward` (should align apart from basis/txn costs).

**D. Hedge 3 – Options (Protective Put or Collar)**  
11. **Put-only floor**: For terminal spot `ST`, USD receipts = `FC_AMT * max(ST, K_put)` less premium (in USD).  
12. **Cost-reduced collar**: buy `K_put`, sell `K_call`; net premium = `Prem_put – Prem_call`.  
13. For each `ST` in a scenario set (see §6), compute USD payoff path and **effective floor** and **cap** (if call is exercised).

**E. Comparison & Decision Metrics**  
14. Assemble **comparison table** for base case and scenarios: `USD_forward`, `USD_mm`, `USD_put_only`, `USD_collar`.  
15. Compute:  
   - **Downside shortfall vs Plan** (`min(USD – Plan_USD, 0)`).  
   - **Upside participation** (when `ST > F0_1Y`).  
   - **Cost to carry** (premiums, balance-sheet usage, line utilization).  
16. Flag feasibility constraints (credit line, accounting policy, operations).

---

## 5) Outputs (model deliverables)

| Output | Description | Format | Purpose |
|---|---|---|---|
| `Table_Base` | Base-case USD proceeds by hedge | Table | One-glance CFO view |
| `Table_Sensitivity` | USD proceeds across `ST` grid | Table | Robustness check |
| `Chart_Outcomes` | USD proceeds vs. `ST` by hedge | Line chart | Visual comparison |
| `Chart_Variance` | Variance to Plan_USD by hedge | Bar/line | Budget risk framing |
| `Metrics` | Floor, cap, net premium, basis delta | KPIs | Decision levers |
| `One-Pager_Summary` | Plain-English interpretation | 4–6 bullets | Exec brief |

Model should produce **print-ready** charts and a summary block that can drop directly into Stage 5.

---

## 6) Sensitivity Plan

- **Terminal spot grid (`ST`)**: from **−10% to +10%** vs. `S0`, step **1%**.  
- **Interest-rate shock** (optional): parallel ±50 bps to `r_USD_12M` and `r_EUR_12M` to observe forward parity/`USD_mm` shifts.  
- **Transaction cost overlay**: add 3 bps spread to spot/forward in a second view to show friction impact.  
- **Visuals**:  
  - **Line chart**: USD proceeds vs. `ST` (all hedges).  
  - **Shaded band** at **Plan_USD** to visualize shortfall/excess.  
  - **Marker** at `F0_1Y` to show no-arbitrage anchor.

---

## 7) Limitations & Next Steps

**Limitations**  
- Implied volatility, skew, and delta hedging **not modeled** (use dealer premiums only).  
- **Counterparty credit/CSA** and liquidity haircuts excluded in Stage 2.  
- Tax and hedge-accounting effects **not quantified** (qualitative flag only).  
- Cross-currency basis and funding spreads **assumed negligible** in base case.

**Next Steps (Stage 3 build plan)**  
1. Implement input sheet with **named ranges** matching this spec.  
2. Build three modules (Forward, MM, Options) using the §4 flow; validate **CIP**.  
3. Create the `ST` scenario table and link to **comparison charts**.  
4. Add a **summary dashboard** (metrics + bullets) suitable for CFO.  
5. Prepare a short **prompt block** that references each named range for Stage 4 AI assistance (optional).

---

## Governance & Reproducibility

- **Version control**: stamp inputs and market snapshot (S0, F0_1Y, rates, timestamp).  
- **Traceability**: log any manual overrides to premiums or strikes.  
- **Quality checks**: (i) CIP difference < ~5–10 bps; (ii) `USD_mm` ~ `USD_forward`.  
- **Hand-off**: another analyst can rebuild by following §§2–6 and the named-range map.

---

## Glossary

- **CIP**: Covered Interest Parity; linkage between spot, forward, and rates.  
- **Floor/Cap**: Minimum/maximum USD outcome embedded in options structure.  
- **Plan_USD**: FP&A budget anchor for receivable conversion.
