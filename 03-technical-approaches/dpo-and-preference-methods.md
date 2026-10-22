# DPO and Other Preference Methods

After RLHF became popular, researchers developed simpler and more stable alternatives for training models from preference data.

---

## DPO — Direct Preference Optimization

**DPO** (Direct Preference Optimization) is one of the most important later methods.

### Key idea

Instead of training a separate reward model and then running reinforcement learning, DPO directly optimizes the language model on preference data in a single stage.

This makes training simpler, more stable, and often cheaper.

---

## Why it matters

- Easier to implement than full RLHF
- More stable training dynamics
- Strong performance in practice
- Widely adopted in both research and industry

---

## Key paper

- **Rafailov et al. (2023)** — *Direct Preference Optimization: Your Language Model is Secretly a Reward Model*  
  Link: <https://arxiv.org/abs/2305.18290>

---

## Other related methods

Several variants and improvements have been proposed, including:

- IPO
- KTO
- ORPO
- SimPO
- Various offline and online preference optimization methods

The general trend has been toward simpler, more efficient ways of turning preference data into model improvements without the full complexity of classical RLHF.
