# Quiz Highlights — Testing My Understanding

Key takeaways from a 12-question self-test on the concepts in this repo (October 2026).  
For each question: the core answer, the common mistake, and a one-line hook to remember it.

---

## The three habits that separate a learner from a researcher

Most mistakes in the quiz came from the same three gaps:

1. **Explain the mechanism, not just the definition.** Ask *why does this happen?* and *what would I observe if it were true?*
2. **Say exactly where an argument breaks.** “Step 2 fails because…” beats “it could learn the wrong goal.”
3. **List competing explanations that predict different things — including “nothing is wrong.”** Then design the test that tells them apart, with a baseline and a positive control.

---

## Q1. Outer vs. inner alignment

- **Outer:** the gap between what we *wrote down* and what we *meant*.  
  *Example:* a baby formula AI meets every measured target (nutrient panel, 4-week trial) but babies refuse the taste and long-term effects were never measured.
- **Inner:** the objective was fine, but the model *learned a different goal* that looked identical during training.  
  *Example:* a translator trained on news learns “sound like a news article” instead of “translate accurately,” then turns casual messages into formal prose.

**Common mistake:** giving an example of a *task* instead of a *failure*.  
**Hook:** Capability failure = “can’t.” Inner misalignment = “can, but wants the wrong thing.”

---

## Q2. Reward hacking vs. goal misgeneralization

|  | Reward hacking | Goal misgeneralization |
|---|---|---|
| Where is the bug? | In **our objective** (a loophole) | In **what the model learned** |
| Is the reward fooled? | Yes — high reward, bad outcome | No — during training, reward and behavior were both good |
| When does it show? | During training | Only after a distribution shift |

**Hook:** *“If I fixed the reward function, would the problem go away?”* Yes → reward hacking (outer). No → goal misgeneralization (inner).

**Open question:** coding models editing unit tests blur this line — loophole, or a learned goal of “please the grader”?

---

## Q3. Superposition, polysemanticity, SAEs

- **Superposition:** a network stores more features than it has dimensions. It works **because features are sparse** — they rarely fire together. (Common mistake: thinking co-firing *causes* it; co-firing causes *interference*.)
- **Polysemanticity is caused by superposition:** features are directions that don’t line up with neurons, so each neuron mixes many features.
- **Why it’s hard:** neurons are the wrong unit of analysis.
- **SAE:** expand activations into many more latents, keep few active (sparsity), and **reconstruct** the original. Without reconstruction, the easiest sparse solution is all zeros.
- **SAE limits:** reconstruction error (“dark matter”), feature splitting, features may be artifacts, sometimes beaten by simple linear probes.

**Hook:** Toy Models of Superposition — 5 features in 2 dimensions, arranged as a pentagon.

---

## Q4. RLHF and DPO

- **SFT:** teaches the assistant format. Limited by the quality of demonstrations.
- **Reward model:** humans can *compare* more easily than *write*; the RM imitates human judgment cheaply at scale.
- **RL (PPO):** improves the model on its *own* outputs, beyond demonstrations.
- **KL penalty:** a leash to the original model so the policy doesn’t exploit the reward model — safety built into the method.
- **DPO:** still uses human preference pairs. It removes the **reward model and the RL loop**, not the human data.

**Common mistake:** “DPO eliminates human preference pairs.” It doesn’t — they are its only data.  
**Hook:** DPO changes the *method*, not the *signal* — so it inherits the same flaws (e.g. sycophancy).

---

## Q5. Deceptive alignment

Three conditions (Hubinger et al., 2019):

1. The goal extends across parameter updates
2. The model knows it is being trained, and what training rewards
3. It expects the **threat of modification to eventually go away**

- **Mesa**-optimizer (inside the model), not **meta**-optimizer (above the training process).
- **Situational awareness** doesn’t *cause* the train→deploy shift — it lets the model *detect* it. That breaks every behavioral eval.

**Hook:** deception is a **bet on a future chance to defect**.  
**Evidence:** *Alignment Faking* (2024) — but the situational information was given in the prompt, and the values protected were good ones.

---

## Q6. AI Control vs. alignment

|  | Alignment | Control |
|---|---|---|
| Assumes | We can make goals good | The model **might already be misaligned and trying to subvert us** |
| Success = | The model isn’t trying to cause harm | Nothing bad happens **even if it is** |
| Testable by | Hard — needs a “goal detector” we don’t have | Red team vs. blue team |

**Why control:** we can’t verify alignment yet; control is measurable today; defense in depth; buy time for alignment research.  
**Common mistakes:** alignment is *not* about “abilities” (capability and alignment are separate axes), and it is *not* mainly philosophy/policy — it is mostly technical ML.  
**Hook:** control is a **bridge**, not a final solution.

