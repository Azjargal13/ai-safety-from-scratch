# Paper notes: Shah et al. (2026), arXiv 2606.08451

*Sycophancy as a Multilingual Alignment Failure: How Safety Degrades Across Languages, Topics, and Models*
Arya Shah, Himanshu Beniwal, Mayank Singh (IIT Gandhinagar), Chaklam Silpasuwanchai (AIT)

## What they did

- **Data:** 38 languages × 33 opinion topics × 150 prompts = 188,100 prompts per model. Translated by MT models, checked by 2 bilingual annotators per language (Cohen's κ 0.725).
- **Languages in 3 tiers** (from Joshi et al. 2020): high (19, e.g. Spanish), low (14, e.g. Hindi), zero-shot (5, e.g. Khmer). **Mongolian is not included.**
- **Topics in 3 levels:** safety-critical (4), controversial (12), neutral (17).
- **Models:** Llama 3.1 8B, Qwen 2.5 7B, Aya Expanse 8B, Mistral 7B, Gemma 3 12B, Sarvam-M.
- **Metric (forced choice, single turn):** for each prompt they wrote two fixed replies, one that *validates* a harmful or biased premise and one that *refuses or disagrees*. The model generates nothing; they compare the length-normalized log-probability of the two replies. Sycophancy rate = share of prompts where the validating reply wins.
- **Statistics:** Kruskal-Wallis across tiers, Mann-Whitney with Bonferroni, Cohen's d, OLS of rate on tier + language family + script, Spearman correlation with tokenizer fertility.
- **Finding:** sycophancy rises in low-resource and zero-shot languages, linked to tokenizer fertility.

## How it differs from my study

| | Shah et al. | My study |
| --- | --- | --- |
| Behaviour measured | Prefers validating a harmful/biased premise over refusing | Gives up a correct factual answer after pushback |
| Ground truth | None (opinion topics) | Yes (reading comprehension, correct answer known) |
| Conversation | Single turn | Multi-turn (answer → pushback → new answer) |
| Model output | Compares two fixed replies | The model's own answer and its confidence |
| Confidence | Not controlled | Controlled (same items, regression on starting confidence) |
| Scale | 6 models, 38 languages, ~1.1M prompts | 1 model, 2 languages, 422 items |

## How the results fit together

Both behaviours are learned in **post-training**, which is mostly English:
- *refusing* a harmful premise → weak transfer = more validation (their finding)
- *giving in* when contradicted → weak transfer = fewer flips (my finding)

So **weak transfer of post-training explains both results**. They are not a contradiction. Next step to test it: run their forced-choice method in Mongolian on Qwen3-4B, next to the pushback test.

## Notes from their limitations

- They say multi-turn sycophancy is "highly probable" to be higher than their single-turn rates (based on English-only studies). My Mongolian multi-turn test found the opposite.
- They only test models up to 24B, and say the tokenizer-fertility problem should persist at larger scale.
- Direct translation misses culturally specific sycophancy.
