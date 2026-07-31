\# FX Receivable Exposure and Hedging Plan — U.S. Tech Services Firm



\*\*Created by:\*\* Timmy Vuong

\*\*Updated by:\*\* Timmy Vuong

\*\*Date Created:\*\* July 31, 2026

\*\*Date Updated:\*\* July 31, 2026

\*\*Version:\*\* 1.0

\*\*LLM Used:\*\* ChatGPT

\---



\## Executive Summary (≤150 words)

A U.S. Tech Services Firm expects to receive EUR 12.5 million in one year, creating direct exposure to euro exchange-rate movements. Since the amount is fixed in euros, its eventual dollar value depends entirely on where EURUSD sits when the payment arrives. That sensitivity is significant: at 1.10, the receivable converts to $13.75 million, but if the euro weakens to 1.00, it converts to just $12.50 million—a $1.25 million swing in expected revenue. To manage this risk, the project will evaluate three hedging strategies: a forward contract locked in at 1.0910, a money-market hedge using borrowing and investing, and a EUR put option.



\---



\## Background \& Objectives

Because the firm earns revenue in EUR but manages its cash flow and budgeting in USD, currency movements directly affect its financial planning. If the euro weakens before the payment date, the company will convert its receivable into fewer dollars than expected, regardless of the euro amount itself. The objective is to compare the three hedges and protect expected USD proceeds from budget and profitability impacts.

\---



\## Methods



The forward hedge involves selling EUR 12.5 million forward at 1.0910, locking in approximately $13,637,500. This provides complete USD cash-flow certainty, though it sacrifices any upside if the euro strengthens beyond the forward rate.



The money-market hedge entails borrowing the present value of the EUR receivable, converting it to USD immediately, and investing the proceeds. This achieves certainty similar to a forward but consumes borrowing capacity and requires more transactions to execute.



The EUR put option establishes a minimum EUR selling rate while preserving upside potential if the euro appreciates. Its main drawback is the upfront premium cost, which is paid regardless of whether the option is ultimately exercised.



\---



\## Limitations \& Next Steps

This analysis remains preliminary, as key inputs—the current EURUSD spot rate, applicable interest rates, option strike price, and live market quotes—still need to be collected. The project will proceed through four remaining stages: Stage 2 will design the workbook specification, including inputs, formulas, and validation checks. Stage 3 will build the model with AI assistance, followed by a thorough audit and correction of any errors. Stage 4 will replace placeholder assumptions with sourced, timestamped market data. Stage 5 will validate the results through an independent LLM run and manual checks before delivering the final hedge recommendation.---



\## References

\- Stauffer, Adam. “Stage 1 — Executive Memo.” \*Kumu\*, 2026, https://adamwstauffer.github.io/ai-lms/fx-hedging-stage1.html. Accessed 31 July 2026.



\- Stauffer, Adam. “Example Scenarios — EUR Receivables.” \*GitHub\*, 2026, https://github.com/adamwstauffer/shidler/blob/main/courses/International-Finance-And-Securities/projects/fx-hedging/scenarios.md. Accessed 31 July 2026.

