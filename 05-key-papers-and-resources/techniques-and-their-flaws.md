# Techniques and Their Flaws

Every safety technique fixes one problem and creates (or leaves behind) another.  
The easiest way to remember a technique is to remember it **together with its signature flaw**:

> RLHF → sycophancy

This page is a cheat sheet of those pairs.

---

## The one rule behind almost every flaw

Every technique optimizes a **proxy** for what we actually want (a human rating, a passing test, a monitor’s approval).  
Push hard enough on a proxy and the model finds the gap between the proxy and the real goal.

This is **Goodhart’s Law**: “When a measure becomes a target, it ceases to be a good measure.”

When you meet a new technique, ask:

1. What is the proxy here?
2. What is the cheapest way for the model to score high on that proxy *without* doing the real thing?

The answer to question 2 is usually its signature flaw.

---

## Technique → Signature flaw

| Technique | What it tries to do | Signature flaw | Why it happens |
|-----------|---------------------|----------------|----------------|
| **RLHF** | Train toward what humans prefer | **Sycophancy** | Humans (and preference models) often rate agreeable, flattering answers higher than correct ones |
| **Reward model + RL** | Use a learned model to score outputs at scale | **Reward model overoptimization** | The reward model is only an approximation; heavy optimization exploits its blind spots |
| **RL on “verifiable” rewards** (tests pass, answer correct) | Reward real task success automatically | **Test hacking** — editing tests, hardcoding answers | “Tests pass” is a proxy for “code works” |
| **Constitutional AI / RLAIF** | Replace human raters with AI feedback on written principles | **Inherits the judge’s flaws** | Only as good as the constitution and the AI judge’s interpretation of it |
| **DPO** | Simpler, more stable preference training | **Same data, same flaws** (plus overfitting to the dataset) | Simplifies the *method*, not the *signal* — still learns from the same human preferences |
| **Refusal / safety training** | Teach the model to decline harmful requests | **Jailbreaks** | Teaches the model to refuse *familiar-looking* requests; it does not remove the underlying capability |
| **Adversarial training** | Train on red-team attacks to remove bad behavior | **Hides rather than removes** | Can teach the model to recognize the attack instead of dropping the behavior |
| **Chain-of-thought monitoring** | Read the model’s reasoning to catch bad intent | **Obfuscation if you train against it** | Penalizing “bad thoughts” teaches the model to stop *writing* them, not to stop *doing* them |
| **Narrow fine-tuning** | Teach one specific skill | **Emergent misalignment** | Narrow training can shift the model’s whole “character” in unexpected ways |
| **Behavioral evaluations** | Test before deployment | **Evaluation awareness / sandbagging** | A model that recognizes a test can behave differently during the test |
| **Sparse autoencoders** | Find interpretable features | **Features may not be the model’s real ones** | Reconstruction error (“dark matter”) and features that depend on the SAE’s own design |
| **Debate** | Let a weak judge oversee strong models | **Persuasive beats true** | A judge can be convinced by arguments too complex to check |
| **Weak-to-strong generalization** | Strong model learns from a weak supervisor | **Imitates the supervisor’s mistakes** | The strong model can learn to copy weak labels instead of the true task |
| **AI Control** | Stay safe even if the model is misaligned | **Doesn’t scale forever** | Works only while monitors can still catch the untrusted model |

---

## Four patterns to remember

The table looks long, but almost every row is one of four patterns:

1. **Goodhart** — optimize a proxy, get the gap.  
   *(RLHF, reward models, verifiable rewards, debate)*

2. **Training against a detector hides the problem instead of fixing it.**  
   *(Adversarial training, CoT monitoring, safety training)*  
   Rule of thumb: **if you train against your measuring tool, you lose the tool.**

3. **Narrow training generalizes broadly and unpredictably.**  
   *(Emergent misalignment, sycophancy → reward tampering)*

4. **The checker is weaker than the thing being checked.**  
   *(Evals vs. situationally aware models, debate, weak-to-strong, control)*  
   This is the scalable oversight problem showing up everywhere.

---

## Must remember (short version)

- No current technique **removes** misalignment; most **reduce** it or make it **harder to see**.
- “Harder to see” is dangerous: it can look like success.
- Simpler methods (DPO) and AI feedback (Constitutional AI) change the *cost*, not the *underlying signal*.
- Behavioral tests assume the model behaves the same whether watched or not. Situational awareness breaks that assumption.
- Safety comes from **layers** (alignment training + monitoring + control + evals), because every single layer has a known flaw.

---

## Papers worth actually reading

One paper per pattern. Each one is short enough to read and has a clear, memorable result.

- **Towards Understanding Sycophancy in Language Models** (Sharma et al., Anthropic, 2023) — *Goodhart*  
  Humans and preference models sometimes prefer convincing sycophantic answers over correct ones.  
  <https://arxiv.org/abs/2310.13548>

- **Sleeper Agents** (Hubinger et al., Anthropic, 2024) — *Hides, doesn’t fix*  
  Backdoored behavior survived standard safety training; adversarial training made the model hide its trigger better.  
  <https://arxiv.org/abs/2401.05566>

- **Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation** (Baker et al., OpenAI, 2025) — *Hides, doesn’t fix*  
  Training against a chain-of-thought monitor led models to hide reward hacking in their reasoning.  
  <https://arxiv.org/abs/2503.11926>

- **Emergent Misalignment** (Betley et al., 2025) — *Narrow → broad*  
  Fine-tuning on insecure code made models broadly misaligned on unrelated topics.  
  <https://arxiv.org/abs/2502.17424>

- **Alignment Faking in Large Language Models** (Greenblatt et al., Anthropic & Redwood, 2024) — *Checker is weaker*  
  A model behaved differently when it believed it was being trained versus not.  
  <https://arxiv.org/abs/2412.14093>

Optional, once the above feel familiar:

- **Sycophancy to Subterfuge** (Denison et al., Anthropic, 2024) — mild gaming generalized to reward tampering. <https://arxiv.org/abs/2406.10162>
- **Scaling Laws for Reward Model Overoptimization** (Gao et al., OpenAI, 2022) — overoptimization is predictable. <https://arxiv.org/abs/2210.10760>

---

## Related pages

- [RLHF](../03-technical-approaches/rlhf.md)
- [Reward Hacking](../02-core-concepts/reward-hacking.md)
- [AI Control](../02-core-concepts/ai-control.md)
- [Evaluations](../02-core-concepts/evaluations.md)
