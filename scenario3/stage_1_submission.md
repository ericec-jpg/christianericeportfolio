# Executive Memo – Stage 1 Submission (Scenario 3)

**To:** CFO, U.S. Tech Services Firm  
**From:** Treasury Analyst  
**Date:** October 23, 2025  
**Subject:** EUR Receivable Exposure and Initial Hedging Considerations

## Executive Summary
- The firm expects to collect **€12.5 million** in twelve months for European service contracts. At today’s EURUSD spot rate (quote pending confirmation), this exposure represents a material FX risk to next year’s USD cash flows.
- A one-year forward rate of **1.0910** locks in approximately **$13.64 million** in dollar proceeds, eliminating FX uncertainty at the cost of foregoing potential upside if the euro appreciates.
- Exchange-traded option premiums (Put: $0.017, Call: $0.022 per euro) enable asymmetric protection strategies, though final strikes and notional alignment with the receivable must be confirmed.
- Recommend validating interest-rate inputs, evaluating forward vs. option hedge costs, and preparing scenario analysis ahead of Stage 2 technical specification.

## Exposure Overview
- **Receivable:** €12,500,000 due in one year (customer credit risk assumed minimal for this stage).  
- **Functional Currency:** USD; exposure arises from euro-denominated cash inflow.  
- **Current Market Data:**
  - Spot rate: EURUSD (exact quote pending – obtain latest broker feed).  
  - 1-year forward rate: 1.0910.  
  - USD interest rate: [n.nn%] (Treasury to confirm).  
  - EUR interest rate: [n.nn%] (Treasury to confirm).

## Risk Assessment
- **Translation to USD:** Each 0.01 move in EURUSD alters USD receipts by roughly $125,000 (0.01 × €12.5M).  
- **Budget Sensitivity:** Budget assumes USD receipts at or above forward-implied value; unhedged exposure could materially impact EBITDA forecasts.  
- **Macro Drivers:** ECB vs. Fed policy divergence, eurozone growth data, and geopolitical risk (energy supply shocks) are primary drivers over the next 12 months.

## Hedging Alternatives
1. **Natural Hedge:** No material euro-denominated expenses currently available to offset receipts; investigate future euro cost commitments.  
2. **Forward Contract:** Lock EURUSD at 1.0910 for €12.5M notional. Provides certainty, zero upfront premium, but sacrifices upside. Requires credit line / ISDA documentation.  
3. **Option Strategies:**  
   - **Protective Put:** Buy EUR put (USD call) at strike [EURUSD]; protects against euro depreciation while allowing appreciation. Premium outlay: ~$212,500 (0.017 × €12.5M). Confirm strike and contract sizing.  
   - **Collar:** Finance put premium by selling EUR call (USD put) at strike [EURUSD]; limits upside beyond strike while reducing net cost. Premium differential: ~$62,500 net inflow (0.022 − 0.017) × €12.5M, pending strike validation.  
   - **Participating Forward / Option Structure:** Evaluate hybrids subject to counterparty offerings.

## Data and Process Gaps
- Obtain firm EURUSD spot quote and historical volatility series.  
- Confirm USD and EUR yield curves to validate forward parity relationships.  
- Verify counterparty credit limits, ISDA/CSA status, and treasury policy compliance.  
- Document accounting treatment (ASC 815) implications for derivatives employed.

## Next Steps (Pre-Stage 2)
1. Finalize Stage 2 technical specification inputs (market data sources, modeling assumptions, valuation methodology).  
2. Quantify hedge effectiveness under at least three EURUSD scenarios (appreciation, base, depreciation).  
3. Coordinate with accounting to ensure hedge documentation readiness.  
4. Schedule stakeholder review to align on preferred hedging direction before trade execution window.

---
Prepared in accordance with Stage 1 specification requirements for Scenario 3.
