<div style="border-top: 6px solid #024731; border-bottom: 1px solid #B2B2B2; padding: 12px 0; margin-bottom: 24px; font-family: 'Open Sans', Helvetica, Arial, sans-serif;">

&#x20; <div style="color: #024731; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; font-size: 0.85rem;">University of Hawaiʻi at Mānoa · Shidler College of Business</div>

&#x20; <div style="color: #000000; font-weight: 700; font-size: 1.25rem; margin-top: 4px;">FIN-321 International Finance &amp; Securities</div>

&#x20; <div style="color: #525252; font-weight: 400; font-size: 0.95rem;">FX Transaction Hedging Project — Technical Specification</div>

</div>



<!--

BRAND FORMATTING — applied per docs/_branding/design.json (v1.0.0)

&#x20; ┌─ Colors ─────────────────────────────────────────────────────────────┐

&#x20; │ Primary green ........... #024731  RGB 2,71,49    Pantone 3435 C     │

&#x20; │ Primary black ........... #000000  RGB 0,0,0      Process Black      │

&#x20; │ Silver (secondary) ...... #B2B2B2  RGB 178,178,178 Cool Gray 5 C     │

&#x20; │ White (secondary) ....... #FFFFFF                                    │

&#x20; │ Neutral-600 (muted) ..... #525252  (secondary text, captions)        │

&#x20; │ UH-green 700 (hover) .... #013D26  (link hover, pressed state)       │

&#x20; │ UH-green 50 (tint) ...... #E6F2EF  (callout backgrounds)             │

&#x20; │ Yellow (Excel only) ..... #FFFF00  (input highlight — not brand)     │

&#x20; ├─ Typography ─────────────────────────────────────────────────────────┤

&#x20; │ Headings (web)  .......... Open Sans Bold (H1/H2) / Semibold (H3/H4) │

&#x20; │ Headings (print)  ........ Avenir Bold                               │

&#x20; │ Body (web)  .............. Open Sans Regular                         │

&#x20; │ Body (print)  ............ Avenir Book                               │

&#x20; │ Fallback stack  .......... Helvetica, Arial, sans-serif              │

&#x20; │ Monospace  ............... Consolas / ui-monospace                   │

&#x20; │ Body minimum size  ....... 10 pt (11–12 pt preferred for print)      │

&#x20; │ Leading  ................. 3–5 pt greater than type size (print)     │

&#x20; │ Alignment  ............... Flush left, ragged right                  │

&#x20; ├─ Accessibility ──────────────────────────────────────────────────────┤

&#x20; │ • ADA-compliant contrast ratios for ALL text and UI elements         │

&#x20; │ • No red body type                                                   │

&#x20; │ • No layouts that are too dark for readability                       │

&#x20; │ • No custom palettes or gradients outside the official brand         │

&#x20; └──────────────────────────────────────────────────────────────────────┘

&#x20; Full brand standard: docs/_branding/design.json · Source: https://manoa.hawaii.edu/brand/




# U.S. Tech Services Firm — FX Transaction Hedge Model · Technical Specification



> <span style="color:#024731; font-weight:700;">Technical specification</span> for the FX transaction hedge model — the named-range contract, calculation flow, and validation checks, precise enough that an AI or a colleague could build (or rebuild) the workbook from this document alone. This spec is the input the AI-assisted build works from.



| Field | Value |

|------|------|

| **Created by** | Timmy Vuong |

| **Updated by** | Timmy Vuong |

| **Date Created** | 2026-08-07 |

| **Date Updated** | 2026-08-07 |

| **Version** | 0.1 |

| **LLM Used** (optional) | ChatGPT — explanation and feedback |

| **Role** | Treasury Analyst / FP&A Analyst |

| **Audience** | CFO / Director of Treasury |

| **Companion Workbook** | `docs/spreadsheets/International Finance Spreadsheets.xlsx` (Chapter 8 Transaction Hedging tabs — reference/worked example) or student build |



---





## 1. Problem Statement



U.S. Tech Services Firm expects to receive EUR 12,500,000 in 365 days.

Because the company budgets and reports in USD, the payment’s dollar value depends on the EUR/USD exchange rate.

If the euro weakens before settlement, the company will receive fewer dollars, potentially affecting its cash flow and planned spending.

The proposed model will compare an unhedged position with forward, money-market, and put-option hedges to evaluate their protection and trade-offs.



