---
# ============================================================
#  FX Exposure Executive Memo – Spec-Driven Template
#  Version 2.0 (Codex/LLM Ready)
#  Author: [Your Name]
#  Date: [YYYY-MM-DD]
# ============================================================

spec_name: FX Exposure Executive Memo
course: FIN321 – International Finance
version: 2.0
author: [Your Name]
inputs:
  exposure_currency: "EUR"
  exposure_amount: 1_000_000
  settlement_date: "2026-03-01"
  current_spot_rate_usd: 1.08
  volatility_estimate: "High"
  firm_name: "Example Corp"
  analyst_name: "[Your Name]"
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

# [Memo Title: FX Receivable Exposure – [Currency Pair]]

**Created by:** {{ analyst_name }}  
**Updated by:** {{ analyst_name }}  
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
[Auto-generated summary here]

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
[Auto-generated background and objectives]

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
| Forward | Lock in future exchange rate | Eliminates uncertainty | No upside potential |
| Option | Buy right, not obligation | Flexibility; upside retained | Premium cost |
| Money Market | Use borrowing/lending to synthetically lock rate | No derivatives | Complex execution |

<!-- note: In later stages, link to fx_model.xlsx for quantitative hedge comparison -->
**Quantitative Extension:** Spreadsheet model (`fx_model.xlsx`) will compute expected USD receipts under each hedge.

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
- Spot/forward rates assumed constant until settlement.  
- Volatility estimate based on historical 1-year standard deviation.  
- Excludes counterparty and credit risks.  

**Next Steps:**
1. Draft technical model specification for `fx_model.xlsx`.  
2. Use Python + Codex to auto-populate sensitivity tables (USD receipts vs. FX rate).  
3. Test three hedge scenarios in Excel model.  
4. Generate AI-assisted final memo and recommendation.

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
