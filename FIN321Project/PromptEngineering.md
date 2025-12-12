You are a financial modeling assistant and Excel automation engine.

# GOAL
Create a complete, audit-ready Excel workbook that models forward, money market (synthetic forward), and option hedges for a EUR receivable. 
Use the **exact variables, named ranges, color coding, and model logic** specified below. 
Do **not** invent your own naming conventions or structure.

# CONTEXT
This model is **Stage 4 – Prompt Engineering** of a multi-stage FX hedge project. 
You must:
- Respect the technical design defined in my Stage 2 specification.
- Follow the implementation patterns already used in my Stage 3 Excel file.
- Produce a clean, professional workbook suitable for CFO / Treasury review.

## CONTEXT FILES (GitHub)
Use these context files to align logic, structure, and intent:

- Stage 2 technical specification (logic and hedge design):  
  https://github.com/ericec-jpg/christianericeportfolio/blob/main/FIN321Project/Spec.md

- Stage 3 model (structure, layout, and formulas reference):  
  https://github.com/ericec-jpg/christianericeportfolio/blob/main/FIN321Project/stage3-model-ERICE.xlsx

When building the Stage 4 workbook, you may **reuse** the logical flow and modeling ideas, but you must **enforce** the named ranges and formatting standards described in this prompt.

# INPUT VARIABLES
Use this **single scenario** with **real market data** (snapshot as of Dec 2025). 
Populate these values on an Inputs/Assumptions block and assign the named ranges exactly as shown.

**Scenario – EUR Receivable**

- FC_AMT (EUR receivable)  
  - Value: **11,494,253**  
  - Unit: EUR  
  - Named range: `FC_AMT`

- Spot rate (EUR/USD, USD per EUR)  
  - Value: **1.1737**  
  - Named range: `S0_in`

- 1-year forward rate (EUR/USD, USD per EUR)  
  - Value: **1.1937**  
  - Named range: `F0_in`

- USD interest rate (1-year, p.a.)  
  - Value: **3.55%**  
  - Named range: `R_USD`

- EUR interest rate (1-year, p.a.)  
  - Value: **2.04%**  
  - Named range: `R_FC`

- Put strike (EUR put, USD per EUR)  
  - Value: **1.0900**  
  - Named range: `K_PUT`

- Call strike (EUR call sold, USD per EUR)  
  - Value: **1.1300**  
  - Named range: `K_CALL`

- Put premium (paid, per EUR, in USD)  
  - Value: **0.0170**  
  - Named range: `PREM_PUT`

- Call premium (received, per EUR, in USD)  
  - Value: **0.0120**  
  - Named range: `PREM_CALL`

- Tenor in days  
  - Value: **365**  
  - Named range: `T_DAYS`

- Tenor in years (derived)  
  - Formula: `=T_DAYS/365`  
  - Named range: `T_YRS`

Additionally, include a **Plan USD** budget anchor and map it to the Stage 2 spec:
- Plan_USD target inflow  
  - Value: **12,500,000**  
  - Named range: `PLAN_USD`

# SPREADSHEET REQUIREMENTS

The workbook must:

1. Use **named ranges** exactly as specified in this prompt (see next section).
2. Implement **three hedge modules**:
   - Forward hedge
   - Money market hedge (3-step synthetic forward)
   - Option hedges (protective put and collar)
3. Include a **spot sensitivity table** from **0.95 × S0_in** to **1.05 × S0_in**.
4. Provide a **summary panel** comparing USD proceeds vs. `PLAN_USD`.
5. Include **cross-checks**:
   - Covered interest parity check.
   - Consistency between forward and money-market hedges.

# NAMED RANGE DEFINITIONS

Use these **standardized named ranges** in the workbook. 
Do not create alternative names.

- `FC_AMT`   → EUR receivable notional
- `S0_in`    → Current spot rate (USD per EUR)
- `F0_in`    → 1-year forward rate (USD per EUR)
- `R_USD`    → USD annual interest rate for tenor `T_YRS`
- `R_FC`     → EUR annual interest rate for tenor `T_YRS`
- `K_PUT`    → Put strike (USD per EUR)
- `K_CALL`   → Call strike (USD per EUR)
- `PREM_PUT` → Put premium per EUR (USD)
- `PREM_CALL`→ Call premium per EUR (USD; positive = received)
- `T_DAYS`   → Tenor in days
- `T_YRS`    → Tenor in years (=T_DAYS/365)
- `PLAN_USD` → Budget anchor for USD inflow

