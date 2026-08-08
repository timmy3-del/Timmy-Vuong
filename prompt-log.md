July 31, 2026 — Stage 0 Bio Revision



Prompt: Expand my GitHub portfolio bio to 100–150 words. Include my year and Finance major at Shidler, relevant skills and interests, hospitality experience, and goal of moving from property operations into asset management.



How I used the response: I reviewed the draft, revised the wording to reflect my own voice, and confirmed that my education, experience, and career goals were accurate.



July 31, 2026 — Stage 1 Executive Memo



Prompt: Help me plan and review a 300–400-word executive memo for Scenario 3, a U.S. Tech Services Firm expecting a EUR 12.5 million receivable in one year. Check that the memo explains the exposure, quantifies the USD risk, compares a forward at 1.0910, a money-market hedge, and a put option, and previews Stages 2–5.



How I used the response: I drafted each section in my own words and used the feedback to verify the currency calculations, explain the hedge trade-offs clearly, complete the project roadmap, and reduce the memo to the required word count.



\## 2026-08-07 — Stage 2 Technical Specification



\*\*Task:\*\* Develop validation rules for the FX hedging model.



\*\*Prompt used:\*\* “Can you solve it and make it copy and pasteable?”



\*\*AI suggestion:\*\* ChatGPT proposed a validation table covering required inputs, formula checks, interest-rate parity, the option floor, sensitivity scenarios, and error messages.



\*\*My review and changes:\*\* I renamed several validation labels, clarified the failure actions, and simplified the descriptions while keeping the required formulas and 0.5% parity tolerance unchanged.



\*\*Final decision:\*\* I retained the required formulas and named ranges but revised the explanations to reflect my own understanding of the model.



\## 2026-08-08 — Stage 3 AI-Assisted Build



\*\*Task:\*\* Build and troubleshoot the Excel FX transaction-hedging model for Scenario 3.



\*\*Prompt used:\*\* “Help me build and troubleshoot a formula-driven Excel workbook for a U.S. Tech Services Firm expecting a EUR 12,500,000 receivable in one year. The workbook should compare no hedge, a forward hedge, a money-market hedge, a EUR put, and a EUR call reference. It should also include sensitivity analysis, named ranges, validation checks, and the required formatting.”



\*\*AI suggestion:\*\* ChatGPT helped develop the workbook structure, formulas, named ranges, strategy calculations, sensitivity table, chart, and validation checks. It also helped identify and correct formula-reference problems that initially caused Excel errors.



\*\*My review and changes:\*\* I opened the workbook in Excel, reviewed the input values and formulas, and personally completed three audit tests. I changed `FC\_AMT`, `S0\_in`, and `K\_PUT` individually and observed how the Cover, Sensitivity, and Checks sheets responded. I documented the results in my Stage 3 build-audit note and restored every input to its original value after testing.



\*\*Final decision:\*\* I retained the completed workbook after confirming that the model responded correctly to the three input tests, the formulas recalculated properly, and the Cover sheet returned to `MODEL STATUS PASS`.


## 2026-08-08 — Stage 4 Market Data and Population

**Task:** Replace the Stage 3 placeholder assumptions with sourced market data, calculate the CIP-implied forward, populate the workbook, and cross-check the results.

**Prompt used:** “Help me complete Stage 4 for Scenario 3. Find reputable sources for the latest EUR/USD spot rate and one-year USD and EUR rates, show the covered-interest-parity forward calculation, and guide me through documenting and entering the values into my workbook.”

**AI suggestion:** ChatGPT identified the ECB EUR/USD reference rate, the FRED one-year U.S. Treasury rate, and the ECB one-year euro-area government yield. It calculated a CIP-implied forward of 1.170681 and suggested setting both option strikes equal to the live spot rate of 1.1535 while retaining the scenario-provided premiums.

**My review and changes:** I recorded each value, source, observation date, and rationale in the market-data memo. I entered the live values only through the named-range input cells and confirmed that the Cover sheet showed `MODEL STATUS PASS`. I also checked that the Sensitivity table and chart recalculated around the new spot rate.

**Final decision:** I retained the sourced values and CIP-implied forward after comparing the workbook with the course FX Hedging Lab. The forward, money-market, put, and sensitivity results matched, with only insignificant rounding differences. No structural formula corrections were required.



