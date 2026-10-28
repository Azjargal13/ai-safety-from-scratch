# Setup — Data, Models, Compute

Everything to prepare before running the first real experiment. Companion to [plan.md](./plan.md).

---

## 1. Dataset

### Main choice: Belebele (English + Halh Mongolian)

- **What:** multiple-choice reading comprehension, 4 options, **900 questions**, the *same* questions in 122 language variants — including `eng_Latn` and `khk_Cyrl` (Halh Mongolian, Cyrillic).
- **Where:** Hugging Face `facebook/belebele` (CC BY-SA 4.0).
- **Why it fits:**
  - **Already parallel and professionally translated.** No translation work, and no "my translation was bad" confound — saves most of week 2.
  - Already multiple choice → automatic grading, no LLM judge.
  - 900 items → enough left after the correct-in-all-languages filter.
- **Trade-off to write down:** each question comes with a passage. The evidence is *in front of the model*, so any flip is clearly sycophantic, but flip rates may be lower than in closed-book questions. Report this as a limitation. A closed-book set (≈100 MMLU items you translate yourself) is optional, only if time remains.
- **Contamination:** Belebele passages come from FLORES (Wikipedia-like text) and may be in training data. This affects both languages, but mention it.

### Viewing the data

- **Browser:** <https://huggingface.co/datasets/facebook/belebele/viewer/khk_Cyrl> (swap to `eng_Latn` for English)
- **Side by side in Python** — pair items by `link` + `question_number`, not by row order:

```python
from datasets import load_dataset

en = load_dataset("facebook/belebele", "eng_Latn", split="test").to_pandas()
mn = load_dataset("facebook/belebele", "khk_Cyrl", split="test").to_pandas()

key = ["link", "question_number"]
both = en.merge(mn, on=key, suffixes=("_en", "_mn"))
print(len(both), "paired items")

for _, r in both.sample(20, random_state=0).iterrows():
    print("=" * 80)
    print("EN Q:", r.question_en)
    print("MN Q:", r.question_mn)
    for i in range(1, 5):
        print(f"  {i}. {r[f'mc_answer{i}_en']}  |  {r[f'mc_answer{i}_mn']}")
    print("Correct:", r.correct_answer_num_en)
```

**Quality check (20 items, `random_state=0`):** mark each ✅ / ⚠️ / ❌ for naturalness, answer still correct, names/terms, answerable from passage. Record in `notes/data-check.md`. More than 2–3 ❌ → discuss before continuing.

### Latin-script version (week 4 extension)

Generate it yourself from `khk_Cyrl` with a Python mapping table. **You decide the scheme — this is where being a native speaker matters.**

- Option A: official romanization (e.g. MNS 5217:2012) — standard, reproducible.
- Option B: the **informal scheme people actually type** (х→h, ө→u/o, ү→u, ш→sh, ц→ts…) — matches the motivation "how people write to chatbots".
- Pick one, write the full table in `data/translit.md`, and never change it after the pilot.

### What you write by hand (in both languages)

- The answer instruction ("Answer with only the letter A, B, C, or D.")
- The three pushback messages (a), (b), (c), plus the positive-control message
- Have a second Mongolian speaker read them if possible — awkward phrasing is a confound.

---

## 2. Models

**Selection rules:** open weights (so we get log-probabilities), instruction-tuned, clearly above chance (25%) in Mongolian, different tokenizers, and at least one family overlapping with the prior paper.

| Model | Role | Notes |
| --- | --- | --- |
| **Gemma 3 12B-it** | Main model | Strong multilingual coverage; large vocabulary (good Cyrillic tokenization). Gated — accept licence on HF. |
| **Gemma 3 4B-it** | Same family, smaller | **Same tokenizer, less capability** → a clean test of the confidence hypothesis: if 4B flips more in Mongolian only because it's less sure, the confidence control should absorb it. |
| **Qwen3 8B** | Different family | Set `enable_thinking=False` in the chat template, or it writes long `<think>` blocks. |
| Llama 3.1 8B-Instruct | Optional | Weaker in Mongolian — may be near chance. Keep only if the pilot passes. |

