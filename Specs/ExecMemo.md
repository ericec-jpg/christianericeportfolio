# **FX Exposure Executive Memo**

**Prepared by:** [Your Name]  
**Reviewed by:** [Instructor or CFO Name]  
**Date Created:** [MM/DD/YYYY]  
**Last Updated:** [MM/DD/YYYY]  
**Version:** [1.0]  
**LLM Support (if used):** [e.g., GPT-5 or Codex]

---

## **Executive Summary (≤150 words)**  
State the core message up front. Identify:  
- **What** the firm’s exposure is (currency, amount, timing).  
- **Why** it matters (impact of FX volatility on USD proceeds).  
- **Recommendation headline:** why hedging merits consideration.  

*Tip:* Write this section last. It should read like an elevator pitch to the CFO—concise, confident, and decision-oriented.

---

## **Background & Objectives**  
Briefly explain:  
- The scenario (foreign receivable, expected payment date, counterparty, etc.).  
- Why FX fluctuations create risk.  
- The objective of this memo—e.g., *to evaluate hedging approaches to stabilize future USD cash inflows.*  
- Any assumptions about the macro environment (interest rates, inflation, central-bank policy).

---

## **Market Data Snapshot**  
Provide key market variables that affect hedging decisions.  
These can later be automated or updated dynamically from a data feed (e.g., FRED, ECB, or Bloomberg API).

| Variable | Symbol | Current Value | Source / Note |
|-----------|---------|----------------|----------------|
| **Spot Rate (EUR/USD)** | S₀ | [1.08] | ECB / Reuters |
| **USD Interest Rate** | i_USD | [5.25%] | Federal Reserve (Effective Fed Funds Rate) |
| **EUR Interest Rate** | i_EUR | [3.75%] | ECB Main Refinancing Rate |
| **Forward Premium/Discount** | (F−S)/S | [auto-calc] | Derived via Covered Interest Parity |

*Tip:* In Stage 2, you’ll automate these fields using Excel formulas or Python’s `pandas_datareader`.

---

## **Methods / Analytical Approach**  
Outline how you will assess the exposure:  
- **Data Inputs:** exchange rates, forward rates, interest differentials.  
- **Analytical Tools:** Excel model (Stage 2), sensitivity analysis, parity conditions.  
- **Comparative Framework:** summarize three hedge types.  

| Strategy | Mechanism | Advantages | Limitations |
|-----------|------------|-------------|--------------|
| Forward Contract | Lock in a fixed FX rate | Eliminates uncertainty | No upside potential |
| Option | Right but not obligation to exchange | Flexibility; upside retained | Premium cost |
| Money-Market Hedge | Borrow/lend to synthetically lock rate | Avoids derivatives | Complex to execute |

---

## **Limitations & Next Steps**  
Identify the boundaries of this initial analysis and preview future work.  
- **Key Assumptions:** stable rates, no transaction costs, reliable counterparty.  
- **Limitations:** simplified volatility outlook, preliminary estimates only.  
- **Next Steps:**  
  1. Build spreadsheet model to quantify hedge outcomes.  
  2. Compare expected USD receipts under each hedge.  
  3. Automate rate inputs for both currencies.  
  4. Prepare final analysis and recommendation memo.  

---

## **References**  
List the main sources or tools used to inform your memo (APA or Chicago style).  
- European Central Bank (ECB). *Euro Foreign Exchange Reference Rates.*  
- Hull, J. (2022). *Options, Futures, and Other Derivatives.* Pearson.  
- Corporate Finance Institute. *FX Hedging Strategies.*
