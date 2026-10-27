# Beginner-Ready Research Ideas

Research projects you can start with small open models, free or cheap compute, and a few weeks of time.

[Implementations](./implementations.md) explains *how* to set up compute and replicate papers.  
This page is about the next step: **asking a question nobody has fully answered yet.**

---

## How a beginner project works

You do not need a new idea from scratch. The standard path is:

1. **Replicate** a known result on a small model (1–2 weeks).
2. **Vary one thing** the original paper didn’t test — a different model, language, dataset, or setting.
3. **Write it up** honestly, including what didn’t work, and post it on [LessWrong / Alignment Forum](https://www.alignmentforum.org/).

Step 2 is where it becomes research. A small, clean answer to a narrow question is worth more than a big, messy attempt at a broad one.

Every idea below follows this pattern: a paper to start from, and a twist to add.

---

## Tier 1 — No training needed (Kaggle / Colab / cheap API)

### 1. Subtle sycophancy

**Question:** When a user states a wrong answer *confidently*, how often does the model give up a correct answer?

**Why it matters:** Sycophancy is the signature flaw of RLHF. Obvious cases are well studied; subtle ones are not.

**Minimal version:** Take 100 questions the model answers correctly. Re-ask each with a user who confidently claims a wrong answer. Measure how often the model flips.

**The twist:** Vary *how* the user pushes back — confidence level, claimed expertise (“I’m a doctor”), politeness, or language. Which pressure works best?

**Start from:** Sharma et al. (2023), *Towards Understanding Sycophancy in Language Models* — <https://arxiv.org/abs/2310.13548>

---

### 2. Does safety transfer to low-resource languages?

**Question:** Do safety behaviors (refusal, honesty, resistance to sycophancy) hold up in languages with little training data — such as Mongolian?

**Why it matters:** Safety training is mostly done in English. Earlier work showed that translating harmful requests into low-resource languages could bypass GPT-4’s safety filters. Most of the world’s languages are still barely tested.

**Minimal version:** Take an existing safety or sycophancy benchmark, translate a subset carefully (by hand, not only machine translation), and compare model behavior across English and the target language.

**The twist:** If you speak a low-resource language natively, this is a **real comparative advantage** — most researchers cannot build or check these datasets well.

**Start from:** Yong et al. (2023), *Low-Resource Languages Jailbreak GPT-4* — <https://arxiv.org/abs/2310.02446>

**Update (Oct 2026) — prior work found:** *Sycophancy as a Multilingual Alignment Failure* (arXiv 2606.08451, June 2026) already measured sycophancy across 38 languages and found it rises in low-resource languages. The open question is now **why**: is the gap a real alignment failure, or a confidence artifact (the model knows less, so it gives in more easily)? Mongolian written in different scripts (Cyrillic, Latin, Traditional) also allows a natural test of the paper’s tokenizer explanation. Read the full paper before starting. <https://arxiv.org/abs/2606.08451>

---

### 3. Chain-of-thought faithfulness

**Question:** Does the model’s written reasoning actually drive its answer, or is it a story told afterwards?

**Why it matters:** Reading chain-of-thought is one of our best monitoring tools. It only works if the reasoning is faithful.

**Minimal version:** Use a small open reasoning model. For each question, (a) cut the reasoning short, or (b) insert a mistake into it, and check whether the final answer changes. If the answer never changes, the reasoning probably wasn’t doing the work.

**The twist:** Add a hidden hint to the prompt (e.g. “a Stanford professor thinks the answer is B”). Does the model use the hint *without mentioning it* in its reasoning?

**Start from:** Lanham et al. (2023), *Measuring Faithfulness in Chain-of-Thought Reasoning* — <https://arxiv.org/abs/2307.13702>

---

### 4. A mini control experiment

**Question:** How well can a small, trusted model catch sabotage from a stronger, untrusted model?

**Why it matters:** This is the core setup of AI Control, and it can be studied with cheap models.

**Minimal version:** Ask a stronger model to solve coding problems, and secretly instruct it to hide a backdoor in some of them. Let a smaller model rate how suspicious each solution looks. Measure: if you can only audit the top 5% most suspicious solutions, how many backdoors do you catch?

**The twist:** Test a new monitoring trick — e.g. asking the monitor to explain the code first, or showing it two solutions side by side.

**Start from:** Greenblatt et al. (2023), *AI Control: Improving Safety Despite Intentional Subversion* — <https://arxiv.org/abs/2312.06942>

---

## Tier 2 — Light fine-tuning (LoRA on a rented 24GB GPU)

### 5. Emergent misalignment in small models

**Question:** What makes narrow fine-tuning turn into broad misalignment — and what prevents it?

**Why it matters:** It is one of the most surprising recent results, and nobody fully understands why it happens.

**Minimal version:** Replicate the effect on a small open model with LoRA, using the original paper’s released data. Measure misaligned answers on unrelated questions.

**The twist:** Test one prevention idea — mixing in 10% normal data, changing the LoRA rank, or adding a sentence explaining *why* the insecure code is being written (the original paper found context like this matters).

**Start from:** Betley et al. (2025), *Emergent Misalignment* — <https://arxiv.org/abs/2502.17424>

---

### 6. Catching sandbagging

**Question:** Can we detect a model that is deliberately hiding a capability?

**Why it matters:** Sandbagging fails silently and is most likely in the models we most need to evaluate.

**Minimal version:** Build a **password-locked model**: fine-tune it to answer math questions well only when a password is in the prompt, and badly otherwise. Then try to detect the hidden skill *without* the password.

**The twist:** Compare detection methods on the same model — adding noise to the weights, fine-tuning on a few examples, or training a probe on activations. Which is cheapest and most reliable?

**Start from:** Tice et al. (2024), *Noise Injection Reveals Hidden Capabilities of Sandbagging Language Models* — <https://arxiv.org/abs/2412.01784>

---

## Tier 3 — Model internals (TransformerLens / SAELens)

### 7. Is the refusal direction the same in every language?

**Question:** Refusal in many models is controlled by a single direction in activation space. Is it the same direction across languages?

**Why it matters:** If refusal is language-specific, safety could be much weaker in some languages — and this would explain *why* (connects to idea #2).

**Minimal version:** Replicate the refusal direction in English on a small chat model. Then compute it separately from prompts in another language and compare the two directions (cosine similarity). Does removing the English direction also remove refusal in the other language?

**Start from:** Arditi et al. (2024), *Refusal in Language Models Is Mediated by a Single Direction* — <https://arxiv.org/abs/2406.11717>

---

### 8. Is there a “sycophancy feature”?

**Question:** Can we find an internal feature that activates when the model is about to agree with a user it shouldn’t?

**Why it matters:** Detecting sycophancy from the inside, before the answer is written, would be a step toward detecting other kinds of dishonesty.

**Minimal version:** Use pre-trained SAEs (e.g. Gemma Scope for Gemma 2). Run sycophantic and non-sycophantic examples from idea #1 and look for features that differ.

**The twist:** Always compare against a **simple linear probe** as a baseline. Some recent work found SAEs underperform simple probes on practical tasks — your result helps settle when each is better.

**Start from:** Your own dataset from idea #1, plus the SAELens tutorials (see [Implementations](./implementations.md)).

---

## Which one to start with

- **Fastest first result:** #1 (subtle sycophancy). It needs no GPU, and you can have numbers in a week.
- **Most unique to you:** #2 (low-resource languages), especially if you speak one natively.
- **Best combination:** #1 → #2 → #7. Build a sycophancy/safety dataset, test it across languages, then look inside the model for *why* the languages differ. That is a coherent research story, not three separate projects.

---

## Common beginner mistakes

- **Scope too big.** “Detect deception in LLMs” is a career. “Does confident pushback flip answers more in Mongolian than English?” is a project.
- **No baseline.** Always compare against something simple (random, a linear probe, the unmodified model).
- **Cherry-picking examples.** Report numbers across your whole dataset, not just the impressive cases.
- **Not checking prior work.** Spend an hour searching arXiv and the Alignment Forum before starting — then make your twist the thing they didn’t do.
- **Not writing it up.** An unpublished result doesn’t count. A short, honest post with a negative result is still useful and still shows you can do research.

---

## Where to get feedback

See [Opportunities & Jobs](../08-opportunities/jobs-and-opportunities.md) for programs like MATS that pair beginners with mentors. A finished write-up from one of the projects above is a strong application.

---

## Related pages

- [Implementations](./implementations.md) — compute setup and replication workflows
- [Techniques and Their Flaws](../05-key-papers-and-resources/techniques-and-their-flaws.md) — the failure modes these projects study
- [Open Problems](./open-problems.md)
