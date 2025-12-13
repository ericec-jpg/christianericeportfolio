# **FX Hedge Recommendation Memo — EUR Receivable (Dec 2025)**  
*Prepared by: Christian Erice*  
*Based on Stage 4 Hedge Model*

---

## **A. Exposure Summary**

The firm expects to receive **€11.49M** in **~1 year**.  
Because USD is the functional currency, fluctuations in **EUR/USD** directly impact the USD value of this cash flow:

- If **EUR depreciates**, USD receipts fall — potentially breaching budgeted cash targets.  
- If **EUR appreciates**, USD receipts rise — but only if the hedge structure preserves upside.

**Budget Benchmark:**  
- **USD Target:** $12,500,000

The primary objective is to secure **cash flow certainty** while maintaining alignment with the firm's treasury risk tolerance.

---

## **B. Summary of Hedge Outcomes (Base Case S₀ = 1.1737)**

| Strategy | USD Proceeds | Variance vs Plan | Premium | Insight |
|---------|--------------|------------------|---------|---------|
| **Unhedged** | **$13.49M** | **+$0.99M** | $0 | Full upside exposure; highest volatility |
| **Forward** | **$13.72M** | **+$1.22M** | $0 | Fully locks in rate; zero flexibility |
| **Money Market** | **$13.69M** | **+$1.19M** | $0 | Economically identical to forward, but uses balance sheet |
| **Protective Put** | **$13.30M** | **+$0.80M** | **$195k** | Downside insured; retains upside |
| **Zero-Cost Collar** | **$12.93M** | **+$0.43M** | **$57k** | Floor + cap; most stable but limited upside |

**Key Takeaways**

- Forward and MM deliver the **highest guaranteed USD value**.  
- Put offers **insurance** but costs premium and results in lower base-case USD than forward.  
- Collar materially **reduces premium cost** but caps upside, producing the lowest hedged base-case.

---

## **C. Sensitivity Interpretation**

### **1. EUR Depreciation (EUR weakens)**  
- **Unhedged:** USD receipts decline sharply — highest P&L volatility.  
- **Forward/MM:** Fully insulated — proceeds remain constant.  
- **Put:** Provides a **hard floor** at strike ≈ **$12.33M**.  
- **Collar:** Protects more aggressively with a floor ≈ **$12.48M**, but upside sacrificed.

**Insight:**  
Option structures (put/collar) preserve protection below S₀, but at different cost–benefit trade-offs.

---

### **2. EUR Appreciation (EUR strengthens)**  
- **Unhedged:** Benefits fully; highest potential value.  
- **Forward/MM:** No upside — proceeds capped at locked rate.  
- **Put:** Retains 100% of upside after premium.  
- **Collar:** Upside is **capped** at ~**$12.94M** due to the short call.

**Insight:**  
Puts offer upside participation. Collars offer *conditional* participation.

---

## **D. Strategic Recommendation**

### **Recommended Strategy: _Forward Contract_**

The forward contract is the most aligned hedge for this exposure given:

- **Highest guaranteed USD proceeds** ($13.72M)  
- **Zero premium cost**  
- **Full budget protection with positive variance**  
- **Operational simplicity** compared to MM  
- **No residual market risk** vs. options-based hedges  

While the protective put delivers upside optionality, its **premium drag (~$195k)** lowers certainty-adjusted value.  
The collar reduces premium but produces the **lowest hedged USD proceeds**, making it inferior given cash-flow targets.

---

## **E. Executive Justification**

### **1. Cash Flow Stability**
Forward locks in **$13.72M**, exceeding the plan by ~$1.22M — removing all FX uncertainty.

### **2. Budget Certainty**
Treasury avoids downside surprises while hitting or exceeding the forecasted cash target.

### **3. Liquidity & Cost Efficiency**
No premiums or upfront cash usage; avoids the put’s $195k liquidity cost.

### **4. Balance Sheet Considerations**
Forward requires **no borrowing or investing**, unlike the MM hedge.

### **5. Strategic Fit**
Given the firm’s objectives (certainty > optionality), the forward is the most risk-efficient hedge.

---

# **Final Recommendation: Execute a 1-Year EUR/USD Forward**

This provides **maximum certainty**, **highest locked-in value**, and **zero cost**, making it the cleanest and most CFO-aligned hedge structure for the EUR 11.49M receivable.