## 2. Inputs — Named-Range Contract

> All placeholder values are indicative and will be replaced with live market data during Stage 4.



| Named Range | Description | Placeholder Value | Unit | Stage 4 Source |

|---|---|---:|---|---|

| `FC_AMT` | Foreign-currency receivable | 12,500,000 | EUR | Company contract |

| `S0_in` | Current EUR/USD spot rate | TBD | USD per EUR | Live FX market data |

| `F0_in` | One-year EUR/USD forward rate | 1.0910 | USD per EUR | Live forward quote |

| `R_USD` | Annual USD interest rate | TBD | Decimal annual rate | Live USD market rate |

| `R_FC` | Annual EUR interest rate | TBD | Decimal annual rate | Live EUR market rate |

| `K_PUT` | EUR put-option strike rate | TBD | USD per EUR | Live option quote |

| `K_CALL` | EUR call-option strike rate | TBD | USD per EUR | Live option quote |

| `PREM_PUT` | EUR put-option premium | 0.017 | USD per EUR | Live option quote |

| `PREM_CALL` | EUR call-option premium | 0.022 | USD per EUR | Live option quote |

| `T_DAYS` | Days until settlement | 365 | Days | Contract settlement terms |

## 3. Tab Architecture

| Workbook Tab | Purpose |
|---|---|
| Cover | Model title, author, version, date, and summary. |
| Legend/Key | Color, input, formula, output, and named-range conventions. |
| Inputs | Values, units, sources, and dates for all ten named inputs. |
| Forward Hedge | Fixed USD proceeds using the forward rate. |
| Money-Market Hedge | EUR borrowing, spot conversion, and USD investment calculations. |
| Option Hedge | Put and call payoffs, premiums, and USD proceeds. |
| Sensitivity | Eleven exchange-rate scenarios and the comparison chart. |
| Notes & Assumptions | Conventions, limitations, sources, and model changes. |


## 4. Assumptions & Constraints

ACT/360: Divide the actual number of days by 360 when calculating interest.

No transaction costs: Ignore bank fees, bid–ask spreads, taxes, and commissions to keep the model simple.

Simple interest: Apply the USD and EUR annual rates only for the portion of the year before settlement.

EUR/USD quote: A rate of 1.0910 means one euro equals 1.0910 U.S. dollars.

Option premium: Subtract the cost of the EUR put option from the protected USD proceeds.

Parity check: The money-market hedge should produce a result reasonably close to the forward hedge.

Placeholder data: Stage 2 uses preliminary figures; Stage 4 replaces them with live rates and quotes.

## 5. Calculation Flow



### Forward Hedge





**Formula**



`USD_FORWARD = FC_AMT × F0_in`



**Placeholder calculation**



`USD_FORWARD = EUR 12,500,000 × 1.0910 USD/EUR = USD 13,637,500`



U.S. Tech Services Firm would sell its expected EUR 12.5 million receivable forward at the one-year rate of 1.0910 USD per EUR. This would lock in USD 13,637,500 at settlement and protect the company if the euro weakens. However, the company would not benefit if the euro strengthens above the contracted forward rate.



### Money-Market Hedge




**Calculation flow**



1. `EUR_BORROW = FC_AMT / (1 + R_FC × T_DAYS / 360)`

2. `USD_NOW = EUR_BORROW × S0_in`

3. `USD_MM = USD_NOW × (1 + R_USD × T_DAYS / 360)`



For U.S. Tech Services Firm, the model will first calculate the amount of euros that must be borrowed today so the loan grows to EUR 12,500,000 in 365 days. The borrowed euros will be converted into dollars at the current spot rate, and those dollars will be invested at the USD interest rate. When the company receives its EUR 12,500,000 payment, it will use that money to repay the euro loan. This strategy creates USD cash-flow certainty but requires borrowing capacity and involves more transactions than a forward contract. A final USD result cannot be calculated until the live spot and interest rates are entered during Stage 4.



### Option Hedge



**Formula**



`USD_PUT = FC_AMT × MAX(S_T, K_PUT) - (FC_AMT × PREM_PUT)`



**Known premium cost**



`PUT_PREMIUM_COST = EUR 12,500,000 × 0.017 USD/EUR = USD 212,500`



