# AI Control

AI Control is a pragmatic approach that asks:

> Even if we cannot fully align a model, can we still extract useful work from it while preventing it from causing unacceptable harm?

It is especially relevant if we deploy models that are not fully trusted.

---

## Core idea

Assume the model might be misaligned (or even actively trying to subvert us).  
Then design protocols that still allow us to get useful outputs while limiting the damage the model can do.

This is different from pure alignment research, which tries to make the model internally want the right things.

---

## Common control techniques

- **Monitoring**: Use other models or systems to watch the untrusted model’s outputs or chain-of-thought for signs of bad behavior.
- **Resampling / Rejection sampling**: Generate multiple outputs and only accept ones that pass safety checks.
- **Trusted editing**: Let a weaker but trusted model edit or filter the outputs of a stronger untrusted model.
- **Limited access to tools and internet**: Restrict what the model can act on.
- **Multi-agent protocols**: Make models debate, critique, or oversee each other.
- **Tripwires and shutdown mechanisms**: Systems designed to detect dangerous behavior and stop the model.

---

## When control is useful

- When we have models that are very capable but not fully trusted
- During the transition period before better alignment methods exist
- For high-stakes applications where failure is very costly

Control is not a full solution to alignment, but many researchers see it as an important layer of defense.

---

## Current status (as of late 2026)

- Organizations such as Redwood Research have done significant work on control protocols.
- Labs are increasingly using monitoring and layered safety systems.
- Control techniques are already being applied in practice, but their reliability against highly capable and potentially deceptive models is still an open research question.
