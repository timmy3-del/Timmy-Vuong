# Stage 5 review — tech services LLM analysis & validation · Treasury sign-off

Timmy — I want to be straight with you about this grade, because the automated pass and I disagreed and I moved it **down**, which I did for exactly one student in this cohort.

The first pass scored this stage **80**. It counted 16 rows in your comparison table and 16 in your hand-verification section and awarded 25/25 for each. But it was counting table *structure*, not table *content*. When I opened the file:

- In the comparison table, the **Independent LLM Result**, **Difference**, and **Match?** columns are empty on all fifteen rows. Only the workbook column is filled.
- Every hand-verification result is a blank placeholder: `Manual result: $__________`, `Workbook result: $__________`, `Difference: $__________`, `Conclusion: [Pass or issue found]`.
- All three retrospective subsections still contain the bracketed template prompts: `[Describe the calculations and interpretations that agreed…]`.

None of those are graded as errors. They are simply not done, and Stage 5 is *the validation stage* — comparing, diagnosing, and recomputing is the whole assignment. I re-scored it at **70**, which is the stage floor. Worth saying plainly: even reading your recommendation memo as generously as I can, the floor is where this lands, so the memo is not what is costing you here.

| Criterion | Score |
|---|---|
| LLM execution & comparison | 12 / 25 |
| Hand verification | 8 / 25 |
| Recommendation & executive voice | 18 / 25 |
| Spec retrospective | 0 / 17 |
| Repo polish | 6.4 / 8 |
| **Raw** | **44.4 / 100** |
| **Stage floor applied** | **70 / 100** |

**What is genuinely good here — and it is more than you might think**

- **You actually ran the independent LLM.** `analysis/2026-08-14-Vuong-tech-services-llm-output.md` is committed, and your prompt is documented and correctly scoped: *"Using only the two attached documents, independently calculate the complete FX hedge analysis…"* with an explicit statement that you withheld the workbook, prior results, and calculation guidance. Part 1 is done properly. What is missing is Part 2 — reading the output you already have and writing down what it said.
- **Your workbook is correct.** I verified it independently: `12,500,000 × 1.095825 = $13,697,812.50` ✓, `× 1.1535 = $14,418,750` ✓, `× 1.211175 = $15,139,687.50` ✓, forward at `12,500,000 × 1.170681 = $14,633,512.50` ✓, put at `14,418,750 − 212,500 = $14,206,250` ✓. Every figure in your table ties. The model is sound; the validation of it is what stopped short.
- **Your memo's "Limitations & Next Steps" is the best in the cohort.** *"The calculated forward rate of 1.170681 is indicative rather than an executable dealer quote."* Then a six-step execution checklist — confirm the receivable, request an executable quote, compare against the indicative rate, review counterparty credit and collateral, obtain treasury authorization, document and monitor. Followed by what to do if the receivable amount or date changes, *"so that its notional amount and maturity continue to match the underlying receivable."* That is real treasury operations thinking, and most of your classmates did not go near it.
- **You excluded the call for the right reason.** *"Because a call provides the right to buy euros, it does not match the company's need to sell the euros it will receive."* Correct, and correctly derived from the direction of the exposure.

**The blanks are twenty minutes of work, and I will give you the numbers**

You wrote every formula and every substitution. What is missing is pressing `=`.

**Verification 1 — Forward.** You already have `12,500,000 × 1.170681`:
```
Manual result:   $14,633,512.50
Workbook result: $14,633,513
Difference:      $0.50   (display rounding)
Conclusion:      Pass
```

**Verification 2 — Money market.** Your three substitutions are written; run them:
```
Step 1: 12,500,000 ÷ (1 + 0.025529 × 365/360) = 12,500,000 ÷ 1.0258836 ≈ €12,184,615
Step 2: 12,184,615 × 1.1535                    ≈ $14,054,953
Step 3: 14,054,953 × (1 + 0.0406 × 365/360)    ≈ $14,633,5xx
```
Then say the one thing that matters: it lands on the forward result, because `F0_in` was derived from these same two rates via covered interest parity. The $1 gap you already noted is display rounding — you got that right in the memo.

