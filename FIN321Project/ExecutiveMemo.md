# FX Exposure Executive Memo – Scenario 3

**Prepared by: Christian Erice
**Reviewed by: Adam Stauffer
**Date Created: [10/24/2025]
**Last Updated: [10/24/2025]
**Version: [1.0]
**LLM Support (if used): GPT-5 Codex
**Exposure:** €11,494,253 (≈$12,500,000 at EUR/USD 1.0875) receivable in 1 year  
**Valuation Date:** 25 October 2025  
**Settlement Date:** 25 October 2026  
**Market Data:** Spot 1.0875 | 1-year forward 1.0910 | USD 12M OIS 4.85% | EUR 12M EURIBOR 3.15%  
**Option Quotes:** EUR put @1.0900 premium $0.017 | EUR call @1.1300 premium $0.022

---

## Executive Summary
A U.S. Tech Services Firm expects to collect €11.49 million in twelve months from a European enterprise client. At today’s spot of 1.0875, the receivable supports a $12.5 million cash-flow target. Because a stronger U.S. dollar would erode the converted value, management should secure budget certainty. Entering a 12-month forward at 1.0910 or pairing a protective put with a covered call both establish a floor near plan while preserving selective upside. The objective is to safeguard EBITDA guidance, anchor investor messaging, and maintain optionality for upside if the euro rallies.

---

## Background & Objectives
The receivable is denominated in euros, leaving the firm exposed to EUR/USD depreciation before conversion next October. Translating the €11.49 million exposure at the current 1.0875 spot rate yields the planned $12.5 million inflow. Dollar strength driven by divergent Federal Reserve and ECB policy could lower realized proceeds, unsettling guidance for the managed-services contract. 

If EUR/USD were to fall to 1.03 by settlement, dollar receipts would decline to about $11.84 million—roughly $0.66 million under plan. A disciplined hedge program using either the posted 1-year forward rate of 1.0910 or a money-market hedge based on 4.85% USD borrowing and 3.15% EUR reinvestment protects cash flow visibility while balancing liquidity and premium considerations.

---

## Methods
| Strategy | Mechanism | Pros | Cons |
|----------|-----------|------|------|
| Forward Contract | Sell €11.49M forward at 1.0910 for settlement on 25 Oct 2026. | Zero cash premium; locks ≈$12.53M; straightforward documentation. | No participation if EUR rallies above forward rate; consumes credit line. |
| Option Collar | Buy EUR put @1.0900 (pay $0.017); sell EUR call @1.1300 (receive ≈$0.012). | Establishes floor near $12.5M; offsets put cost; retains upside until 1.1300. | Requires option approvals; potential margin for short call; residual premium outlay. |
| Money-Market Hedge | Borrow USD today at 4.85%, convert to EUR spot, invest proceeds at 3.15% until maturity. | Replicates forward economics without derivatives; mitigates counterparty concerns. | Ties up balance-sheet capacity; sensitive to funding spreads; unwind can be costly. |

**Quantitative Extension:** Build `fx_model.xlsx` to compare cash outcomes under spot ±5% scenarios and option intrinsic values at maturity.

---

## Limitations & Next Steps
**Known Limitations:**
- Assumes static spot, forward, and interest rates; ignores transaction costs and bid/ask spreads.
- Option premiums are indicative quotes without volatility skew or credit valuation adjustments.
- Accounting, tax, and counterparty credit assessments are pending and may influence final structure.

**Next Steps:**
1. Draft technical requirements for `fx_model.xlsx` covering forward, collar, and money-market cash-flow projections.
2. Refresh market data and calibrate pricing inputs immediately before executing the selected hedge.
3. Review hedge documentation (ISDA/CSA) and confirm hedge-accounting treatment with controllership.
4. Present recommendation and sensitivity analysis to CFO, highlighting trigger levels for layering optional collars.

---

## References
- European Central Bank (ECB) – FX Data API.
- Hull, J. C. *Options, Futures, and Other Derivatives* (11th ed.).
- Corporate Finance Institute (CFI) – *FX Hedging Strategies*.
