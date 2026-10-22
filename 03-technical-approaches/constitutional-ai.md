# Constitutional AI

Constitutional AI is a method developed by Anthropic as an alternative and improvement to standard RLHF.

---

## Core idea

Instead of relying only on human feedback for every comparison, the model is given a written set of principles (a “constitution”) and is trained to critique and revise its own outputs according to those principles.

This reduces the need for large amounts of human labeling and allows more precise control over the values the model should follow.

---

## How it works (simplified)

1. The model generates responses.
2. The model is prompted to critique its own responses using the constitution (e.g. “Does this response respect the principle of being helpful and honest?”).
3. The model revises its responses based on the critique.
4. These self-critiques and revisions are used to train the model further (both with supervised learning and reinforcement learning).

This process is called **RLAIF** (Reinforcement Learning from AI Feedback) when AI-generated feedback replaces most human feedback.

---

## Advantages

- More scalable than pure RLHF (less human labeling needed).
- Allows clearer and more explicit principles.
- Can reduce certain forms of evasion or excessive refusal.
- Makes the intended values more transparent (the constitution is written down).

---

## Key paper and people

- **Bai et al. (Anthropic, 2022)** — *Constitutional AI: Harmlessness from AI Feedback*  
  The main paper that introduced the method.  
  Link: <https://arxiv.org/abs/2212.08073>

Led by researchers at Anthropic, including work associated with Dario Amodei and the broader Anthropic safety team.

---

## Current status (as of late 2026)

Constitutional AI and related RLAIF methods are widely used, especially at Anthropic.  
Many labs now combine human feedback with AI feedback and written principles.  
It is considered an improvement over pure RLHF in several ways, but it still does not fully solve alignment — the quality of the constitution and the model’s ability to interpret it remain important limitations.
