# Stage 4 review — tech services market data & population · Treasury sign-off

Timmy — your `R_FC` is the best-sourced euro leg in the cohort. You used the **ECB AAA euro-area government yield curve, one-year spot rate** (2.5529%), pulled straight from the ECB Data Portal API with the series key in the URL, and your reason is exactly right: "an official one-year euro-area government yield matching the exposure horizon."

Most of the cohort reached for the ECB deposit facility rate — an *overnight* policy rate — against a 365-day horizon, because it is easier to find. That mismatch quietly distorts every forward and money-market number downstream. You went and got the tenor-matched curve point. That is the harder, correct choice, and you made it on both legs: DGS1 for the dollar because "the one-year Treasury maturity matches the 365-day exposure."

| Criterion | Score |
|---|---|
| Data quality & provenance | 50 / 50 |
| Model resolves cleanly | 33 / 33 |
| Lab cross-check | 17 / 17 |
| **Total** | **100 / 100** |

**What you did well — and why it matters**

- **You actually ran the lab and reported its numbers.** Forward proceeds $14,633,513 against money-market $14,633,514; implied and quoted forwards both rounding to 1.1707; parity passing on a ~$2 rounding difference; and at the 0% scenario, unhedged $14,418,750 and put-hedge $14,206,250 — all matching the workbook, "with only occasional $1 rounding differences." That is a real cross-check. A large part of the cohort asserted their workbook and the lab *should* agree and reported no figures at all.
- **You separated data date from retrieval date.** "Data date: 2026-08-07 — latest available market close" against "Retrieval date: 2026-08-08," with per-input observation dates on top of that. Three timestamps, each doing a job.
- **Your API link is re-pullable.** The `R_FC` URL carries the full series key and a `startPeriod` — anyone can re-run your exact query. That is provenance at its strongest: not a citation, but a reproduction recipe.
- **You quantified the forward gap.** 1.0910 → 1.170681, "0.079681 USD per EUR, or approximately 7.30% higher," attributed to the live spot and rate environment versus an indicative classroom input.

**To push it further (real-desk nuance)**

- **Your put figure exposes a convention you should name.** The lab's put-hedge $14,206,250 is exactly `12,500,000 × (1.1535 − 0.017)` — the premium subtracted **undiscounted**. Your workbook agrees, so nothing is broken. But the premium is paid at inception and the proceeds arrive in 365 days, so comparing them without carrying the premium forward at `R_USD` understates its true cost by about $8,600 here. One of your classmates found exactly this as a discrepancy against the lab and documented it as a convention difference. Yours matches because you made the same choice the lab did — worth stating explicitly in your assumptions rather than leaving implicit.
- **Your parity check is close to circular.** `F0_in` is CIP-implied from the same `S0_in`, `R_USD`, and `R_FC` that drive the money-market leg, so a ~$2 gap is arithmetic rather than evidence. It confirms your implementation; it cannot detect a wrong input or a market dislocation. Say so, and note what is missing: no quoted market forward ever enters the model, so dealer spread and cross-currency basis are invisible by construction.
- **Two lines to delete.** The memo ends with "**To be completed after the live values are entered into the workbook**" — a leftover template instruction sitting after the section it refers to, which you did complete. And the file is escaped markdown (`\## Stage 4 Market Data Memo`, `\*\*Student:\*\*`, `FC\_AMT`), so it renders as raw text on GitHub. Same fix as your Stage 2 and Stage 3 files: paste through a plain-text editor and check the rendered view before committing.

**Next — Stage 5**

Hand the workbook and your Stage 2 spec to an LLM, get its analysis, then break it. Recompute at least three outputs by hand with the arithmetic written out — forward proceeds, the put floor, and the crossover spot where the put overtakes the forward (with your undiscounted premium that is simply `F0_in + PREM_PUT` = 1.170681 + 0.017 = 1.187681). Then write the recommendation in a CFO's voice framed on risk tolerance. Your spec retrospective has an easy, honest opening: six of your ten Stage 2 placeholders were `TBD`, and here is what filling them in actually changed.

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
