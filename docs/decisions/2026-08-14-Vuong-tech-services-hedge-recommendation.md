\# U.S. Tech Services Firm — EUR Receivable Hedge Recommendation



\*\*Created by:\*\* Timmy Vuong  

\*\*Updated by:\*\* Timmy Vuong  

\*\*Date Created:\*\* 2026-08-14  

\*\*Date Updated:\*\* 2026-08-14  

\*\*Version:\*\* 1.0  

\*\*LLM Used:\*\* ChatGPT — organization and feedback



\---





\### Executive Summary



The company faces exchange-rate risk on a EUR 12,500,000 receivable due in 365 days. If the euro weakens before settlement, each euro will convert into fewer U.S. dollars. The company would therefore receive less than expected and face greater uncertainty in its cash flow and budgeting.



To manage this risk, we recommend a one-year forward contract to sell the EUR 12,500,000 receivable at the calculated indicative forward rate of 1.170681 USD per EUR. This would lock in proceeds of approximately $14,633,513 at settlement. The forward provides predictable cash flow, requires no upfront option premium, and is simpler to execute than the borrowing and investing transactions required by a money-market hedge. The main trade-off is that the company would give up additional USD proceeds if the euro strengthens above the forward rate.



\---



\### Background \& Objectives



The U.S. Tech Services Firm operates and prepares its financial plans in U.S. dollars, but it expects to receive EUR 12,500,000 in 365 days. Because the payment is fixed in euros, its final USD value will remain uncertain until the company receives and converts the currency.



At the current spot rate of 1.1535 USD per EUR, the receivable would convert to approximately $14,418,750. If the euro depreciates to the downside settlement rate of 1.0958, however, the unhedged proceeds would fall to approximately $13,697,813. This represents a potential decrease of approximately $720,937 from the current spot-rate value. This difference demonstrates how leaving the exposure unhedged could put the expected USD cash proceeds at risk.



The objective of this analysis is to protect the dollar value of the receivable, reduce uncertainty, and provide management with a dependable amount for budgeting and financial planning.



\---



\### Methods



I evaluated the unhedged position, forward contract, money-market hedge, and EUR put using my Excel workbook, an independent LLM analysis, and three manual verification calculations.



| Strategy     | Downside `S\_T = 1.0958` | Base `S\_T = 1.1535` | Upside `S\_T = 1.2112` |

| ------------ | ----------------------: | ------------------: | --------------------: |

| Unhedged     |             $13,697,813 |         $14,418,750 |           $15,139,688 |

| Forward      |             $14,633,513 |         $14,633,513 |           $14,633,513 |

| Money Market |             $14,633,514 |         $14,633,514 |           $14,633,514 |

| EUR Put      |             $14,206,250 |         $14,206,250 |           $14,927,188 |



\*\*Unhedged.\*\* Remaining unhedged gives the company the full benefit if the euro strengthens, but it offers no protection if the euro weakens. Across the scenarios considered, the USD proceeds ranged from approximately $13.70 million to $15.14 million. This makes remaining unhedged the alternative with the greatest cash-flow uncertainty.



\*\*Forward contract.\*\* A forward contract fixes the proceeds at approximately $14,633,513 regardless of the settlement spot rate and requires no upfront option premium. This certainty comes with a trade-off: the company would not benefit if the euro appreciates above the forward rate of 1.170681.



\*\*Money-market hedge.\*\* The money-market hedge produces approximately $14,633,514, which is nearly identical to the forward result, as expected under interest-rate parity. The one-dollar displayed difference is attributable to rounding. Although the money-market hedge also provides predictable proceeds, it requires the company to borrow euros, convert them into dollars, and invest the resulting USD. These steps use borrowing capacity and create greater operational complexity than a forward contract.



\*\*EUR put option.\*\* The put protects the receivable if the euro falls below the strike rate of 1.1535 while allowing the company to benefit if the euro strengthens. This flexibility requires an upfront premium of $212,500, which must be paid whether or not the option is exercised. In the downside case, the put produces net proceeds of $14,206,250, which is less than the forward hedge.



\*\*EUR call option.\*\* The call is included only as a reference calculation. Because a call provides the right to buy euros, it does not match the company’s need to sell the euros it will receive. It is therefore not an appropriate protective hedge for this exposure.



\*\*Why the forward provides the best balance.\*\* The forward provides approximately the same protected proceeds as the money-market hedge but requires fewer transactions, creates less operational complexity, and does not require an upfront option premium. Its main disadvantage is the loss of additional upside if the euro appreciates significantly. Given the company’s objective of protecting its expected USD proceeds and improving budgeting certainty, this trade-off is reasonable.



\## Limitations \& Next Steps



The results depend on the market rates observed during Stage 4. The model does not include transaction costs, bid-ask spreads, bank fees, taxes, liquidity constraints, or counterparty-credit risk. The calculated forward rate of 1.170681 is indicative rather than an executable dealer quote, so the actual proceeds may differ when the company enters the contract.



Before implementing the recommendation, the company should:



1\. Confirm that the EUR 12,500,000 receivable will be received in 365 days.

2\. Request an executable forward quote from an approved counterparty.

3\. Compare the executable quote with the calculated indicative rate of 1.170681.

4\. Review the counterparty’s credit terms and any collateral or fee requirements.

5\. Obtain the required treasury authorization.

6\. Document and monitor the hedge until settlement.



If the receivable amount or settlement date changes before payment, the company should promptly reassess the exposure. Treasury may need to amend, partially offset, or replace the forward contract so that its notional amount and maturity continue to match the underlying receivable. Any adjustment costs should be evaluated and documented to prevent the company from becoming overhedged or underhedged.



\---



\## References



\- Stage 2 technical specification: `docs/specs/2026-08-07-Vuong-tech-services-spec.md`

\- Stage 3 Excel workbook: `models/builds/2026-08-08-Vuong-tech-services-model.xlsx`

\- Stage 4 market-data memo: `data/2026-08-08-Vuong-market-data.md`

\- Stage 5 validation report: `analysis/2026-08-14-Vuong-tech-services-validation.md`

