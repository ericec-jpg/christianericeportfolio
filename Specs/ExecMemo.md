---
# ============================================================
#  FX Exposure Executive Memo – Spec-Driven Template
#  Version 2.0 (Codex/LLM Ready)
#  Author: AI Assistant
#  Date: 2025-10-25
# ============================================================

spec_name: FX Exposure Executive Memo
course: FIN321 – International Finance
version: 2.0
author: AI Assistant
inputs:
  exposure_currency: "EUR"
  exposure_amount: 11_494_253
  notional_usd_equivalent: 12_500_000
  settlement_date: "2026-10-25"
  current_spot_rate_usd: 1.0875
  forward_rate_usd: 1.0910
  usd_interest_rate: 0.0485
  eur_interest_rate: 0.0315
  volatility_estimate: "High"
  firm_name: "U.S. Tech Services Firm"
  analyst_name: "AI Assistant"
  option_put_strike: 1.0900
  option_call_strike: 1.1300
  put_premium_usd: 0.017
  call_premium_usd: 0.022
tasks:
  - summarize_exposure
  - explain_fx_risk
  - compare_hedge_strategies
  - outline_next_steps
outputs:
  - memo_markdown
  - memo_pdf
  - fx_model.xlsx
automation:
  trigger: on_commit
  handler_script: fx_memo_generator.py
  description: >
    Auto-generate the executive memo and supporting spreadsheet
    using LLM (Codex/GPT) + live FX data via pandas_datareader.
---

# FX Receivable Exposure – EUR/USD

**Created by:** AI Assistant
**Updated by:** AI Assistant
**Date Created:** {{ today }}
**Version:** {{ version }}
**LLM Used:** Codex (GPT-powered)

---

## Executive Summary (≤150 words)
<!-- prompt: summarize_exposure
     Input: {exposure_currency}, {exposure_amount}, {settlement_date}, {firm_name}
     Task: Write an executive-friendly paragraph summarizing:
            - What the exposure is
            - Why hedging may be prudent
            - The strategic goal of risk mitigation
     Tone: Clear, concise, persuasive; avoid jargon.
-->
A U.S. Tech Services Firm expects to collect approximately €11.49 million (≈$12.5 million at today’s EUR/USD 1.0875) from a client in one year. Because the receivable will be converted to dollars, any strengthening of the U.S. dollar would erode the firm’s USD cash inflow. Locking in coverage today either through the 1-year forward rate of 1.0910 or a structured options overlay secures budget certainty around a critical services contract. Management’s objective is to preserve margin on the engagement, protect operating cash flow guidance, and retain upside participation only where it is economically justified by the premium outlay.

---

## Background & Objectives
<!-- prompt: explain_fx_risk
     Input: {exposure_currency}, {exposure_amount}, {settlement_date}, {volatility_estimate}
     Task:
       - Explain nature of exposure (foreign receivable → USD conversion risk)
       - Describe potential downside (weaker FX → lower USD receipts)
       - Quantify illustrative impact using current_spot_rate_usd
     Output: 1-2 paragraphs contextualizing why the CFO should consider hedging.
-->
The firm invoices key enterprise clients in Europe, generating a €11.49 million receivable due on 25 October 2026. Translating that amount at today’s EUR/USD spot of 1.0875 equates to the budgeted $12.5 million inflow. The receivable remains unhedged, exposing results to the recent upswing in dollar volatility driven by divergent monetary policy and U.S. growth surprises.

If EUR/USD declines to 1.03 by settlement, cash conversion would fall to roughly $11.84 million, trimming $0.66 million from projected EBITDA. A 1-year forward is currently available at 1.0910, and 12-month interest benchmarks are 4.85% for USD funding and 3.15% for EUR deposits. These inputs frame the decision between forwards, options, and a money-market hedge to stabilize guidance while balancing cost and flexibility.

---

## Methods
<!-- prompt: compare_hedge_strategies
     Task:
       - Summarize three hedge families: Forward Contract, Options, Money-Market Hedge
       - Present as a markdown table (Strategy | Mechanism | Pros | Cons)
       - Maintain executive tone, concise phrasing
-->
| Strategy | Mechanism | Pros | Cons |
|-----------|------------|------|------|
| Forward Contract | Lock in EUR/USD at 1.0910 for 25 Oct 2026 delivery | Zero cost; budget certainty; aligns with revenue plan | Forfeits upside if EUR strengthens above 1.0910 |
| Option Collar | Buy EUR put / sell EUR call near 1.0900; net premium ≈$0.005 per EUR | Defines floor near $12.5M while offsetting premium; retains upside until call strike | Requires credit line for option margin; complex documentation |
| Money-Market Hedge | Borrow USD, convert to EUR spot, invest until maturity | Mirrors synthetic forward using 4.85%/3.15% rates; no derivatives reporting | Operationally intensive; early unwind penalties; locking liquidity today |

<!-- note: In later stages, link to fx_model.xlsx for quantitative hedge comparison -->
**Quantitative Extension:** Spreadsheet model (`fx_model.xlsx`) will compute expected USD receipts under each hedge, including scenario cases at ±5% spot moves.

---

## Limitations & Next Steps
<!-- prompt: outline_next_steps
     Task:
       - Identify assumptions (static interest rates, no transaction costs)
       - Specify Stage-2–3 deliverables:
           1. Technical spec for spreadsheet model (cash-flow simulation, sensitivity table)
           2. Excel model build and validation
           3. AI prompt for automated spreadsheet generation
           4. Final hedge recommendation
     Format: bullet list.
-->
**Known Limitations:**
- Spot, forward, and interest inputs assumed static; no liquidity or bid/ask adjustments captured.
- Option premiums use indicative quotes ($0.017 put, $0.022 call) without volatility skews.
- Counterparty credit, accounting treatment, and tax considerations are outside scope.

**Next Steps:**
1. Draft technical specification for `fx_model.xlsx`, incorporating forward, collar, and money-market cash flows.
2. Parameterize AI prompt to refresh market data (EUR/USD spot, forwards, rates) before memo generation.
3. Build and validate Excel model with sensitivity analysis (±10% FX shocks) and premium amortization.
4. Present hedge recommendation with CFO decision matrix and implementation timeline.

---

## References
<!-- prompt: cite_sources
     Task: Auto-generate or insert references supporting methodology.
-->
- European Central Bank (ECB) – FX Data API
- Hull, J. C. *Options, Futures, and Other Derivatives* (11th ed.)
- Corporate Finance Institute (CFI) – *FX Hedging Strategies*
---

## Automation Hook
<!-- prompt: automation_doc
     Task:
       - Describe integration for Codex/LLM automation pipeline.
       - Specify trigger and dependencies.
-->
**Tool:** `openai.codex`
**Script:** `fx_memo_generator.py`
**Trigger:** On commit of updated YAML spec.
**Dependencies:** `pandas_datareader`, `openpyxl`, `markdown2pdf`
**Description:**
When the YAML inputs are modified or the FX model is updated,
the automation script calls Codex to generate the memo text,
merges quantitative results, and outputs both `.md` and `.pdf` versions.

---
