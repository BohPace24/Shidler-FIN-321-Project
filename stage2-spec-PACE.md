# Scenario 4: U.S. Aerospace Manufacturer Technical Specification

**Created by:** Bohden Pace
**Updated by:** Bohden Pace  
**Date Created:** 11/04/2025   
**Version:** 1.0

**Role:** Financial Analyst 
**Audience:** CFO  

**Purpose:** Provide a professional, quantitative specification outlining the analytical structure for evaluating FX hedging alternatives.

---

## 1. Problem Statement

Our company, a U.S. Aerospace Manufacturer, expects to receive €20,000,000 in 12 months, creating a significant FX risk exposure to potential fluctuations in the EUR/USD rate. This exposure is an FX Receivable (long EUR), and our primary objective is to eliminate downside risk and secure a guaranteed minimum USD value for the cash flow, thereby protecting the profit margin on the underlying contract. The decision context is Corporate Treasury. This specification outlines the analytical framework for quantifying, comparing, and evaluating alternative hedging strategies (Forward, Money Market, and Options) to mitigate this currency risk.

---

## 2. Inputs (Known Variables)

Create a clean, professional input table. This will become the foundation for your spreadsheet and future AI prompts.

| Variable | Description | Unit | Example | Source |
|-----------|-------------|------|----------|--------|
| `FC_AMT` | Foreign-currency receivable | EUR | 1,200,000 | Company data |
| `S₀` | Current EURUSD spot rate | USD/EUR | [Look up] | Market data |
| `F₀` | 1-year EURUSD forward rate | USD/EUR | 1.0890 | Provided |
| `r_USD` | USD 1-year interest rate | % | [Look up] | Market data |
| `r_EUR` | EUR 1-year interest rate | % | [Look up] | Market data |
| `t` | Time to maturity | Years | 1 | Derived |
| `K_put` | EUR Put strike | USD/EUR | [Set at spot] | Analyst choice |
| `K_call` | EUR Call strike | USD/EUR | [Set at spot] | Analyst choice |
| `Premium_put` | Put premium | USD per contract | 0.017 | Scenario |
| `Premium_call` | Call premium | USD per contract | 0.022 | Scenario |

> *Tip:* Keep labels short and standardized. Think like a financial modeler — these names should become variable names, spreadsheet inputs, or prompt parameters later.

---

## 3. Assumptions & Constraints

- Exchange Rates: All exchange rates are expressed as USD per EUR (Direct Quote from a U.S. perspective).  
- nterest Rates: Interest rates ($r_{USD}$, $r_{EUR}$) are quoted on a simple annual basis (not compounded) for the one-year maturity ($t=1$).
- Forward Rate: The forward rate ($F_0$) is a quoted market rate for a 1-year maturity.  
- Option Premiums: Option premiums are paid upfront in USD at time $t=0$ and must be factored into the Net Present Value (NPV) of the final proceeds. 
- Transaction Costs: Transaction costs, bid-ask spreads, and credit risk associated with counterparties are excluded from this initial quantitative analysis.
- Option Contracts: The specified put and call premiums are for the €20,000,000 notional amount at the common strike price of $K = 1.1606$.  


---

## 4. Calculation Flow

1. Forward Hedge (The Certainty Benchmark)
     - Input: Take the Foreign Currency Amount (€20,000,000).
     - Multiply: Multiply this amount by the 1-year Forward Rate ($F_0 = 1.0935$).
     - Result: The output is the Guaranteed USD Proceeds at Maturity ($t=1$) for the forward contract.
2. Money Market Hedge (The Synthetic Hedge)
     - Step Back (Discounting): Calculate the Present Value (P.V.) of the €20,000,000 Receivable by discounting it back one year using the EUR Interest Rate ($r_{EUR} = 2.15\%$). This determines the amount of EUR to borrow today ($P_V(EUR)$).
     - Immediate Conversion: Convert the calculated $P_V(EUR)$ into USD immediately by multiplying it by the Current Spot Rate ($S_0 = 1.0941$). This gives you the USD amount to invest today ($P_V(USD)$).
     - Future Value (Compounding): Project the invested $P_V(USD)$ forward one year by multiplying it by (1 + $r_{USD}$), using the USD Interest Rate ($r_{USD} = 4.11\%$).
     - Result: The output is the Guaranteed USD Proceeds at Maturity ($t=1$) for the money market hedge ($USD_{MM}$).
     - Validation Check: Using the same spot and interest rates, compute the Interest Rate Parity (IRP) Implied Forward Rate ($F_{IRP}$). Compare this calculated rate against the bank's quoted $F_0$ to check for arbitrage or consistency.
