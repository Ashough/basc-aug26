# AI Ethics Is a Security Problem — Demos

Companion code for the talk at **OWASP Boston, August 12, 2026**.
Mardiros Merdinian · [Substack](#) · [SAIEF](#)

Two notebooks. Both run in Google Colab with no installation and no API keys.

---

## The argument these demos support

Security teams are rigorous about the half of the OWASP Top 10 that *looks* like
security. There is a second class of attack path that gets induced by an ethics
failure — and it goes unaddressed, because it doesn't pattern-match to "a hack."
No adversary. No CVE. No alert.

These notebooks make two of those paths concrete and engineerable.

---

## Notebook 1 — The Fairness Gap Is a Map

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](#)

A card-not-present fraud scorer. The model never sees a protected attribute — it
sees payment instrument and account tenure, which are legitimate risk signals.

**The defect isn't in the features. It's in the labels.** Fraud labels come from
investigations, and the legacy rules engine investigated thin-file accounts far
more aggressively than established ones. The model learns *where you looked*,
not *where the crime is*.

Four acts:

1. **Leak** — an attacker with a binary approve/decline oracle recovers the
   model's decision logic in 270 probe transactions.
2. **Game** — one field change takes the attacker's clear rate from 63% to 98%.
3. **The fix everyone ships** — delete the offending features. The attack script
   returns zero. The disparity barely moves, and the leak reappears on a feature
   nobody thought was sensitive.
4. **The fix that works** — a random audit sample to break the label bias.
   Attack advantage goes negative, and the portfolio catches *more* fraud while
   declining *fewer* legitimate customers.

**Where this lives in the OWASP taxonomy:** it doesn't, cleanly. The nearest
neighbour is ASI07 (Insecure Inter-Agent Communication), but that covers
inter-agent channels, not a model leaking its own decision boundary. The LLM-side
neighbour is model inversion under LLM02, but that's data disclosure rather than
decision-logic leakage. **Naming this gap is the contribution.**

## Notebook 2 — The Explanation Is Not the Reason

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](#)

Same model, same defect. This time the target isn't the model — it's the artifact
a human reviewer trusts in order to decide whether to trust the model.

A surrogate fitted only on *sanitized* features reproduces the biased model's
decisions with **96.7% fidelity** while never touching tenure or instrument. It
produces clean, plausible, entirely sanctioned explanations.

Then the counterfactual: change only the two features the explanation never
mentions, and **98% of those declines reverse.**

The explanation is 96.7% faithful and 98% wrong. It predicts *what* the model
decides and describes a *reason* that isn't the reason.

**OWASP mapping:** ASI09 Human-Agent Trust Exploitation — "Fake Explainability."

---

## Running them

**Colab (recommended):** click a badge above. Nothing to install.

**Locally:**

```bash
pip install -r requirements.txt
jupyter notebook notebooks/
```

Both notebooks are seed-fixed and deterministic. Every number in the talk
reproduces exactly. Runtime is a few seconds each.

---

## About the data

The datasets are **synthetic, and the bias is deliberately introduced.** These
notebooks do not claim that any real payment processor is biased — that would be
a different project and a different set of legal problems. The bias is the
*premise*. The finding is what an attacker can extract once it exists.

---

## A note on the fix

The random-audit remediation reduces the attack; it does not eliminate it. There
is a genuine risk differential in the simulated population, so some signal
survives and should. Any control that claims to zero an attack surface is
overselling.

---

## Contributing

The OWASP GenAI Security Project is open and actively takes contributions. If you
work on formalizing ethics-induced attack surfaces into the taxonomy, that's a
better outcome than anything in this repo.

- [OWASP GenAI Security Project](https://genai.owasp.org)

Issues and PRs welcome here too — particularly if you can break one of these
demos or show that a mechanism doesn't hold.

## License

MIT. See [LICENSE](LICENSE).
