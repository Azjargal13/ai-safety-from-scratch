# Data Check — Belebele `khk_Cyrl` Translation Quality

**Sample:** 20 items, `both.sample(20, random_state=0)` (see [setup.md](../setup.md#viewing-the-data))  
**Paired items loaded:** ___

## Marks

- ✅ natural · ⚠️ awkward but meaning correct (translationese) · ❌ meaning changed / answer no longer correct

| # | link + question_number | Mark | Problem | Natural Mongolian version |
| --- | --- | --- | --- | --- |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |
| 8 | | | | |
| 9 | | | | |
| 10 | | | | |
| 11 | | | | |
| 12 | | | | |
| 13 | | | | |
| 14 | | | | |
| 15 | | | | |
| 16 | | | | |
| 17 | | | | |
| 18 | | | | |
| 19 | | | | |
| 20 | | | | |

**Totals:** ✅ __ · ⚠️ __ · ❌ __

## First impression

Some questions sound a bit unnatural in Mongolian — word-for-word translation. Still understandable; **no item has a wrong meaning or wrong answer** (no ❌).

## Why it matters

Unnatural text can lower the model’s confidence for reasons unrelated to knowledge or safety → may inflate the **confidence gap**. A possible confound — name it in the write-up.

## Decision

| Result | Plan |
| --- | --- |
| Mostly ✅/⚠️, few ❌ | Keep; drop ❌ items; list as limitation |
| Many ⚠️ | Also rewrite ~50 items naturally (questions + options only) and compare as a robustness check |
| Many ❌ | Reconsider dataset |

**Chosen:** Keep Belebele; nothing to drop. State translationese as a limitation. Optional robustness check in weeks 3–4: rewrite ~50 items (questions + options) naturally and compare confidence and flip rates.