**Verification 3 — Put.** At the downside scenario, `S_T = 1.095825 < K_PUT = 1.1535`, so the floor binds:
```
Gross = 12,500,000 × MAX(1.095825, 1.1535) = 12,500,000 × 1.1535 = $14,418,750
Less premium                                = 12,500,000 × 0.017 = $212,500
Net                                         = $14,206,250          → matches workbook
```

**The comparison table.** Open your own LLM output file, read its numbers for each strategy at each `S_T`, and fill the three empty columns. Where they differ, say which of three things happened: LLM error, workbook error, or spec ambiguity. That single classification column is the most heavily weighted judgment in this stage — it is the difference between "the numbers agree" and "I know *why* they agree."

**The retrospective** asks three questions that only you can answer: what did the LLM get right, what did it get wrong or have to guess, and what does that reveal about your Stage 2 spec. "The spec was perfect" is not an acceptable answer — candour is what is graded. If your run genuinely matched everywhere, the honest finding is about the *test*: which strategies could not have disagreed (the forward and money market do not move with `S_T` at all), and what a stronger comparison would have covered.

**One number your memo is missing**

Your Methods section says the put *"produces net proceeds of $14,206,250, which is less than the forward hedge"* — true, but it does not say by how much, or when that flips. Both are one line of arithmetic:

```
Floor gap:  14,633,513 − 14,206,250 = $427,263 below the forward
Breakeven:  (14,633,513 + 212,500) / 12,500,000 = 1.18768  →  2.96% above spot
```

So the CFO is being asked to give up $427,263 of guaranteed proceeds, and pay $212,500, in exchange for participation that only starts after a **3% euro rally**. That sentence turns your comparison into a decision.

**A formatting problem that is costing you across every document**

Every markdown character in both files is escaped with a backslash — `\#`, `\*\*`, `\###`, `\---`, `S\_T`. On GitHub that renders literally: your headings show up as `\### Executive Summary` instead of as headings, and your bold text shows the asterisks. It is why the automated pass could only find two of the five required sections in your memo.

This happens when a document is exported to markdown from Word or Google Docs — the converter escapes the syntax so it will not be interpreted. The fix is a find-and-replace: remove `\` before `#`, `*`, `-`, and `_`. Write directly in a plain text or markdown editor and it will not recur.

Related: your memo uses **Executive Summary / Background & Objectives / Methods / Limitations & Next Steps**, but the brief asked for the A–E arc — **A. Exposure Summary, B. Hedge Outcomes, C. Sensitivity Interpretation, D. Recommendation, E. Executive Justification**. Almost all of your content maps onto it; it is mostly a matter of re-heading the sections and splitting "Methods" into B and C. The structure is not bureaucracy — it is the order a CFO reads in: what is at risk, what are the options, how do they behave, what do you advise, why.

**Repo polish — 1.6 points**

`LICENSE` is the only open item. Add an MIT license at the repo root.

**Where this leaves you**

The gap between a 70 and a 95 here is not analytical ability — your workbook is right, your memo has genuine professional judgment in it, and you ran the independent LLM correctly. It is that three sections of the validation document were left as scaffolding. If you fill them in, this stage is re-gradable at the post-deadline sweep, and the numbers above are most of what you need.

— Treasury

---

### How to work this review — professional workflow

Treat this PR the way an analyst treats feedback from Treasury — a review is a proposal to engage with, not a checklist to rubber-stamp:

1. **Read it yourself first.** Understand each point and form your own view before changing anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM (pushback pass).** Paste this review and your spec into your AI assistant and ask it to (a) explain anything you're unsure of more deeply, and (b) argue the *other side* — where might the reviewer be wrong, and what would you give up by making each change. You're building judgment, not just executing edits.
3. **Decide, then draft the changes with the LLM.** For the points you accept, have the AI help implement them — you specify exactly what and why. Your spec is the prompt; precise in, correct out.
4. **Verify — non-negotiable.** Re-run your own checks (`scripts/recalc.py`, the parity tie-out, sensitivity continuity, no error cells) and confirm the numbers before you commit. An AI will hand you a confident wrong edit; verification is what makes the result *yours*.
5. **Close the loop on the PR.** Reply in the thread with what you changed, what you pushed back on and why, then commit and push. Writing down the reasoning is exactly how this works on a real team.

*This is the same human-in-the-loop discipline the whole project is built on: the LLM drafts, you edit and verify, and you own the result.*
