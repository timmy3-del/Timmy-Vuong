\# Stage 5 Independent Validation



\*\*Student:\*\* Timmy Vuong

\*\*Scenario:\*\* 3 — U.S. Tech Services Firm

\*\*Date:\*\* 2026-08-14



## 1. Independent LLM Execution



I opened a fresh LLM conversation and supplied only the following two documents:



\* `docs/specs/2026-08-07-Vuong-tech-services-spec.md`

\* `data/2026-08-08-Vuong-market-data.md`



I did not provide the Excel workbook, workbook results, previous hedge conclusions, or additional calculation guidance.



\*\*Prompt used:\*\*



> Using only the two attached documents, independently calculate the complete FX hedge analysis, including the unhedged position, forward hedge, money-market hedge, put option, call reference, and results at several settlement EUR/USD rates. Show your assumptions and calculations, identify the trade-offs, and recommend a hedging strategy for the CFO.



\*\*Raw LLM output:\*\* [Open the independent LLM output](2026-08-14-Vuong-tech-services-llm-output.md)



## 2. Comparison With the Workbook



The following table will compare the independent LLM analysis with the results produced by my Excel workbook.



| Settlement S\_T | Strategy           | Workbook Result | Independent LLM Result | Difference | Match? |

| -------------: | ------------------ | --------------: | ---------------------: | ---------: | ------ |

|         1.0958 | Unhedged           |$13,697,813      |                        |            |        |

|         1.0958 | Forward            |$14,633,513      |                        |            |        |

|         1.0958 | Money Market       |$14,633,514      |                        |            |        |

|         1.0958 | EUR Put            |$14,206,250      |                        |            |        |

|         1.0958 | EUR Call Reference |$13,422,813      |                        |            |        |

|         1.1535 | Unhedged           |$14,418,750      |                        |            |        |

|         1.1535 | Forward            |$14,633,513      |                        |            |        |

|         1.1535 | Money Market       |$14,633,514      |                        |            |        |

|         1.1535 | EUR Put            |$14,206,250      |                        |            |        |

|         1.1535 | EUR Call Reference |$14,143,750      |                        |            |        |

|         1.2112 | Unhedged           |$15,139,688      |                        |            |        |

|         1.2112 | Forward            |$14,633,513      |                        |            |        |

|         1.2112 | Money Market       |$14,633,514      |                        |            |        |

|         1.2112 | EUR Put            |$14,927,188      |                        |            |        |

|         1.2112 | EUR Call Reference |$15,585,625      |                        |            |        |



## 3. Hand Verification



### Verification 1 — Forward Hedge



\*\*Formula:\*\*



`Forward proceeds = FC\_AMT × F0\_in`



\*\*Substitution:\*\*



`Forward proceeds = 12,500,000 × 1.170681`



\*\*Manual result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Workbook result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Difference:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Conclusion:\*\* `[Pass or issue found]`



### Verification 2 — Money-Market Hedge



\*\*Step 1 — Borrow the present value of the EUR receivable:\*\*



`Borrowed EUR = 12,500,000 ÷ (1 + 0.025529 × 365/360)`



`Borrowed EUR = \_\_\_\_\_\_\_\_\_\_ EUR`



\*\*Step 2 — Convert the borrowed EUR into USD:\*\*



`USD converted = \_\_\_\_\_\_\_\_\_\_ × 1.1535`



`USD converted = $\_\_\_\_\_\_\_\_\_\_`



\*\*Step 3 — Invest the USD until settlement:\*\*



`Settlement proceeds = $\_\_\_\_\_\_\_\_\_\_ × (1 + 0.0406 × 365/360)`



`Settlement proceeds = $\_\_\_\_\_\_\_\_\_\_`



\*\*Manual result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Workbook result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Difference:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Conclusion:\*\* `[Pass or issue found]`



### Verification 3 — EUR Put at a Downside Settlement Rate



\*\*Settlement rate tested:\*\* `S\_T = 1.0958`

\*\*Put strike:\*\* `K\_PUT = 1.1535`

\*\*Put premium:\*\* `PREM\_PUT = 0.017 per EUR`



\*\*Exercise decision:\*\* `[State whether the put is exercised and why.]`



\*\*Gross protected proceeds:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Total premium cost:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Net put proceeds:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Workbook result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Difference:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Conclusion:\*\* `[Pass or issue found]`



## 4. Discrepancy Diagnosis



### Discrepancy 1 — [Strategy and settlement rate]



\*\*Workbook result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Independent LLM result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Manual result:\*\* `$\_\_\_\_\_\_\_\_\_\_`

\*\*Difference:\*\* `$\_\_\_\_\_\_\_\_\_\_`



\*\*Cause:\*\* `[LLM error, workbook error, specification ambiguity, or rounding difference]`



\*\*Explanation:\*\*

`[Explain exactly why the results differed.]`



\*\*Resolution:\*\*

`[Explain whether the workbook, specification, or interpretation should change.]`



## 5. Specification Retrospective



### What the Independent LLM Did Correctly



`[Describe the calculations and interpretations that agreed with your workbook and manual verification.]`



### What the Independent LLM Got Wrong or Assumed



`[Identify errors, unsupported assumptions, or differences in interpretation.]`



### Improvements for Specification Version 2



`[Explain what you would clarify in the specification so that another analyst could reproduce the model more accurately.]`