Use these ranges consistently across all formulas, including sensitivity and outputs.

# MODEL LOGIC (PSEUDOCODE)

Implement logic consistent with the Stage 2 spec (forward, money-market, options, and comparison). 
Translate the following pseudocode into Excel formulas referencing the named ranges.

## 1. Base Data & CIP Check

1. Load base inputs: `FC_AMT`, `S0_in`, `F0_in`, `R_USD`, `R_FC`, `T_YRS`, `PLAN_USD`.
2. Compute **theoretical forward** implied by covered interest parity:

   - `F_theoretical = S0_in * (1 + R_USD * T_YRS) / (1 + R_FC * T_YRS)`

3. Compute forward basis delta in basis points:

   - `Basis_bps = (F0_in / F_theoretical - 1) * 10,000`

4. Display:
   - `F0_in`, `F_theoretical`, `Basis_bps`  
   - Flag if |Basis_bps| > threshold (e.g., 10 bps).

## 2. Hedge 1 – Forward Contract

5. Locked USD proceeds at maturity:

   - `USD_forward = FC_AMT * F0_in`

6. Variance vs. plan:

   - `Var_forward = USD_forward - PLAN_USD`

7. Report:
   - `USD_forward`, `Var_forward`

## 3. Hedge 2 – Money-Market Hedge (Synthetic Forward)

8. Present value of EUR in home currency:

   - `EUR_PV = FC_AMT / (1 + R_FC * T_YRS)`

9. Convert to USD today at spot:

   - `USD_today = EUR_PV * S0_in`

10. Invest USD at `R_USD` to maturity:

   - `USD_mm = USD_today * (1 + R_USD * T_YRS)`

11. Variance vs. plan:

   - `Var_mm = USD_mm - PLAN_USD`

12. Cross-check vs. forward:

   - `Diff_forward_mm = USD_mm - USD_forward`
   - Also compute `%Diff_forward_mm = Diff_forward_mm / USD_forward`

## 4. Hedge 3 – Options (Put and Collar)

Model two structures:

### 4.1 Protective Put Only

13. Define terminal spot `ST` as a variable (for base case and sensitivity table).

14. For each `ST`:
    - **Gross USD receipts** without options: `USD_spot = FC_AMT * ST`
    - **Put payoff (in USD)**:  
      `Payoff_put = FC_AMT * MAX(K_PUT - ST, 0)`
    - **Premium cost (USD)**:  
      `Prem_put_total = FC_AMT * PREM_PUT` (paid at t=0, but report effect on total economics)

15. Effective USD proceeds (economic, ignoring timing nuance):

    - `USD_put_only = USD_spot + Payoff_put - Prem_put_total`

16. Variance vs. plan:

    - `Var_put_only = USD_put_only - PLAN_USD`

### 4.2 Collar (Buy Put, Sell Call)

17. For each `ST`:

    - **Call payoff obligation (USD)**:  
      `Payoff_call = -FC_AMT * MAX(ST - K_CALL, 0)`  
      (negative = USD foregone when spot > K_CALL)

    - **Net premium today (USD)**:  
      `Prem_collar_net = FC_AMT * (PREM_PUT - PREM_CALL)`

18. Effective USD proceeds:

    - `USD_collar = USD_spot + Payoff_put + Payoff_call - Prem_collar_net`

19. Variance vs. plan:

    - `Var_collar = USD_collar - PLAN_USD`

## 5. Sensitivity Plan – Spot Grid

20. Build a sensitivity table for `ST` from **0.95 × S0_in** to **1.05 × S0_in** in equal increments (e.g., 1% steps).

21. For each `ST` in the grid, compute:

    - `USD_forward` (constant across ST)
    - `USD_mm` (constant across ST)
    - `USD_put_only`
    - `USD_collar`
    - Variances vs. `PLAN_USD`