3. Option Hedges (The Insurance Policy)
     - This section requires setting up a variable input for the final spot rate ($S_T$) to perform the sensitivity analysis (see Section 6).
     - A. EUR Put Option (Protection)
     - Future Premium Cost: Calculate the Future Value (F.V.) of the Upfront Premium ($0.019 \times 20,000,000$) by compounding it forward one year using the USD Interest Rate ($r_{USD} = 4.11\%$). This represents the true cost of the insurance at maturity.
     - Hedge Payout (Floor): For a given final spot rate ($S_T$), compare the Strike Price ($K_{put} = 1.1606$) to the Spot Rate ($S_T$).If $S_T$ is lower than $K_{put}$: The option is exercised. The proceeds are the Foreign Currency Amount multiplied by the Strike Price ($K_{put}$).If $S_T$ is higher than or equal to $K_{put}$: The option expires worthless. The proceeds are the Foreign Currency Amount multiplied by the Spot Rate ($S_T$).
     - Net Proceeds: Subtract the calculated Future Premium Cost from the Hedge Payout result. The output is the Net USD Proceeds at Maturity ($t=1$) for the put hedge for that specific $S_T$.B.
       
     - EUR Call Option (Benchmark)
     - Future Premium Cost: Calculate the Future Value (F.V.) of the Upfront Premium ($0.024 \times 20,000,000$) by compounding it forward one year using the USD Interest Rate ($r_{USD} = 4.11\%$).
     - Hedge Payout: This is calculated simply as the Foreign Currency Amount multiplied by the Spot Rate ($S_T$). (Note: In this specific scenario, the company is long EUR and would use a put to hedge. The call option calculation serves primarily as a second benchmark for unlimited upside less the premium cost, assuming the firm is selling the option or comparing with a collar, but for the basic model, the simplest case is just the unhedged proceeds minus the premium cost.)
     - Net Proceeds: Subtract the calculated Future Premium Cost from the Hedge Payout result. The output is the Net USD Proceeds at Maturity ($t=1$) for the call benchmark for that specific $S_T$.



---

## 5. Outputs

List expected results from the model. These become your **spreadsheet outputs**, **AI prompt targets**, and **Stage 5 discussion points**.

| Output | Description | Format | Purpose |
|---------|--------------|---------|----------|
| `USD_forward` | USD proceeds from forward hedge | Numeric | Certainty benchmark |
| `USD_mm` | USD proceeds from money market hedge | Numeric | Cross-check against forward |
| `USD_put` | USD proceeds from EUR put hedge | Table | Sensitivity & protection |
| `USD_call` | USD proceeds from EUR call hedge | Table | Optional upside case |
| `Chart_1` | Hedge outcomes vs. S_T | Line chart | Visual comparison |
| `Summary` | Written conclusion | 1–2 paragraphs | Executive-ready takeaway |

> *Outputs should read like a professional financial dashboard — clear, repeatable, and decision-focused.*

---

## 6. Sensitivity Plan

To test the robustness of each strategy and visualize the risk profiles, we will define and test a range of hypothetical spot rates at maturity ($S_T$):
  1. Range Definition: Vary the EUR/USD spot rate at maturity ($S_T$) from 0.90 $\times S_0$ to 1.30 $\times S_0$ (representing a significant downside and upside movement) in increments of 0.01.
  2. Calculation: For each value of $S_T$ in the defined range, compute the final USD proceeds at $t=1$ under the Forward, Money Market, and Put Option strategies.
  3. Visualization: Present the results in a line chart (Chart_1) with $S_T$ on the x-axis and $USD$ Proceeds at $t=1$ on the y-axis. The chart will clearly show the horizontal, risk-free lines for the Forward and Money Market hedges, and the "hockey stick" payoff profile for the Put option.


---

## 7. Limitations & Next Steps

7. Limitations & Next Steps
   This specification lays the analytical groundwork but does not incorporate implied volatility (only using observed market rates for $S_0$, $F_0$, and $K$), transaction costs, liquidity risk, or credit risk. The options analysis assumes a single strike for simplification, and the money market hedge assumes perfect access to the stated interbank interest rates. The immediate next step is to construct an Excel model (Stage 3) that implements the Calculation Flow (Section 4) and Sensitivity Plan (Section 6) to quantify the final USD proceeds and NPV for each hedge structure.

---
