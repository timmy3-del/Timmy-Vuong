\# Stage 3 Build Audit



\*\*Student:\*\* Timmy Vuong

\*\*Scenario:\*\* 3 — U.S. Tech Services Firm

\*\*Date:\*\* 2026-08-08



\## Finding 1 — Receivable Amount Test



\*\*Input tested:\*\* `FC\_AMT`



\*\*Change made:\*\* Increased the receivable amount from $12,500,000 to $13,000,000.



\*\*What I observed:\*\* After temporarily increasing the receivable amount, I saw the related USD proceeds update on the Cover sheet. The values in the Sensitivity table and the accompanying chart also changed, while the validation checks continued to pass. This demonstrated that the receivable input was correctly connected to the model’s formulas.



\*\*Result:\*\* Pass



\## Finding 2 — Spot Rate Test



\*\*Input tested:\*\* `S0\_in`



\*\*Change made:\*\* Decreased the EUR/USD spot rate from 1.0800 to 1.0500.



\*\*What I observed:\*\* The No Hedge proceeds decreased from $13,500,000 to $13,125,000, while the Forward proceeds remained fixed at $13,637,500. The Money Market proceeds decreased to approximately $13,258,681, the EUR Put proceeds decreased to $13,162,500, and the EUR Call reference proceeds decreased to $12,850,000. The Sensitivity table and chart also updated. The model status changed to FAIL because the revised spot rate no longer satisfied the existing interest-rate parity assumptions.



\*\*My interpretation:\*\* This test showed that the spot-dependent strategies responded correctly to the lower EUR/USD rate, while the forward hedge remained unchanged because it uses a fixed contractual rate. The validation warning also demonstrated that the model detects inconsistent market assumptions.



\*\*Result:\*\* Expected validation warning



\## Finding 3 — Put Strike Test



\*\*Input tested:\*\* `K\_PUT`



\*\*Change made:\*\* Increased the EUR put-option strike rate from 1.0700 to 1.0900.



\*\*What I observed:\*\* The put’s intrinsic value increased from 0.0000 to 0.0100 per EUR, while the premium cost remained $212,500. The EUR Put proceeds increased from $13,287,500 to $13,412,500, and its effective conversion rate increased from 1.0630 to 1.0730. The other hedge strategies remained unchanged. The EUR Put results also increased in the weaker-euro scenarios on the Sensitivity sheet, raising the downside protection shown by the chart. The model status remained PASS.



\*\*My interpretation:\*\* This test showed that a higher put strike provides a stronger minimum conversion rate and improves downside protection without affecting the forward, money-market, no-hedge, or call calculations.



\*\*Result:\*\* Pass