22. Use this table to feed charts if desired.

# FORMATTING & COLOR CODING

Apply the following conventions **consistently**:

- **Yellow** = Inputs / decision variables  
  - All raw scenario inputs, including `FC_AMT`, `S0_in`, `F0_in`, `R_USD`, `R_FC`, `K_PUT`, `K_CALL`, `PREM_PUT`, `PREM_CALL`, `T_DAYS`, `PLAN_USD`.

- **Blue** = Assumptions / derived parameters  
  - `T_YRS`, any thresholds (e.g., basis tolerance), any scenario grid definitions.

- **Green** = Formulas / calculation cells  
  - Intermediate steps: `F_theoretical`, `Basis_bps`, `USD_forward`, `USD_mm`, `USD_put_only`, `USD_collar`, all sensitivity table formulas.

- **Gray** = Outputs / KPIs / summary metrics  
  - Main KPI block with: `USD_forward`, `USD_mm`, `USD_put_only`, `USD_collar`, their variances vs. `PLAN_USD`, and key metrics like min / max USD, effective floor/cap.

Additional formatting:

- Use financial formatting with commas and 2 decimal places for USD amounts.
- Use % format for rates and variances where appropriate.
- Clearly labeled section headers:
  - “Inputs & Assumptions”
  - “CIP Check”
  - “Forward Hedge”
  - “Money-Market Hedge”
  - “Options – Put Only”
  - “Options – Collar”
  - “Spot Sensitivity”
  - “Summary Dashboard”

# OUTPUT REQUIREMENTS

The final workbook must include:

1. **Core Outputs**
   - Base-case USD proceeds:
     - `USD_forward`
     - `USD_mm`
     - `USD_put_only` (at base `ST = S0_in`)
     - `USD_collar` (at base `ST = S0_in`)
   - Variances vs. `PLAN_USD` for each hedge.

2. **Sensitivity Table**
   - A structured table with `ST` from 0.95 × `S0_in` to 1.05 × `S0_in`, showing:
     - `USD_forward`
     - `USD_mm`
     - `USD_put_only`
     - `USD_collar`
     - Optionally, variance vs. `PLAN_USD`.

3. **Summary Panel**
   - A compact block that compares hedges:
     - Locked-in USD (forward, MM)
     - Floor and cap levels implied by options
     - Net premium cost/benefit
     - Key observations (formula-driven, not hard-coded text).

# VERIFICATION

Before finalizing the file, perform these validation steps and expose the results in the workbook:

1. **Forward vs. Money-Market Parity**
   - Check that `USD_mm` is approximately equal to `USD_forward` for the given rates.
   - Compute:
     - `Diff_forward_mm`
     - `%Diff_forward_mm`
   - Flag if `%Diff_forward_mm` is outside a small tolerance (e.g., ±0.5%).

2. **Covered Interest Parity**
   - Confirm that `F0_in` is close to `F_theoretical`.
   - Display `Basis_bps` and a textual indicator (e.g., “OK” / “Warning”).

3. **Named Range Integrity**
   - Confirm that all named ranges listed in the “NAMED RANGE DEFINITIONS” section are present and correctly mapped.
   - Provide a small table mapping:
     - Named Range → Cell Address → Description.

4. **Formula Mapping (Auditability)**
   - Provide a sample mapping table listing:
     - Key output cells (e.g., `USD_forward`, `USD_mm`, `USD_put_only`, `USD_collar`)
     - The Excel formulas used (in A1 notation).
   - Ensure there are **no hard-coded numbers** inside critical calculation formulas other than assumptions/inputs.

# EXPORT

- Return a **fully functional `.xlsx` file** that:
  - Is compatible with Excel 2019 or later.
  - Contains all named ranges as defined above.
  - Preserves all formulas (no values pasted over formulas).
  - Preserves color coding and section headers.
- Do **not** lock or protect sheets.
- The file should be ready for direct download and further manual review by a human analyst.

You must follow all instructions in this prompt exactly and prioritize consistency with the Stage 2 spec and Stage 3 model linked above.
