\# Stage 4 Market Data Memo



\*\*Student:\*\* Timmy Vuong  

\*\*Scenario:\*\* 3 — U.S. Tech Services Firm  

\*\*Exposure:\*\* EUR 12,500,000 receivable  

\*\*Settlement:\*\* 365 days  

\*\*Data date:\*\* 2026-08-07 — latest available market close 

\*\*Retrieval date:\*\* 2026-08-08  



\## Market Inputs



| Named Input | Value | Source | Market Date/Time | Method or Notes |

|---|---:|---|---|---|

| `FC\_AMT` | 12,500,000 | Scenario 3 | — | Scenario-provided receivable |

| `S0\_in` | 1.1535 | \[European Central Bank reference rates](https://www.ecb.europa.eu/stats/eurofxref/eurofxref-hist-90d.xml) | 2026-08-07; retrieved 2026-08-08 | Latest available EUR/USD reference rate; USD per EUR |

| `R\_USD` | 4.06% (0.0406) | \[FRED — 1-Year Treasury Constant Maturity Rate](https://fred.stlouisfed.org/series/DGS1) | Observation 2026-08-06; retrieved 2026-08-08 | Chosen because the one-year Treasury maturity matches the 365-day exposure; latest published observation |

| `R\_FC` | 2.5529% (0.025529) | \[ECB — AAA Euro-Area Government Yield Curve, 1-Year Spot Rate](https://data-api.ecb.europa.eu/service/data/YC/B.U2.EUR.4F.G\_N\_A.SV\_C\_YM.SR\_1Y?startPeriod=2026-08-01\&format=csvdata) | Observation 2026-08-06; retrieved 2026-08-08 | Chosen as the EUR rate proxy because it is an official one-year euro-area government yield matching the exposure horizon |

| `F0\_in` | 1.170681 | Calculated from the sourced `S0\_in`, `R\_USD`, and `R\_FC` values | Data observations 2026-08-06 and 2026-08-07 | CIP-implied one-year forward using the assignment formula |

| `K\_PUT` | 1.1535 | Assumption based on the live ECB spot rate | 2026-08-07 | Set equal to `S0\_in`; at-the-money put strike |

| `K\_CALL` | 1.1535 | Assumption based on the live ECB spot rate | 2026-08-07 | Set equal to `S0\_in`; at-the-money call strike || `PREM\_PUT` | 0.017 | Scenario 3 | — | Scenario premium retained |

| `PREM\_CALL` | 0.022 | Scenario 3 | — | Scenario premium retained |

| `T\_DAYS` | 365 | Scenario 3 | — | One-year settlement period |



\## CIP-Implied Forward

\*\*Calculation:\*\* `1.1535 × (1 + 0.0406 × 365/360) ÷ (1 + 0.025529 × 365/360) = 1.170681`



\*\*Scenario indicative forward:\*\* 1.0910  

\*\*Calculated live forward:\*\* 1.170681  

\*\*Difference:\*\* 0.079681 USD per EUR, or approximately 7.30% higher than the scenario forward.



The difference reflects the current spot rate and interest-rate environment, while the scenario forward was an indicative classroom input.








## FX Lab Cross-Check

I entered the live inputs into the course FX Hedging Lab and compared its results with my Excel workbook. The lab calculated forward proceeds of $14,633,513 and money-market proceeds of $14,633,514, matching the workbook. The lab’s implied and quoted forward rates both rounded to 1.1707, and its parity check passed with an approximately $2 difference caused by rounding.

At the 0% settlement-rate scenario, the lab calculated unhedged proceeds of $14,418,750 and put-hedge proceeds of $14,206,250, also matching the workbook. The remaining sensitivity scenarios followed the same pattern, with only occasional $1 rounding differences. No structural formula corrections were necessary because the workbook and the FX Lab produced consistent results.


To be completed after the live values are entered into the workbook.

