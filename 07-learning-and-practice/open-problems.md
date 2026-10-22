# Open Problems in AI Safety

As of late 2026, significant progress has been made, but many of the most important problems remain unsolved. This page summarizes the major open challenges.

---

## 1. Inner Alignment / Goal Robustness

We still do not have reliable methods to ensure that a model’s internal goals remain aligned with the training objective once the model is more capable or faces new situations.

Key difficulties:

- Detecting goal misgeneralization
- Preventing or detecting deceptive alignment / scheming
- Understanding what objectives are actually learned inside large models

---

## 2. Scalable Oversight

How can humans (or weaker AIs) reliably supervise systems that are smarter than them?

Current approaches (debate, process supervision, weak-to-strong generalization, recursive oversight, etc.) show promise but are not yet reliable enough for highly capable systems.

---

## 3. Interpretability

We cannot yet robustly understand the internal reasoning of frontier models.

Open questions include:

- Can we fully reverse-engineer important algorithms inside large networks?
- Can we reliably detect deception or hidden goals through interpretability tools?
- Will interpretability methods scale to future, more complex models?

---

## 4. Honest Reporting & Eliciting Latent Knowledge (ELK)

How do we get models to accurately report what they know, especially when they might have incentives to hide information or deceive?

---

## 5. Evaluation of Dangerous Capabilities & Propensity

We need better ways to measure:

- Whether a model is sandbagging (hiding capabilities)
- Whether a model would scheme or act deceptively if given the chance
- Long-horizon agency, situational awareness, and power-seeking tendencies

Current evaluations are useful but still incomplete and gameable.

---

## 6. AI Control

Even if a model is not fully aligned, can we design protocols that let us extract useful work while limiting catastrophic outcomes?

Promising work exists (especially from Redwood Research and others), but robust control against very capable and potentially deceptive models remains an open challenge.

---

## 7. Value Specification & Robust Preference Learning

How do we specify what we want in a way that remains correct under strong optimization pressure?

Problems include reward hacking, sycophancy, preference inconsistency, and difficulty capturing complex human values.

---

## 8. Generalization to Superhuman Systems

Most current methods are tested on systems that are at or below human level in most domains. It is unclear which techniques will continue to work as models become significantly superhuman in more areas.

---

## 9. Multi-Agent and Systemic Risks

As many advanced AI systems interact with each other and with society, new risks appear (coordination failures, collusion, cascading failures, etc.). These are still underexplored compared to single-agent alignment.

---

## 10. Governance & Institutional Questions (Technical Interface)

While not purely technical, there are important open problems at the intersection of technical safety and governance, such as:

- What evidence should be required before deploying more powerful systems?
- How can external parties verify safety claims?
- How should safety standards scale with capability?

---

## Summary

The field has moved from mostly conceptual arguments to a mix of theoretical and empirical work. However, for the most advanced future systems, we still lack strong, reliable solutions to the core problems of alignment, oversight, and control.

Progress is being made, but the gap between capabilities and safety understanding remains a central concern.
