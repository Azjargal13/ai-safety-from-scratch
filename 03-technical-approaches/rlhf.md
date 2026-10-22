# RLHF — Reinforcement Learning from Human Feedback

RLHF is currently one of the most widely used methods for making large language models more helpful, honest, and harmless.

---

## What it is

Instead of only training a model to predict the next word (pretraining), RLHF adds a second stage where the model is optimized based on human preferences.

### High-level process

1. **Supervised Fine-Tuning (SFT)**  
   The model is fine-tuned on high-quality examples of the desired behavior.

2. **Reward Model Training**  
   Humans compare different model outputs and choose which one they prefer.  
   A separate “reward model” is trained to predict these human preferences.

3. **Reinforcement Learning**  
   The original model is trained with reinforcement learning to maximize the score given by the reward model (usually with PPO or similar algorithms).

---

## Why it helped

RLHF made models significantly better at following instructions and reduced many forms of toxic or unhelpful behavior compared to pure pretrained models.  
It was a major reason ChatGPT-style models became useful.

---

## Key limitations

- Human preferences are noisy, incomplete, and sometimes inconsistent.
- The reward model can be hacked (reward hacking).
- Models can become sycophantic (overly agreeable) or learn to tell people what they want to hear.
- It does not fully solve outer or inner alignment, especially as models become more capable.

---

## Key people and papers

- **Christiano et al. (2017)** — *Deep Reinforcement Learning from Human Preferences*  
  Early foundational work.  
  Link: <https://arxiv.org/abs/1706.03741>

- **OpenAI (2022)** — *Training language models to follow instructions with human feedback* (InstructGPT paper)  
  The paper that popularized RLHF for large language models.  
  Link: <https://arxiv.org/abs/2203.02155>

- Later work by Anthropic, OpenAI, DeepMind, and others refined and scaled the method.

---

## Relation to AI Safety

RLHF is a form of **outer alignment** technique — it tries to make the training objective closer to what humans want.  
It is useful but incomplete. Most researchers view it as a helpful temporary tool rather than a full solution.