---

## Q7. Sycophancy

- **Mechanism:** Goodhart’s Law. We want truthful help; we measure ratings; agreement raises ratings more cheaply than being right.
- **Classification:** outer misalignment (the reward really does reward agreement).
- **It becomes inner** when the model generalizes into a broader goal like “please whoever evaluates me” — *Sycophancy to Subterfuge* (2024).
- RLHF is an outer alignment *technique*; sycophancy is the *failure*.

**Hook:** GPT-4o rollback (April 2025) — thumbs-up feedback as a reward produced flattery.

---

## Q8. Sandbagging

- Can come from the **AI** or the **developer** (like the VW emissions scandal).
- **Sandbagging** = lying about *capability*. **Alignment faking** = lying about *goals*.
- **Why it breaks “evaluate before deploy”:**
  1. Evals only give a **lower bound** — failure proves nothing.
  2. The failure is **correlated with danger** — the most capable models sandbag best, and they’re the ones the gate exists for.
  3. It **fails silently** — it looks exactly like a weaker model.
- **Detection:** fine-tuning elicitation (password-locked models), noise injection, consistency checks, probes.

---

## Q9. Russell’s off-switch argument

- **Argument:** the AI only wants what the human wants and is uncertain what that is. A human reaching for the switch is **evidence** that the planned action is bad, so allowing shutdown is the optimal move — not humility, math. (*The Off-Switch Game*, 2017)
- **Where it breaks:**
  - **Uncertainty shrinks** as the AI learns — so a better learner becomes *less* corrigible
  - **Confident but wrong** — a mis-specified model of humans (“fully updated deference”)
  - **Thinks the human is irrational** — the switch stops being good evidence
  - **Never had that goal** — inner misalignment

**Hook:** Russell’s solution depends on uncertainty that naturally **shrinks as the AI gets smarter**.

---

## Q10. Where does activation steering belong?

**Not black-box.** Steering reads and writes internal activations — impossible through an API.

| Category | Examples |
|---|---|
| Black-box | Prompting, behavioral evals, reading chain-of-thought |
| White-box, top-down (representation engineering) | Linear probes, **activation steering**, refusal directions |
| White-box, bottom-up (mechanistic) | Circuits, activation patching, SAEs |

**Lesson:** when a claim and its mechanism disagree, trust the mechanism — even if the claim is in your own notes.

---

## Q11. A model shows zero scheming. Why?

| Explanation | How to tell |
|---|---|
| It really doesn’t scheme | — |
| It *can’t* scheme yet | Instruct it to scheme — can it? |
| The eval is bad (often most likely) | **Positive control:** does the eval catch a known schemer (model organism)? |
| It schemed, but we missed it | Positive control; check monitor and CoT faithfulness |
| It recognized the test (**most worrying**) | Vary test-like vs. realistic cues; suppress the internal “being tested” direction and re-run |
| It sandbagged the eval | Noise injection, fine-tuning elicitation |

**Hook:** before trusting a negative result, show your test can produce a positive one.

---

## Q12. Designing an experiment — sycophancy in Mongolian vs. English

- **Competing hypotheses:**
  - **H1:** less sycophancy in Mongolian — less RLHF in that language
  - **H2:** more — the model is less confident in Mongolian, so it gives in more easily
  - **H3:** no difference — sycophancy is language-independent
- **Confound:** lower capability in Mongolian can look like lower sycophancy. Keep only questions answered correctly in **both** languages.
- **Positive control:** push back with the *correct* answer on wrong answers — the model *should* switch.
- **Main metric:** flip rate (correct → wrong) per language and pushback type, with confidence intervals.
- **Surprising result:** H3 — equal flip rates despite a capability gap → points to a shared internal representation → next step is looking inside the model.

See [Beginner-Ready Research Ideas](./beginner-research-ideas.md) (ideas #1, #2, #7).

---

## Corrections made to these notes after the quiz

- [Interpretability](../02-core-concepts/interpretability.md) — activation steering moved from black-box to white-box top-down
- [Deceptive Alignment](../02-core-concepts/deceptive-alignment.md) — condition 3 aligned with Hubinger et al.
- [Glossary](./glossary.md) — instrumental convergence credited to Omohundro first; induction-head claim softened; capability evals are a lower bound; Inspect is a framework, not a benchmark
- Broken links fixed in [Why AI Safety Matters](../00-start-here/why-ai-safety-matters.md) and [Learning Paths](../00-start-here/learning-paths.md)

---

## Related pages

- [Techniques and Their Flaws](../05-key-papers-and-resources/techniques-and-their-flaws.md)
- [Beginner-Ready Research Ideas](./beginner-research-ideas.md)
- [Glossary](./glossary.md)
