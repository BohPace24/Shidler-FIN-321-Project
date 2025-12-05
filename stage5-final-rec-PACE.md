# **FX Hedge Analysis Executive Ready Memo**

****Prepared by:** Bohden Pace**
# **Scenario:** 4


---

# **A. Exposure Summary**

The company—an American aerospace manufacturer—expects to receive **€20,000,000 in exactly 12 months**. Because revenue is ultimately converted into USD, the firm has a material **foreign exchange exposure**: if the EUR weakens before settlement, the USD value realized at maturity will fall. This directly impacts:

* **Operating margins**
* **Liquidity forecasts**
* **Contract profitability**
* **Budget accuracy**

The business objective, consistent with Stage 2, is to **eliminate downside risk** and secure a **minimum guaranteed USD value** while understanding the performance tradeoffs of alternative hedge structures.

---

# **B. Summary of Hedge Outcomes (Based on Stage 3 Model)**

The Stage 3 Excel model produced the following insights:

## **1. Forward Hedge**

* Formula: `USD_forward = FC_AMT × F0_in`
* Using the provided forward rate (1.0935), the forward hedge generates a **locked-in USD amount** at maturity.
* This creates **100% certainty** with no upfront cost.

## **2. Money Market Hedge**

* Synthetic hedge created through EUR borrowing, USD conversion, and USD investment.
* Outputs nearly identical results to the forward hedge due to **interest rate parity**, validating the model.
* Requires more operational steps and funding coordination than a forward.

## **3. Option Hedges**

Sensitivities were run from **0.95 × S₀ to 1.05 × S₀** using the Stage 3 table.

### **Put Option (Appropriate hedge for receivable)**

* Establishes a **floor** at the strike (1.1606), protecting against EUR depreciation.
* Because premiums are substantial (0.019 × notional, compounded at 4.11%), net proceeds are **lower** than the forward/MM unless EUR appreciates significantly.

### **Call Option (Benchmark only)**

* Not a hedge for EUR receivable exposure.
* Always strictly worse than unhedged exposure after premium costs.

**Insight:** Options introduce **flexibility** and **upside participation**, but at a material premium that meaningfully reduces expected value.

---

# **C. Sensitivity Interpretation (Using Stage 3 Chart & Table)**

### **EUR Depreciation (S_T ↓)**

* **Forward & MM:** Completely insulated from downside.
* **Put Option:** Protects value once S_T < K_put, but premium drags net proceeds below forward/MM.
* **Call Option:** Performs worst—no payoff, premium lost.

### **EUR Appreciation (S_T ↑)**

* **Forward & MM:** Opportunity cost—no upside participation.
* **Put Option:** Best performance; benefits from upward movement while premium remains the only cost.
* **Call Option:** Still not relevant for a receivable.

**Interpretation:** The put option creates a “hockey-stick” payoff, while forward/MM create flat horizontal payoff lines, confirming the qualitative FX hedge expectations.

---

# **D. Strategic Recommendation**

### **Recommended Hedge: Forward Contract (or Money Market Equivalent)**

**Rationale:**

* Delivers **highest certainty** and **best guaranteed USD proceeds** per Stage 3 outputs.
* Requires **no upfront premium** and minimal administrative burden.
* Matches treasury’s mandate in Stage 2: **protect profit margin** and **eliminate downside risk**.

### **Secondary Consideration: Protective Put**

A EUR put may be used *if management values upside optionality*, but:

* Premium reduces expected USD value.
* Only advantageous if significant EUR appreciation (> 5–8%) is expected.

---

# **E. Executive Justification**

### **Cash Flow Stability**

Forward/MM fully stabilize USD receipts, supporting reliable liquidity planning.

### **Budget Certainty**

Protects margins on the aerospace contract, supporting Stage 2’s stated objective.

### **Liquidity & Cost**

Forwards avoid upfront premium drains and are simpler than MM execution.

### **Optionality vs. Value**

Options provide upside only at material cost—rarely optimal unless market views predict sharp EUR appreciation.

### **Accounting Considerations**

Forwards may qualify for hedge accounting treatment, smoothing earnings.

---

# Extra Credit 

## **1. Claude Skills – Real-Time Automation**

Integrating a Claude Skill would allow:

* Automatic fetching of EURUSD forward curves and interest rates.
* Continuous re-valuation of hedge positions.
* Auto-generation of updated hedging memos.
* Fully automated regeneration of Stage 3 spreadsheets.

This turns the model into a **live FX risk management system**.

---

## **2. OpenAI Codex / Code Interpreter**

Codex can:

* Convert Stage 3 Excel logic into Python for full reproducibility.
* Run Monte Carlo FX simulations.
* Validate formulas to prevent spreadsheet drift.
* Regenerate spreadsheets from specs, eliminating manual modeling risk.

This directly reduces model risk—an essential treasury and audit requirement.

---

## **3. GitHub Version Control & Automation (Required)**

### **What Version Control Provides**

* Every change recorded permanently.
* Ability to roll back to prior specifications (Stage 2) or models (Stage 3).
* Full transparency for auditors.

### **Why It Matters in Finance**

* Supports hedge accounting documentation.
* Ensures controls under internal audit & SOX.
* Eliminates silent spreadsheet errors.

### **Workflow Benefits**

* Branching for model upgrades.
* Pull Requests for review of hedge assumptions.
* GitHub Actions to auto-run formula validation.

**Tie to Stages 2–4:**
Your specification, model, and memo can be **regenerated at will**—a major advantage for governance.

---

# **Expanded Career Insight**

This project demonstrates real-world skills used in:

* **Corporate Treasury:** exposure quantification, hedge design.
* **Investment Banking:** cross-currency valuation.
* **FP&A:** multi-scenario planning.
* **Audit/Accounting:** hedge documentation & effectiveness.
* **AI/Data:** model reproducibility, automation frameworks.

---
