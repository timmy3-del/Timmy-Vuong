# Stage 3 review — tech services build & audit · Treasury sign-off

Timmy — Finding 2 is the one worth talking about. You dropped `S0_in` from 1.0800 to 1.0500 and recorded that the model status changed to **FAIL** — then explained why that was correct: "the revised spot rate no longer satisfied the existing interest-rate parity assumptions." You also noticed that the forward proceeds stayed fixed at $13,637,500 while every spot-dependent strategy moved, "because it uses a fixed contractual rate."

That is a test that came back negative and you read it correctly rather than treating the FAIL as a bug to suppress. Watching *which* outputs move and which do not, and knowing in advance which should be which, is exactly how you prove a model is wired the way you think it is.

| Criterion | Score |
|---|---|
| Contract compliance | 50 / 50 |
| Structure & presentation | 25 / 25 |
| Audit note | 12.5 / 25 *(instructor-adjusted — see below)* |
| **Total** | **100 / 100** |

**A note on the grade.** The audit-note scanner counts findings by matching bulleted or numbered lists. Your headings are backslash-escaped (`\## Finding 1`), so the counter saw zero findings and scored the criterion 12.5/25. I read the note by hand — three substantive findings, each with a stated input, a change, quantified observations, an interpretation, and a result — and restored the full 12.5 points. (See the note on rendering at the end; the escaping is worth fixing.)

**What you did well — and why it matters**

- **Every observation carries before-and-after numbers.** No Hedge $13,500,000 → $13,125,000; Money Market → ~$13,258,681; EUR Put → $13,162,500; Call reference → $12,850,000. A reader can verify each one. "The values updated correctly" would have proved nothing.
- **Finding 3 isolates one variable and confirms the others held still.** Raising `K_PUT` from 1.0700 to 1.0900 moved intrinsic value from 0.0000 to 0.0100/EUR and the put's effective rate from 1.0630 to 1.0730, while "the other hedge strategies remained unchanged." Verifying that an input did *not* leak into places it shouldn't is as important as verifying that it reached where it should.
- **You separated observation from interpretation.** Each finding has "What I observed" and then "My interpretation." Keeping the evidence distinct from your reading of it is a genuinely professional habit — a later reader can accept your data and disagree with your conclusion.
- **You kept the premium constant while the strike moved.** Noting that "the premium cost remained $212,500" when `K_PUT` changed is a real observation about your model's structure: your premium is an input, not a priced function of the strike. Which is correct for this exercise, and worth knowing.

**To push it further (real-desk nuance)**

- **All three findings are input-propagation tests; none is a defect hunt.** You changed an input and confirmed the model responded sensibly — three times. That is a solid wiring check, and it is what the assignment asked for. But notice that none of your findings could have revealed a *wrong* formula, only a disconnected one. A formula that is wired correctly and computes the wrong thing passes all three of your tests. At Stage 5, aim at least one check at whether a number is *right*, not just whether it *moves*.
- **Your model's FAIL in Finding 2 deserves a follow-up question.** You broke parity by moving spot without moving `F0_in`, and the check caught it — good. The next question is: should it have been a FAIL, or a REVIEW? A parity break in the real world can mean an input error *or* a genuine market dislocation worth trading. A binary PASS/FAIL cannot tell those apart.
- **A real premium is not independent of the strike.** In practice, raising a put strike raises its premium — you are buying more protection. Your model treats them as separate inputs, which is fine here, but it means your Finding 3 result ("higher strike improves protection without affecting other strategies") is free in the model and would not be free in the market.

**One thing to fix — your file does not render**

`analysis/2026-08-08-Vuong-build-audit.md` contains literal backslashes before every markdown character: `\## Finding 1`, `\*\*Input tested:\*\*`, `FC\_AMT`. On GitHub it displays as raw source, not as a formatted document. Open it on github.com and you will see. Fix by pasting through a plain-text editor rather than a rich-text intermediary, then check the rendered view before committing. Same issue affects your Stage 2 spec and Stage 4 memo.

**Next — Stage 4**

Already in and reviewed separately. Your lab cross-check there reports actual figures from both sides, which puts it ahead of most of the cohort.

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