U.S. Tech Services Firm could purchase an EUR put option covering its EUR 12.5 million receivable. If the euro falls below the option’s strike rate, the company can exercise the put and convert its euros at the protected rate. If the euro remains above the strike, the company can let the option expire and convert the payment at the more favorable market rate. This strategy provides downside protection while preserving potential gains from a stronger euro, but it requires a $212,500 premium. Because the strike rate has not yet been provided, the minimum protected USD proceeds will be calculated after live option data is added during Stage 4.



## 6. Sensitivity Plan

The sensitivity analysis will evaluate settlement exchange rates ranging from 95% to 105% of the initial EUR/USD spot rate. The model will use the following 11 scenarios:



0.95 × S0_in, 0.96 × S0_in, 0.97 × S0_in, 0.98 × S0_in, 0.99 × S0_in, 1.00 × S0_in, 1.01 × S0_in, 1.02 × S0_in, 1.03 × S0_in, 1.04 × S0_in, and 1.05 × S0_in



For each settlement rate, the model will calculate:



No hedge: USD_UNHEDGED = 12,500,000 × S_T

Forward hedge: USD_FORWARD = USD 13,637,500

Money-market hedge: USD_MM, calculated using the EUR and USD interest rates

Put-option hedge: USD_PUT = 12,500,000 × MAX(S_T, K_PUT) − 212,500



The results will be presented in a line chart with the settlement EUR/USD rate on the horizontal axis and USD proceeds on the vertical axis. The chart will show the put option’s protected floor, the fixed proceeds from the forward and money-market hedges, and any exchange rates where the preferred strategy changes. Exact results will be populated after live market inputs are added during Stage 4.

## 7. Validation Rules



| Validation Test             | Passing Condition                                                                                             | Failure Response                             |

| --------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |

| Required named ranges       | All ten required names exist and contain numeric values.                                                      | Display `CHECK INPUTS`.                      |

| Input boundaries            | `FC_AMT`, `S0_in`, `F0_in`, `K_PUT`, `K_CALL`, and `T_DAYS` are greater than zero; premiums are not negative. | Highlight the invalid input.                 |

| Forward calculation         | `USD_FORWARD` equals `FC_AMT × F0_in`, allowing for rounding to the nearest cent.                             | Display `FORWARD ERROR`.                     |

| Implied forward rate        | `F_IMPLIED = S0_in × (1 + R_USD × T_DAYS / 360) / (1 + R_FC × T_DAYS / 360)`.                                 | Display the difference from `F0_in`.         |

| Interest-rate parity        | The relative difference between `F_IMPLIED` and `F0_in` is no more than 0.5%.                                 | Flag the result for review.                  |

| Money-market reconciliation | `USD_MM` is within 0.5% of `USD_FORWARD` when contemporaneous rates are used.                                 | Display `PARITY CHECK`.                      |

| Put-option floor            | `USD_PUT` is never below `FC_AMT × K_PUT − FC_AMT × PREM_PUT`.                                                | Display `OPTION ERROR`.                      |

| Sensitivity range           | The table contains 11 scenarios from `0.95 × S0_in` through `1.05 × S0_in` in 1% increments.                  | Display `RANGE ERROR`.                       |

| Missing data                | Blank, text-based, or invalid market inputs do not produce financial outputs.                                 | Display a clear warning instead of a result. |



## 8. Outputs



The completed workbook will provide the following decision-oriented outputs for U.S. Tech Services Firm:



| Output                    | Specification                                                                                       |

| ------------------------- | --------------------------------------------------------------------------------------------------- |

| Strategy comparison       | Display USD proceeds for no hedge, forward, money-market, and EUR put-option strategies.            |

| Forward proceeds          | Show the placeholder locked proceeds of `USD 13,637,500`, calculated using the 1.0910 forward rate. |

| Option cost and floor     | Show the `USD 212,500` put premium and the protected minimum proceeds after `K_PUT` is populated.   |

| Effective conversion rate | Calculate `USD proceeds ÷ FC_AMT` for each strategy.                                                |

| Difference from no hedge  | Calculate each strategy’s USD gain or loss relative to the unhedged position.                       |

| Sensitivity analysis      | Display all 11 settlement-rate scenarios and a line chart comparing the four strategies.            |

| Validation status         | Report whether the named ranges, formulas, option floor, and interest-rate parity checks pass.      |

| Data documentation        | Identify each market-data source and the date and time each live input was retrieved.               |



The outputs will support a preliminary comparison of hedge alternatives. A final hedge recommendation will not be issued until the model is populated with live data and independently validated in later stages.