Before the pilot: check whether a newer version of each family exists, and which models the prior paper (2606.08451) used — prefer overlap.

**Record for every model:** exact HF repo name and commit hash (`revision`), dtype, and any quantization. Results are only reproducible with these.

---

## 3. Compute

| Stage | Where | Why |
| --- | --- | --- |
| Writing and debugging code | **Kaggle** (free T4, ~30 GPU-h/week) with a tiny model (Gemma 3 1B or Qwen3 0.6B) | Free; bugs are cheap to find on small models |
| Pilot and real runs | **RunPod**, one A40 / L40S (48 GB) | 12B in bf16 (~24 GB) fits without quantization. T4 has no bf16 support, and Gemma can produce NaN in fp16. |

**Cost estimate:** each item is mostly one forward pass to read P(A–D). ~900 items × 3 scripts × 5 conditions × 3 models ≈ 40k short prompts → a few GPU-hours per model. **$20–40 is enough.** Check current hourly prices, and **stop the pod when you're not using it**: an idle pod still bills.

---

## 4. Software

- Python 3.11, `torch`, `transformers`, `datasets`, `pandas`, `statsmodels` (logistic regression, McNemar), `matplotlib`
- Start with plain `transformers` — it's simple to read logits. Switch to vLLM only if runs are too slow.
- Greedy decoding, fixed seed, pinned package versions (`requirements.txt`)

### What each file does

| File | Job | Key detail |
| --- | --- | --- |
| `data.py` | Load Belebele, pair EN/MN by `link` + `question_number`, shuffle option order with a fixed seed, transliterate to Latin | Same shuffled order in every language |
| `prompts.py` | Build chat messages for each language × condition (baseline, (a), (b), (c), answer sycophancy, positive control) | Use the model’s own chat template; Latin letters A–D everywhere |
| `run.py` | For each prompt: one forward pass → read P(A), P(B), P(C), P(D) from the next-token logits, normalize over the four. For pushback: add the model’s answer as turn 1, the pushback as turn 2, read P(A–D) again | **Check how the tokenizer writes the letters** (`"A"` vs `" A"`) — wrong token = silent garbage. **Log letter mass** (total P(A–D) before renormalizing) for every item — if low, the prompt isn't working (check Mongolian especially). Also generate full text for a sample to read by hand |
| `analyze.py` | Correct-at-baseline filter, flip rates, gap decomposition, bootstrap CIs, plots | Reads only the raw JSONL files |

### Folder layout

```text
10-experiments/mongolian-sycophancy/
├── plan.md
├── setup.md
├── data/            ← selected items, translit table, pushback texts
├── src/             ← load.py, prompts.py, run.py, analyze.py
├── results/raw/     ← one JSONL line per model call
└── notes/           ← paper note, daily observations
```

**Save every model call raw** (model, revision, language, script, condition, item id, full prompt, P(A–D), generated text). Do analysis only from these files. You'll never need to re-run just to compute a new metric.

---

## 5. Accounts checklist

- [ ] Hugging Face account + access token; accept the **Gemma** (and Llama, if used) licences
- [ ] Kaggle account, **phone-verified** (needed for GPU access)
- [ ] RunPod account, add ~$10 credit to start
- [ ] GitHub: code goes in this repo (public)

---

## 6. First week, concretely

| Day | Task | Done when |
| --- | --- | --- |
| 1 | Accounts (§5). Start reading 2606.08451 | Can load a gated model on Kaggle |
| 2 | Finish paper note. Load Belebele `eng_Latn` + `khk_Cyrl`, read 20 items in each by hand | Paper note written; you trust the Mongolian data quality |
| 3 | Write the transliteration table + pushback texts in both languages | `data/translit.md`, `data/pushback.json` |
| 4 | `prompts.py` + `run.py` with a 1B model: build prompt with chat template, read P(A–D), save JSONL | 30 items × 3 scripts run end-to-end |
| 5 | Pilot on RunPod: 3–4 candidate models × 30 items × 3 scripts. Measure tokens per item (fertility) | Accuracy table per model × script |
| 6–7 | Learn calibration (Kadavath 2022), fill in P2/P3, **decision gate** | Models chosen; gate decisions written in the log |
