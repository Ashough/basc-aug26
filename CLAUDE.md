# Project rules for Claude Code

## What this repo is

Companion code for a conference talk (OWASP Boston, Aug 12 2026). Two Jupyter
notebooks demonstrating that a fairness defect in an ML model creates an
exploitable attack surface.

The owner is a security practitioner, **not a professional developer**. Explain
what you are doing in plain language. Do not assume familiarity with git,
package managers, or Python tooling.

---

## THE ONE RULE THAT MATTERS

**The notebooks in `notebooks/` are verified artifacts. Every number in them has
been checked and is quoted verbatim on stage in front of a technical audience.**

Do NOT, unless explicitly and specifically asked in the current message:

- refactor, reformat, or "clean up" notebook code
- change variable names, random seeds, model hyperparameters, thresholds, or
  data-generation parameters
- upgrade, pin, or swap libraries
- re-run notebooks in a way that overwrites saved cell outputs
- "improve" the statistics, add cross-validation, or tune anything
- reorganize cell order or merge/split cells

A change that shifts a printed number by one decimal place breaks the talk.
Silent improvements are worse than no help.

If you believe something in a notebook is wrong, **say so and stop.** Do not fix
it. Report what you found and wait.

---

## What you SHOULD help with

- README, documentation, and repo hygiene
- `.gitignore`, license, requirements
- Git operations: init, commit, branch, push, remote setup — explaining each step
- GitHub setup: creating the repo, adding Colab badge links, checking that
  notebooks render on github.com
- Answering "what does this command do" and "did that work"

## Working style

- Take one step at a time. Show the command, explain it, run it, confirm it worked.
- Before any destructive or irreversible operation (force push, rebase, branch
  delete, file delete, history rewrite), stop and ask.
- Never commit secrets, tokens, or `.env` files.
- Prefer the simplest thing that works over the idiomatic thing.
- If a task would take more than about five steps, outline the plan first and
  get agreement before starting.

## Repo layout

```
README.md          public-facing; explains both demos
CLAUDE.md          this file
LICENSE            MIT
requirements.txt   local-run only; Colab needs none of it
.gitignore
notebooks/
  01_fairness_side_channel.ipynb   4-act attack + remediation  [FROZEN]
  02_fairwashing.ipynb             surrogate explanation attack [FROZEN]
```

## Facts about the demos (do not restate these incorrectly)

- Data is **synthetic**; the bias is deliberately introduced. This is stated in
  the README and must stay stated.
- Notebook 1 headline numbers: reported AUC 0.778 vs true AUC 0.641; 270 probes;
  clear rate 63% → 98%; naive fix leaves disparity ~unchanged; real fix moves
  portfolio catch rate 18.6% → 21.0% and false declines 6.20% → 6.03%.
- Notebook 2 headline numbers: 96.7% surrogate fidelity; 98.0% of declined
  thin-file transactions flip on tenure/instrument alone.
- The remediation **reduces** the attack, it does not eliminate it. Never write
  copy claiming otherwise.
