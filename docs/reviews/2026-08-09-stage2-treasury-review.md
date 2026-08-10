# Stage 2 review — tech services · Treasury sign-off

Timmy — the structure here is right: all ten named ranges, a tab per job, the three hedge families each with a formula and a worked placeholder calculation, and a sensitivity plan. Your assumptions section is also unusually readable — writing "EUR/USD quote: a rate of 1.0910 means one euro equals 1.0910 U.S. dollars" in plain language is a kindness to whoever inherits this model, and quote-convention confusion is a real source of expensive errors.

| Criterion | Score |
|---|---|
| Named-range contract & tab architecture | 30 / 30 |
| Calculation flow | 30 / 30 |
| Validation & sensitivity plan | 20 / 20 |
| Reproducibility & prompt log | 20 / 20 |
| **Total** | **100 / 100** |

**Two things to fix before Stage 5 — neither costs you points, both matter**

**1. Six of your ten placeholders are `TBD`.**

`S0_in`, `R_USD`, `R_FC`, `K_PUT`, and `K_CALL` are all listed as TBD with the Stage-4 source given as "Live FX market data" or "Live option quote." Only `F0_in` (1.0910), the premiums, `FC_AMT`, and `T_DAYS` carry actual numbers.

The test for a spec is whether a colleague could build the complete workbook from it without asking you anything. With six inputs blank, they could build the *structure* but could not populate or test it — and neither could you. That is why your own §4 parity check has to be stated so loosely: "the money-market hedge should produce a result reasonably close to the forward hedge." You could not commit to a tolerance because you had no rates to compute one from.

Compare with how a stronger version works: choose indicative placeholders that are *parity-consistent* with your 1.0910 forward — say `S0_in` 1.0700, `R_USD` 4.00%, `R_FC` 2.00% — and then the parity check has a real target and your Stage 3 build has something that can actually fail. Placeholders are not filler; they are what make the model testable before live data arrives.

**2. "Reasonably close" needs a number.**

Every validation rule needs a threshold decided *before* you see the answer, or the tolerance quietly becomes whatever your model produced. Write it as: "the money-market and forward proceeds must agree within 0.05% of notional; a larger gap is treated as an input or formula error." That gives your Stage 3 audit a rule to test against rather than a judgment call.

**One more, and it affects every file you have committed**

Your markdown is escaped. This spec is full of `&#x20;` entities and double-spaced lines; your Stage 3 audit note and Stage 4 memo are worse — they contain literal backslashes (`\## Finding 1`, `\*\*Student:\*\*`, `FC\_AMT`), which means **GitHub renders them as raw text rather than as headings and bold**. Open your own `analysis/2026-08-08-Vuong-build-audit.md` on github.com and you will see it.

This is almost certainly a copy-paste through a converter that escaped the markdown on the way out. The content is fine; the presentation is broken, and on a real desk a document that renders as source code does not get read. The fix is to paste as plain text into a plain editor (VS Code, Notepad) rather than through a rich-text intermediary — then check the rendered view on GitHub before you call a file done.

Also: your tab architecture table lists **Inputs twice** — a copy-paste duplicate worth deleting.

**Next — Stages 3 and 4**

Both are in and reviewed separately. Your Stage 3 input-perturbation tests and your Stage 4 lab cross-check are both genuinely good work — which is exactly why the rendering problem is worth ten minutes of your time.

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
