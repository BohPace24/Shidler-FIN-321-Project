# Stage 4 – Spec and Generated Spreadshett
# Bohden Pace
**Scenario:** 4

You are a financial modeling assistant.

# GOAL
Create an Excel file modeling forward, money market, and option hedges for my EUR receivable.

# CONTEXT FILES (GitHub)
Use the logic in:
- 
- 

| Name          | Value    | Description                     |
| ------------- | -------- | ------------------------------- |
| **FC_AMT**    | 20000000 | EUR receivable (EUR 20,000,000) |
| **S0_in**     | 1.0941   | Current spot rate (USD per EUR) |
| **F0_in**     | 1.0935   | 1-year forward rate             |
| **R_USD**     | 0.0411   | USD 1-year interest rate        |
| **R_FC**      | 0.0215   | EUR 1-year interest rate        |
| **K_PUT**     | 1.1606   | EUR put strike                  |
| **K_CALL**    | 1.1606   | EUR call strike                 |
| **PREM_PUT**  | 0.019    | Put premium per EUR             |
| **PREM_CALL** | 0.024    | Call premium per EUR            |
| **T_DAYS**    | 365      | Days to maturity                |
| **T_YRS**     | 1        | Time in years                   |

# **SENSITIVITY TABLE**

Create a two-column data table:

Column 1: S_T

Column 2: USD_put

Column 3: USD_call

Column 4: USD_forward (constant line)

Column 5: USD_mm (constant line)


## 3. MODEL COMPONENTS TO BUILD

### **(A) Forward Hedge**

**Formula:**  
`USD_forward = FC_AMT × F0_in`

- Mark formulas in **green**  
- Output in **gray**

---

### **(B) Money Market Hedge (3-step synthetic hedge)**

#### **1. Borrow EUR today**  
`EUR_PV = FC_AMT / (1 + R_FC)`

#### **2. Convert to USD at spot**  
`USD_today = EUR_PV × S0_in`

#### **3. Invest USD at USD interest rate**  
`USD_mm = USD_today × (1 + R_USD)`

#### **IRP parity check:**  
`F_IRP = S0_in × (1 + R_USD) / (1 + R_FC)`

---

### **Highlight Rules:**

- Money-market formulas = **green**  
- MM output (`USD_mm`) = **gray**  
- Parity check area = **blue** for inputs, **gray** for check results

---

### **(C) Option Hedge Calculations**

Define a variable:

`S_T` = future spot rate.

Create a sensitivity table for S_T ranging:

`0.95 × S0_in` → `1.05 × S0_in` (increments of **0.01**)

---

### **Put Option**

#### **Premium cost (future value):**  
`FV_prem_put = PREM_PUT × FC_AMT × (1 + R_USD)`

#### **Payoff:**  
`Payoff = MAX(K_PUT − S_T, 0) × FC_AMT`

#### **Net USD Proceeds:**  
`USD_put = (FC_AMT × S_T + Payoff) − FV_prem_put`

---

### **Call Option (Benchmark)**

#### **Premium cost (future value):**  
`FV_prem_call = PREM_CALL × FC_AMT × (1 + R_USD)`

#### **Net USD Proceeds:**  
`USD_call = (FC_AMT × S_T) − FV_prem_call`

---

### **Formatting Rules**

- All formulas = **green**  
- All outputs = **gray**


# **SPREADSHEET REQUIREMENTS**
Use named ranges.
Color code inputs yellow, formulas green, outputs gray, assumptions blue.
Include forward hedge, money market hedge, option hedge, and sensitivity analysis.

# **VERIFICATION**
Validate parity and confirm all named ranges.

# **EXPORT**
Return a downloadable Excel file.




