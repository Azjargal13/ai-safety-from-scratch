# Evaluations

Evaluations (often called “evals”) are one of the most practical and important parts of AI Safety work.

---

## What are evaluations?

Evaluations are systematic tests designed to measure:

- What a model is capable of (especially dangerous capabilities)
- How the model tends to behave (propensities)
- Whether safety measures actually work

Without good evaluations, it is very hard to know how risky a model is or whether progress is being made on safety.

---

## Main types of evaluations

### 1. Dangerous Capability Evaluations

These test whether a model has skills that could be misused or become dangerous if the model is highly autonomous.

Common areas include:

- Cybersecurity (hacking, finding vulnerabilities)
- Biological knowledge and assistance
- Chemical knowledge
- Persuasion and manipulation
- Autonomous replication / self-improvement
- Long-horizon planning and agency
- Deception and scheming ability

### 2. Alignment / Propensity Evaluations

These try to measure the model’s tendencies:

- Does it act deceptively when given the chance?
- Does it pursue goals different from the ones we intended?
- Does it sandbag (hide its true capabilities during testing)?
- Does it seek power or resist being shut down?

### 3. Safety Technique Evaluations

These test whether specific safety methods work:

- Does monitoring actually catch bad behavior?
- Do control protocols remain effective against stronger models?
- How robust is refusal training against jailbreaks?

---

## Why evaluations are hard

- Models can behave differently when they know they are being tested.
- Very capable models may hide abilities (sandbagging).
- Some dangerous capabilities are rare or only appear in complex situations.
- It is difficult to design tests that stay valid as models become smarter.
- There is often a trade-off between making tests realistic and making them safe to run.

---

## Important organizations working on evaluations

- **METR** (formerly part of ARC) — focused on autonomous capabilities and task performance
- **Apollo Research** — specialized in detecting scheming and deceptive behavior
- **UK AI Security Institute** and other government-linked evaluation teams
- Frontier labs themselves (Anthropic, OpenAI, DeepMind) run extensive internal evaluations

---

## Current status (as of late 2026)

Evaluations have improved significantly since 2023.  
Most frontier labs now run structured dangerous capability evaluations before releasing major models, and some publish high-level results.

However, major limitations remain:

- We still lack reliable ways to detect sophisticated deception.
- Evaluations often lag behind the newest capabilities.
- There is no strong consensus on what level of risk should block deployment.

Good evaluations are necessary but not sufficient for safety. They tell us about the current state of a model — they do not by themselves solve alignment or control.

---

## Related concepts

- AI Control
- Scalable Oversight
- Inner Alignment
- Dangerous Capabilities
