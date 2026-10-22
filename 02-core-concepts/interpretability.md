# Interpretability

Interpretability is the attempt to understand what is happening *inside* AI models.

---

## Why it matters

Current large language models are mostly black boxes.  
We can see the inputs and outputs, but we have only limited understanding of the internal computations.

Without interpretability, it is hard to:

- Detect whether a model has learned unwanted goals
- Notice deceptive or scheming behavior
- Debug failures
- Build justified confidence in a model’s safety

Better interpretability would help with both outer and inner alignment, as well as control and evaluations.

---

## Two main flavors

### 1. Behavioral / Black-box interpretability

Studying the model by looking at its inputs and outputs only.

- Probing with carefully designed tests
- Looking at chain-of-thought reasoning
- Activation steering (changing behavior by modifying internal activations without fully understanding them)

### 2. Mechanistic interpretability

Trying to reverse-engineer the actual algorithms running inside the network.

- Finding “features” (meaningful directions in activation space)
- Identifying “circuits” (groups of neurons that perform specific functions)
- Using tools like sparse autoencoders to discover more human-interpretable features

Mechanistic interpretability is harder but potentially more powerful.

---

## Key progress and limitations (as of 2026)

**Progress**

- Sparse autoencoders have helped discover many interpretable features in large models.
- Researchers have reverse-engineered some simple circuits (e.g. induction heads, certain factual recall mechanisms).
- Activation steering can control some high-level behaviors.

**Limitations**

- We still cannot fully understand large models.
- Many important internal processes remain opaque.
- Scaling interpretability methods to the largest models is still difficult and expensive.
- Even when we find features, connecting them reliably to high-level goals or deception is hard.

---

## Important related ideas

- **Features**: Directions in activation space that correspond to meaningful concepts.
- **Circuits**: Sub-networks that implement specific algorithms.
- **Dictionary learning / Sparse Autoencoders**: Techniques to find more monosemantic features.
- **Steering vectors**: Using identified features to control model behavior.

---

## Current status

Interpretability is one of the most active research areas in AI Safety.  
Significant progress has been made since 2022–2023, but the field is still far from being able to fully audit advanced models for dangerous internal goals or deception.
