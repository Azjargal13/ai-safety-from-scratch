# AISafetyLab: A Comprehensive Framework for AI Safety Evaluation and Improvement

It is a paper published by researchers at **Tsinghua University (CoAI Group)** and **Beihang University**.

It addresses one of the biggest headaches in AI safety engineering: **fragmentation**.

Historically, when researchers invented a new jailbreak attack (like GCG or AutoDAN) or a defense (like SmoothLLM or guardrail filters), they published their own messy, standalone GitHub repository. This made apples-to-apples comparisons of attacks and defenses notoriously difficult. **AISafetyLab** solves this by providing a single, standardized, open-source library that unifies **Attacks**, **Defenses**, and **Evaluations** under one clean Python API.

---

### The Three Core Pillars of AISafetyLab

The authors structured the framework into three modular components:

```
                     ┌───────────────────────┐
                     │     AISafetyLab       │
                     └──────────┬────────────┘
         ┌──────────────────────┼──────────────────────┐
         ▼                      ▼                      ▼
  [ Attack Module ]     [ Defense Module ]    [ Evaluation Module ]
  • White-Box           • Inference-Time       • Automated Scorers
  • Gray-Box            • Training-Time        • Safety Benchmarks
  • Black-Box           
```

#### 1. The Attack Module (13+ Jailbreak Methods)

The framework standardizes how adversarial prompts are constructed across three access levels:

* **White-box Attacks:** When you have full gradient and parameter access (e.g., GCG / Greedy Coordinate Gradient).
* **Gray-box Attacks:** When you have token probability/logit access but cannot calculate backward gradients.
* **Black-box Attacks:** When you only have text-in, text-out access (e.g., AutoDAN, PAIR, prompt mutations).
* *Engineering design:* All attacks are broken down into a standard pipeline: **Initialization $\to$ Mutation $\to$ Selection $\to$ Feedback**.

#### 2. The Defense Module (16+ Defense Mechanisms)

The authors implemented defenses categorized by where they sit in the lifecycle:

* **Inference-Time Defenses:** Defenses applied dynamically without retraining the model weights:
  * *Input Modification:* Pre-processing or perplexity filtering to detect adversarial patterns before they hit the model.
  * *Decoding Guidance:* Modifying the model's logits during token generation to steer away from toxic completions.
  * *Output Guardrails:* Classifiers screening the output text before the user sees it.
* **Training-Time Defenses:** Changing the model weights directly via adversarial safety fine-tuning or machine unlearning.

#### 3. The Evaluation Module (7+ Safety Scorers)

Instead of guessing whether an attack succeeded, the toolkit integrates automated evaluators:

* Evaluator models such as **Llama-Guard-3-8B** acting as an automated safety judge.
* Standardized testing pipelines against benchmarks like **HarmBench**.

---

### Key Takeaways from Their Experiments

The authors ran systematic empirical tests (notably evaluating models like `Vicuna-7B-v1.5` under various attack-defense combinations on HarmBench):

1. **No Single Defense is Bulletproof:** Inference-time input preprocessing catches naive black-box mutations, but struggles against gradient-based white-box attacks.
2. **The "Alignment Tax":** Overly aggressive inference-time defenses often trigger a high false-refusal rate, rejecting harmless benign queries.
3. **Standardized Benchmarking Matters:** By testing attacks and defenses inside the exact same harness, the paper revealed that some defenses claimed to be "robust" in original papers were actually just overfitting to specific prompt styles.

---

### Why This Paper Matters for You

If you want to be a top implementor in AI safety, **this codebase (`thu-coai/AISafetyLab` on GitHub) is a goldmine:**

* **Clean OOP Design:** Instead of writing custom scripts for every attack, it gives you clean base classes (`BaseAttacker`, `BaseDefender`, `BaseEvaluator`).
* **Runs on Budget Hardware:** You can clone this repo onto a Kaggle or RunPod instance, pick an open-source model (like Vicuna or Llama-3-8B), and run a complete attack $\to$ defense $\to$ evaluation pipeline in under 30 lines of Python.
* **Instant Research Surface:** Because it standardizes existing methods, you can easily use it to test a novel hypothesis (for example: *"Does applying an SAE feature steering vector beat standard inference-time defenses against AutoDAN?"*). You just plug your new method into their modular pipeline and benchmark it.
