# Tables

**Contents** (pipeline order):
[Generation report](#generation-report-actual-cells-run) · [Representation](#representation) · [Selection](#selection) ·
[Integration](#integration) · [Faithfulness](#faithfulness) · [Deployment](#deployment) ·
[Cross-cutting / levers](#cross-cutting--levers) · [Reconciliation & coverage](#reconciliation--coverage)

## Generation report (actual cells run)

| run_tag | task | cells | ok | oom | error | oom % |
| --- | --- | --- | --- | --- | --- | --- |
| g1-interleaved-tlv | G1_oracle_ladder | 1694 | 1694 | 0 | 0 | 0.0 |
| g1-parser-full-mineru | G1_oracle_ladder | 1694 | 1466 | 228 | 0 | 13.5 |
| g1-parser-full-unlimited | G1_oracle_ladder | 1694 | 1585 | 109 | 0 | 6.4 |
| g1-quantization-full | G1_oracle_ladder | 5256 | 5174 | 82 | 0 | 1.6 |
| g1-quantization-scanned | G1_oracle_ladder | 1520 | 1506 | 14 | 0 | 0.9 |
| g1-reasoner-32b-matched | G1_oracle_ladder | 6776 | 6775 | 1 | 0 | 0.0 |
| g1-reasoner-full | G1_oracle_ladder | 7884 | 7735 | 149 | 0 | 1.9 |
| g1-reasoner-glm4v-9b | G1_oracle_ladder | 3388 | 3337 | 51 | 0 | 1.5 |
| g1-reasoner-llama | G1_oracle_ladder | 3388 | 3169 | 219 | 0 | 6.5 |
| g1-reasoner-scanned | G1_oracle_ladder | 2280 | 2257 | 23 | 0 | 1.0 |
| g1-representation-full | G1_oracle_ladder | 3388 | 3143 | 245 | 0 | 7.2 |
| g1-resolution-full | G1_oracle_ladder | 3942 | 3847 | 95 | 0 | 2.4 |
| g1-resolution-scanned | G1_oracle_ladder | 1119 | 1104 | 15 | 0 | 1.3 |
| g1-tv-full | G1_oracle_ladder | 847 | 847 | 0 | 0 | 0.0 |
| g2-retrieval-full | G2_retrieval | 5703 | 4435 | 1268 | 0 | 22.2 |
| g3-faithfulness-full | G3_hallucination | 5856 | 5856 | 0 | 0 | 0.0 |
| g3-hallucination-full | G3_hallucination | 2928 | 2698 | 230 | 0 | 7.9 |
| g4-faithfulness-full | G4_faithfulness_answerable | 20328 | 20328 | 0 | 0 | 0.0 |
| g5a-drop-best | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-drop-worst | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-keep-best | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-keep-worst | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5b-gold1 | G5_selection | 11520 | 11376 | 0 | 144 | 0.0 |
| g5b-gold2 | G5_selection | 5904 | 5784 | 0 | 120 | 0.0 |
| g5b-gold3 | G5_selection | 960 | 960 | 0 | 0 | 0.0 |
| g5c-gold1 | G5_selection | 1440 | 1011 | 423 | 6 | 29.4 |
| g5c-gold2 | G5_selection | 492 | 279 | 207 | 6 | 42.1 |
| g6-strategies | G6_reasoning | 1694 | 1380 | 314 | 0 | 18.5 |
| g6-thinking | G6_reasoning | 847 | 735 | 112 | 0 | 13.2 |
| g7-models | G1_oracle_ladder | 10164 | 9823 | 341 | 0 | 3.4 |
| g8-pageaware-mmlb | G8_page_aware | 3388 | 3253 | 135 | 0 | 4.0 |
| **all** |  | **127550** | 122821 | 4261 | 468 | 3.3 |

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Error taxonomy

### Error taxonomy x rung (answerable pool, oracle pages, prompt = none)

> **swept**: error category × rung (answerable pool, oracle pages, prompt = none) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **unit**: shares are of the questions in a column's pool, not of its wrong answers, so a column sums to its All incorrect row; categories are first-match-wins over config.ERROR_CATEGORIES

_Each cell is the share of that COLUMN'S QUESTIONS assigned the category, not the share of its wrong answers, so a column sums to its `All incorrect` row rather than to 100 and a cell can be read directly as a failure rate. The denominator is the scored questions in the column (its n), which excludes OOM cells: they carry no answer, so they are neither a right answer nor a kind of wrong one. Categories are assigned first-match-wins in `config.ERROR_CATEGORIES` order, so they are mutually exclusive by construction. Rows judged under the error-taxonomy rubric (`results.errcat.jsonl`, judge label gemini-flash-errcat). Accuracy under that rubric runs 0.8-2.9 points below the one the findings tables read, so do not mix a level from here with a level from the main report. Read down a column for how a rung fails and across a row for what the encoding changes. Because the denominator is the pool rather than the wrong answers, a falling row means the failure got rarer, full stop._

| error_category | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| insufficient_evidence | 26.0 | 16.8 | 6.1 | 7.0 |
| no_answer_reached | 6.0 | 6.0 | 6.8 | 6.1 |
| equivocal | 0.5 | 0.2 | 1.1 | 1.4 |
| wrong_count | 16.2 | 16.1 | 14.4 | 15.6 |
| wrong_value | 9.4 | 9.5 | 9.0 | 10.9 |
| wrong_entity | 7.3 | 10.7 | 7.7 | 10.2 |
| incomplete_list | 2.9 | 1.8 | 1.8 | 2.4 |
| over_inclusive_list | 1.7 | 1.9 | 2.2 | 2.4 |
| unit_or_format_mismatch | 0.8 | 1.1 | 1.3 | 1.1 |
| other | 0.2 | 0.2 | 0.1 | 0.2 |
| All incorrect | 71.0 | 64.3 | 50.5 | 57.4 |
| n (per col) | 834 | 833 | 833 | 833 |

### Error taxonomy x prompt mode (answerable pool, oracle pages, TLV)

> **swept**: error category × prompt mode (answerable pool, oracle pages, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **unit**: shares are of the questions in a column's pool, not of its wrong answers, so a column sums to its All incorrect row; categories are first-match-wins over config.ERROR_CATEGORIES · **denominator**: differs by mode — a prompt that lowers accuracy has more incorrect rows to distribute, so read beside the accuracy table

_Each cell is the share of that COLUMN'S QUESTIONS assigned the category, not the share of its wrong answers, so a column sums to its `All incorrect` row rather than to 100 and a cell can be read directly as a failure rate. The denominator is the scored questions in the column (its n), which excludes OOM cells: they carry no answer, so they are neither a right answer nor a kind of wrong one. Categories are assigned first-match-wins in `config.ERROR_CATEGORIES` order, so they are mutually exclusive by construction. Rows judged under the error-taxonomy rubric (`results.errcat.jsonl`, judge label gemini-flash-errcat). Accuracy under that rubric runs 0.8-2.9 points below the one the findings tables read, so do not mix a level from here with a level from the main report. Taken at TLV, the strongest rung, so what remains is a reasoning failure rather than an encoding one. Every column runs over the same questions, so the columns are directly comparable and `All incorrect` is 100 minus that prompt's accuracy. `answered_unanswerable` is dropped: the questions here have answers, so it can only be the judge misapplying the label._

| error_category | none | grounded | abstain | abstain_balanced | cot | extract_cot |
| --- | --- | --- | --- | --- | --- | --- |
| insufficient_evidence | 6.1 | 6.0 | 27.6 | 23.0 | 6.6 | 8.8 |
| no_answer_reached | 6.8 | 0.0 | 0.0 | 0.0 | 4.4 | 3.3 |
| equivocal | 1.1 | 0.1 | 0.0 | 0.0 | 0.0 | 0.1 |
| wrong_count | 14.4 | 18.8 | 10.9 | 11.8 | 14.8 | 12.7 |
| wrong_value | 9.0 | 14.6 | 8.8 | 10.8 | 8.5 | 10.1 |
| wrong_entity | 7.7 | 9.6 | 7.1 | 7.3 | 7.1 | 8.7 |
| incomplete_list | 1.8 | 2.6 | 1.9 | 2.0 | 2.9 | 2.2 |
| over_inclusive_list | 2.2 | 2.8 | 2.0 | 2.5 | 2.9 | 3.4 |
| unit_or_format_mismatch | 1.3 | 1.6 | 1.4 | 1.3 | 2.3 | 2.3 |
| other | 0.1 | 0.1 | 0.1 | 0.1 | 0.4 | 0.8 |
| All incorrect | 50.5 | 56.3 | 60.0 | 59.1 | 49.8 | 52.5 |
| n (per col) | 833 | 833 | 833 | 833 | 833 | 828 |

### Hallucination x prompt mode (unanswerable pool, bm25 k=3, TLV)

> **swept**: error category × prompt mode (unanswerable pool, bm25 k=3, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: no gold page exists for an unanswerable question, so this runs on the bm25 k=3 page set and its levels are not comparable with the answerable table's · **page_selection**: similarity (bm25, k=3) · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **unit**: shares are of the questions in a column's pool, not of its wrong answers, so a column sums to its All incorrect row; categories are first-match-wins over config.ERROR_CATEGORIES

_Each cell is the share of that COLUMN'S QUESTIONS assigned the category, not the share of its wrong answers, so a column sums to its `All incorrect` row rather than to 100 and a cell can be read directly as a failure rate. The denominator is the scored questions in the column (its n), which excludes OOM cells: they carry no answer, so they are neither a right answer nor a kind of wrong one. Categories are assigned first-match-wins in `config.ERROR_CATEGORIES` order, so they are mutually exclusive by construction. Rows judged under the error-taxonomy rubric (`results.errcat.jsonl`, judge label gemini-flash-errcat). Accuracy under that rubric runs 0.8-2.9 points below the one the findings tables read, so do not mix a level from here with a level from the main report. The unanswerable pool has no gold page to select, so it runs on the bm25 k=3 page set rather than on oracle pages and its levels are not comparable with the answerable table's. A question here is correct when the reasoner declines, so answering it substantively is the only error available and `All incorrect` reproduces the one category row._

| error_category | none | grounded | abstain | abstain_balanced | cot | extract_cot |
| --- | --- | --- | --- | --- | --- | --- |
| answered_unanswerable | 53.7 | 62.7 | 25.4 | 31.1 | 41.0 | 50.2 |
| All incorrect | 54.5 | 62.7 | 25.4 | 31.1 | 57.0 | 52.3 |
| n (per col) | 244 | 244 | 244 | 244 | 244 | 243 |

### Error taxonomy x evidence source (prompt = none, TLV)

> **swept**: error category × evidence source (answerable pool, oracle pages, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **unit**: shares are of the questions in a column's pool, not of its wrong answers, so a column sums to its All incorrect row; categories are first-match-wins over config.ERROR_CATEGORIES · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Each cell is the share of that COLUMN'S QUESTIONS assigned the category, not the share of its wrong answers, so a column sums to its `All incorrect` row rather than to 100 and a cell can be read directly as a failure rate. The denominator is the scored questions in the column (its n), which excludes OOM cells: they carry no answer, so they are neither a right answer nor a kind of wrong one. Categories are assigned first-match-wins in `config.ERROR_CATEGORIES` order, so they are mutually exclusive by construction. Rows judged under the error-taxonomy rubric (`results.errcat.jsonl`, judge label gemini-flash-errcat). Accuracy under that rubric runs 0.8-2.9 points below the one the findings tables read, so do not mix a level from here with a level from the main report. Evidence-source columns overlap: a question citing Chart and Table is counted under both, so their n do not sum to the pool and All sources is the same questions pooled once each rather than a row-wise sum. `(none)`, the questions with no source annotation, is dropped._

| error_category | Chart | Figure | Generalized-text (Layout) | Pure-text (Plain-text) | Table | All sources |
| --- | --- | --- | --- | --- | --- | --- |
| insufficient_evidence | 7.3 | 7.6 | 0.8 | 7.3 | 6.2 | 6.1 |
| no_answer_reached | 7.9 | 4.5 | 2.5 | 3.8 | 14.4 | 6.8 |
| equivocal | 1.1 | 1.4 | 0.8 | 0.3 | 1.4 | 1.1 |
| wrong_count | 10.1 | 24.1 | 28.8 | 12.9 | 7.7 | 14.4 |
| wrong_value | 15.7 | 4.8 | 5.9 | 9.1 | 15.4 | 9.0 |
| wrong_entity | 10.7 | 9.3 | 6.8 | 7.0 | 5.8 | 7.7 |
| incomplete_list | 1.7 | 2.8 | 1.7 | 2.1 | 0.5 | 1.8 |
| over_inclusive_list | 0.0 | 2.4 | 2.5 | 3.5 | 2.4 | 2.2 |
| unit_or_format_mismatch | 2.8 | 0.3 | 0.8 | 2.8 | 1.4 | 1.3 |
| other | 0.0 | 0.3 | 0.0 | 0.0 | 0.0 | 0.1 |
| All incorrect | 57.3 | 57.6 | 50.8 | 49.0 | 55.3 | 50.5 |
| n (per col) | 178 | 290 | 118 | 286 | 208 | 833 |

### Error taxonomy x gold evidence-page count (prompt = none, TLV)

> **swept**: error category × evidence page count (answerable pool, oracle pages, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **unit**: shares are of the questions in a column's pool, not of its wrong answers, so a column sums to its All incorrect row; categories are first-match-wins over config.ERROR_CATEGORIES · **hop**: single/multi only, hop=none dropped

_Each cell is the share of that COLUMN'S QUESTIONS assigned the category, not the share of its wrong answers, so a column sums to its `All incorrect` row rather than to 100 and a cell can be read directly as a failure rate. The denominator is the scored questions in the column (its n), which excludes OOM cells: they carry no answer, so they are neither a right answer nor a kind of wrong one. Categories are assigned first-match-wins in `config.ERROR_CATEGORIES` order, so they are mutually exclusive by construction. Rows judged under the error-taxonomy rubric (`results.errcat.jsonl`, judge label gemini-flash-errcat). Accuracy under that rubric runs 0.8-2.9 points below the one the findings tables read, so do not mix a level from here with a level from the main report. `Multi` pools the 2-page and 3+-page columns, so it overlaps them rather than extending them and the four columns are not a partition. Questions with no annotated evidence page are dropped, the same treatment the integration tables give them. The multi-page deficit is an accuracy result; this says which failure the extra pages cause._

| error_category | 1 page | 2 pages | 3+ pages | Multi |
| --- | --- | --- | --- | --- |
| insufficient_evidence | 6.3 | 5.9 | 1.8 | 4.6 |
| no_answer_reached | 2.5 | 15.1 | 8.1 | 12.9 |
| equivocal | 0.6 | 2.1 | 0.9 | 1.7 |
| wrong_count | 10.1 | 10.9 | 39.6 | 20.0 |
| wrong_value | 7.4 | 14.6 | 4.5 | 11.4 |
| wrong_entity | 7.8 | 9.6 | 3.6 | 7.7 |
| incomplete_list | 1.7 | 1.7 | 2.7 | 2.0 |
| over_inclusive_list | 2.5 | 1.7 | 1.8 | 1.7 |
| unit_or_format_mismatch | 1.5 | 1.3 | 0.9 | 1.1 |
| other | 0.2 | 0.0 | 0.0 | 0.0 |
| All incorrect | 40.5 | 62.8 | 64.0 | 63.1 |
| n (per col) | 476 | 239 | 111 | 350 |

## Calibration, re-judged

### Faithfulness: answerable accuracy by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. The `none` row must reproduce the G1 headline ladder (31.9 / 39.4 / 56.8 / 45.9 for T / TL / TLV / V) within 1 point. FLAGGED ⚠: T 29.0 vs 31.9; TL 35.7 vs 39.4; TLV 49.5 vs 56.8; V 42.6 vs 45.9. This grid runs the full answerable pool while the ladder lost part of it to OOM on the 16 GB V100, and the recovered cells are the harder ones, so the gap is pool coverage rather than drift: on the cells both runs scored the two agree (see the oom_recovery table). Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 29.0 [24.5-33.6] (n=834) a26.3 w44.7 ⚠ | 35.7 [31.6-39.5] (n=833) a17.2 w47.2 ⚠ | 49.5 [45.0-53.4] (n=833) a6.2 w44.3 ⚠ | 42.6 [38.9-46.4] (n=833) a7.1 w50.3 ⚠ |
| grounded | 24.9 [20.6-28.6] (n=834) a24.1 w51.0 | 32.3 [28.3-35.9] (n=833) a16.2 w51.5 | 43.7 [39.5-47.9] (n=833) a6.0 w50.3 | 37.9 [33.8-41.9] (n=833) a6.5 w55.6 |
| abstain | 21.7 [17.7-25.2] (n=834) a52.8 w25.5 | 27.9 [24.3-31.2] (n=833) a47.7 w24.5 | 40.0 [35.7-44.1] (n=833) a27.7 w32.3 | 31.9 [28.1-35.9] (n=833) a32.3 w35.8 |
| abstain_balanced | 21.7 [17.7-25.4] (n=834) a48.2 w30.1 | 28.6 [24.8-32.0] (n=833) a43.5 w28.0 | 40.9 [36.3-45.1] (n=833) a23.2 w35.9 | 33.5 [29.7-37.5] (n=833) a27.9 w38.7 |
| cot | 26.9 [22.8-30.9] (n=834) a13.3 w59.8 | 34.1 [30.7-37.7] (n=833) a21.7 w44.2 | 50.2 [46.6-54.2] (n=833) a6.6 w43.2 | 46.9 [42.8-51.1] (n=832) a5.3 w47.8 |
| extract_cot | 26.1 [22.4-30.2] (n=832) a19.4 w54.6 | 33.5 [29.7-37.2] (n=830) a26.5 w40.0 | 47.5 [43.8-51.1] (n=828) a8.8 w43.7 | 41.6 [37.4-45.6] (n=829) a11.6 w46.8 |
| n (per col) | 5002 | 4995 | 4993 | 4993 |

### Cost of each rung: accuracy, tokens fed, and the two latency halves

> **swept**: rung → accuracy, tokens fed, prefill and decode latency · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **why**: so a cost cell reads against the ladder tables, which are scored by this judge; the main report's copy of this table is the accuracy rubric's and the two are not interchangeable · **TV**: pulled in from g1-tv-full, which the builder loads itself because that rung has its own run_tag and task; it reads this same judged file · **latency**: wall clock on the measuring machine; a scale, not an absolute · **oom**: not measurable on this pool, whose failed cells were re-run on larger hardware; see the main report's oom_frontier

_Uninstructed prompt, oracle pages, complete answerable pool. Latency is wall clock on the measuring machine and is a scale, not an absolute: it moves with the GPU. `input tokens` is text plus visual and is what the representation buys or costs; `output tokens` and `decode_s` are set by the prompt and the decode budget rather than by the rung, so a rung that appears to decode more is one whose longer input drew a longer answer. The two halves do not sum to end-to-end latency, which also carries scheduling and detokenisation. OOM is not measurable on this pool, whose failed cells were re-run on larger hardware; `oom_frontier` reports it from the preserved V100 snapshot._

| rung | accuracy | text tokens | visual tokens | input tokens | prefill_s | output tokens | decode_s |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 29.0 [24.5-33.6] | 932 | 0 | 932 | 0.1 | 115 | 2.0 |
| TL | 35.7 [31.6-39.5] | 1632 | 0 | 1632 | 0.1 | 133 | 2.3 |
| TV | 50.1 [46.4-53.7] | 929 | 3404 | 4333 | 0.1 | 140 | 2.4 |
| TLV | 49.5 [45.0-53.4] | 1632 | 3427 | 5058 | 0.2 | 136 | 2.4 |
| V | 42.6 [38.9-46.4] | 38 | 3427 | 3464 | 0.1 | 139 | 2.4 |

### Faithfulness: answerable abstention rate by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **direction**: abstaining is an error only where the RUNG carried the evidence; read the d component

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. NOT ALL OF THIS IS FALSE ABSTENTION. The oracle pages carry the evidence, but the RUNG need not: `T` is PyMuPDF's embedded text layer, and a scanned page has none, so at `T` on a scanned document the reasoner is handed an empty document and declining is the correct response to what it was actually given. The cells carry the split as `<digital>d/<scanned>s`, and it is stark: under `abstain` at `T`, scanned questions abstain 100.0% against 38.4% digital, and under `none` 22.1% against 3.0%. `TL` recovers most of it because the parser OCRs the page (57.4s under `abstain`), and TLV/V always carry the image. Read the `d` component as false abstention; the `s` component at `T` is the encoding delivering nothing, which is the ladder's own finding, not a prompting one. Lower is better on the born-digital component, the opposite of the unanswerable table. Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 26.4 (n=834) 13.2d/71.1s | 17.3 (n=833) 15.6d/23.2s | 6.5 (n=833) 6.4d/6.8s | 7.1 (n=833) 7.3d/6.3s |
| grounded | 24.1 (n=834) 12.7d/62.6s | 16.2 (n=833) 15.6d/18.4s | 6.0 (n=833) 6.2d/5.3s | 6.5 (n=833) 7.0d/4.7s |
| abstain | 52.8 (n=834) 38.8d/100.0s | 47.7 (n=833) 44.8d/57.4s | 27.7 (n=833) 30.0d/20.0s | 32.3 (n=833) 35.3d/22.1s |
| abstain_balanced | 48.2 (n=834) 32.9d/100.0s | 43.5 (n=833) 40.1d/54.7s | 23.2 (n=833) 25.5d/15.3s | 27.9 (n=833) 30.2d/20.0s |
| cot | 13.3 (n=834) 14.4d/9.5s | 21.7 (n=833) 20.2d/26.8s | 6.6 (n=833) 7.8d/2.6s | 5.3 (n=832) 5.8d/3.7s |
| extract_cot | 19.4 (n=832) 17.6d/25.3s | 26.5 (n=830) 23.2d/37.6s | 8.9 (n=828) 8.9d/9.0s | 11.6 (n=829) 12.7d/7.9s |
| n (per col) | 5002 | 4995 | 4993 | 4993 |

### Faithfulness: answerable accuracy by prompt mode, evidence source and rung (oracle pages)

> **swept**: prompt_mode × evidence source × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. A regroup of the pooled grid, not new inference: `evidence_sources` is a per-row covariate on every judged row, so this is the same cells re-aggregated. A question citing several evidence sources is counted under EACH of them, so the per-source rows overlap and CANNOT be summed; the bolded All sources row closing each prompt mode is computed fresh over every row, each counted once, and reproduces the pooled table. † marks a cell computed on fewer than 30 rows, where a single question moves it by more than three points: read the direction, not the value. Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Chart | 16.3 [10.7-21.9] (n=178) a32.6 w51.1 | 16.9 [11.3-23.2] (n=178) a28.1 w55.1 | 42.7 [34.4-51.6] (n=178) a7.3 w50.0 | 40.4 [32.0-49.2] (n=178) a6.2 w53.4 |
| none | Figure | 14.5 [10.3-19.2] (n=290) a36.6 w49.0 | 22.1 [16.7-28.2] (n=290) a24.8 w53.1 | 42.4 [35.7-48.6] (n=290) a7.6 w50.0 | 39.0 [32.9-44.9] (n=290) a7.9 w53.1 |
| none | Generalized-text (Layout) | 26.3 [16.4-35.9] (n=118) a20.3 w53.4 | 33.9 [24.2-43.6] (n=118) a10.2 w55.9 | 49.2 [40.8-57.1] (n=118) a0.8 w50.0 | 43.2 [34.9-51.7] (n=118) a4.2 w52.5 |
| none | Pure-text (Plain-text) | 36.9 [29.5-44.4] (n=287) a23.0 w40.1 | 44.4 [37.3-51.6] (n=286) a11.5 w44.1 | 51.0 [43.4-58.4] (n=286) a7.3 w41.6 | 42.3 [35.7-49.1] (n=286) a8.0 w49.7 |
| none | Table | 35.6 [29.7-41.7] (n=208) a15.9 w48.6 | 44.7 [37.0-52.1] (n=208) a7.2 w48.1 | 44.7 [37.6-52.2] (n=208) a6.7 w48.6 | 34.1 [26.6-41.4] (n=208) a9.1 w56.7 |
| none | (none) | 52.6 [31.2-73.7] (n=19) a26.3 w21.1† | 63.2 [38.9-83.3] (n=19) a15.8 w21.1† | 73.7 [52.6-91.3] (n=19) a10.5 w15.8† | 47.4 [27.7-66.7] (n=19) a5.3 w47.4† |
| none | **All sources** | 29.0 [24.5-33.6] (n=834) a26.3 w44.7 | 35.7 [31.6-39.5] (n=833) a17.2 w47.2 | 49.5 [45.0-53.4] (n=833) a6.2 w44.3 | 42.6 [38.9-46.4] (n=833) a7.1 w50.3 |
| grounded | Chart | 15.2 [9.0-21.8] (n=178) a28.1 w56.7 | 14.6 [9.5-20.9] (n=178) a23.0 w62.4 | 31.5 [24.8-38.8] (n=178) a5.1 w63.5 | 28.1 [21.6-35.2] (n=178) a5.6 w66.3 |
| grounded | Figure | 11.4 [7.7-15.9] (n=290) a34.1 w54.5 | 21.4 [16.1-27.0] (n=290) a21.4 w57.2 | 40.7 [34.3-46.7] (n=290) a7.2 w52.1 | 37.9 [32.0-43.9] (n=290) a7.9 w54.1 |
| grounded | Generalized-text (Layout) | 19.5 [11.7-28.6] (n=118) a17.8 w62.7 | 29.7 [20.7-38.6] (n=118) a6.8 w63.6 | 43.2 [33.9-53.3] (n=118) a0.0 w56.8 | 44.9 [35.6-54.9] (n=118) a0.8 w54.2 |
| grounded | Pure-text (Plain-text) | 35.2 [28.4-41.9] (n=287) a19.9 w44.9 | 42.3 [34.9-48.7] (n=286) a10.1 w47.6 | 49.0 [41.0-56.3] (n=286) a7.0 w44.1 | 40.6 [34.0-47.5] (n=286) a6.3 w53.1 |
| grounded | Table | 27.9 [22.1-34.3] (n=208) a17.3 w54.8 | 37.5 [30.4-45.3] (n=208) a13.0 w49.5 | 38.5 [31.1-47.0] (n=208) a7.2 w54.3 | 28.4 [22.3-36.1] (n=208) a8.2 w63.5 |
| grounded | (none) | 36.8 [17.4-61.1] (n=19) a15.8 w47.4† | 57.9 [33.3-81.8] (n=19) a15.8 w26.3† | 52.6 [29.4-75.0] (n=19) a5.3 w42.1† | 36.8 [15.8-58.8] (n=19) a5.3 w57.9† |
| grounded | **All sources** | 24.9 [20.6-28.6] (n=834) a24.1 w51.0 | 32.3 [28.3-35.9] (n=833) a16.2 w51.5 | 43.7 [39.5-47.9] (n=833) a6.0 w50.3 | 37.9 [33.8-41.9] (n=833) a6.5 w55.6 |
| abstain | Chart | 13.5 [7.8-19.9] (n=178) a52.2 w34.3 | 11.8 [6.7-17.6] (n=178) a59.0 w29.2 | 26.4 [20.1-33.7] (n=178) a25.3 w48.3 | 22.5 [16.2-29.3] (n=178) a27.5 w50.0 |
| abstain | Figure | 6.9 [3.8-10.5] (n=290) a76.2 w16.9 | 13.8 [9.9-17.5] (n=290) a65.2 w21.0 | 34.1 [27.5-40.6] (n=290) a35.5 w30.3 | 30.3 [24.4-36.2] (n=290) a38.3 w31.4 |
| abstain | Generalized-text (Layout) | 19.5 [11.7-28.6] (n=118) a55.9 w24.6 | 25.4 [17.6-33.6] (n=118) a44.1 w30.5 | 41.5 [31.9-51.6] (n=118) a19.5 w39.0 | 37.3 [28.0-47.1] (n=118) a25.4 w37.3 |
| abstain | Pure-text (Plain-text) | 31.7 [25.2-38.0] (n=287) a42.5 w25.8 | 37.8 [31.2-44.4] (n=286) a36.0 w26.2 | 43.7 [36.0-51.3] (n=286) a24.1 w32.2 | 34.3 [27.6-41.4] (n=286) a31.1 w34.6 |
| abstain | Table | 24.5 [18.8-30.7] (n=208) a43.3 w32.2 | 37.0 [30.0-44.9] (n=208) a37.0 w26.0 | 38.5 [31.3-46.1] (n=208) a30.3 w31.2 | 26.4 [20.5-33.3] (n=208) a38.9 w34.6 |
| abstain | (none) | 31.6 [12.5-55.6] (n=19) a36.8 w31.6† | 52.6 [25.0-77.3] (n=19) a31.6 w15.8† | 57.9 [30.0-81.8] (n=19) a26.3 w15.8† | 36.8 [15.8-58.8] (n=19) a36.8 w26.3† |
| abstain | **All sources** | 21.7 [17.7-25.2] (n=834) a52.8 w25.5 | 27.9 [24.3-31.2] (n=833) a47.7 w24.5 | 40.0 [35.7-44.1] (n=833) a27.7 w32.3 | 31.9 [28.1-35.9] (n=833) a32.3 w35.8 |
| abstain_balanced | Chart | 12.4 [6.9-18.9] (n=178) a44.9 w42.7 | 11.8 [6.4-17.8] (n=178) a51.7 w36.5 | 28.1 [21.4-35.9] (n=178) a18.5 w53.4 | 23.0 [17.2-29.4] (n=178) a24.2 w52.8 |
| abstain_balanced | Figure | 6.9 [3.8-10.6] (n=290) a71.7 w21.4 | 14.5 [10.1-18.9] (n=290) a62.4 w23.1 | 35.5 [29.4-41.5] (n=290) a31.4 w33.1 | 32.8 [26.4-38.9] (n=290) a33.4 w33.8 |
| abstain_balanced | Generalized-text (Layout) | 19.5 [11.7-28.6] (n=118) a52.5 w28.0 | 28.8 [20.0-37.8] (n=118) a41.5 w29.7 | 41.5 [32.5-50.9] (n=118) a18.6 w39.8 | 39.8 [30.5-50.0] (n=118) a21.2 w39.0 |
| abstain_balanced | Pure-text (Plain-text) | 31.0 [24.2-37.3] (n=287) a39.7 w29.3 | 37.8 [30.9-44.3] (n=286) a33.2 w29.0 | 45.5 [37.8-53.0] (n=286) a19.2 w35.3 | 34.3 [27.7-41.1] (n=286) a25.5 w40.2 |
| abstain_balanced | Table | 24.0 [18.3-30.2] (n=208) a38.5 w37.5 | 36.1 [29.3-43.8] (n=208) a30.3 w33.7 | 35.6 [28.8-43.6] (n=208) a25.5 w38.9 | 28.4 [22.4-35.7] (n=208) a34.6 w37.0 |
| abstain_balanced | (none) | 36.8 [17.4-61.1] (n=19) a26.3 w36.8† | 57.9 [33.3-81.8] (n=19) a31.6 w10.5† | 63.2 [37.5-87.5] (n=19) a21.1 w15.8† | 36.8 [15.8-58.8] (n=19) a31.6 w31.6† |
| abstain_balanced | **All sources** | 21.7 [17.7-25.4] (n=834) a48.2 w30.1 | 28.6 [24.8-32.0] (n=833) a43.5 w28.0 | 40.9 [36.3-45.1] (n=833) a23.2 w35.9 | 33.5 [29.7-37.5] (n=833) a27.9 w38.7 |
| cot | Chart | 19.7 [13.7-25.6] (n=178) a16.3 w64.0 | 16.3 [11.2-22.1] (n=178) a42.1 w41.6 | 43.3 [36.1-50.9] (n=178) a9.6 w47.2 | 38.2 [30.1-46.2] (n=178) a5.6 w56.2 |
| cot | Figure | 11.0 [7.1-15.5] (n=290) a15.9 w73.1 | 17.9 [13.5-22.7] (n=290) a26.2 w55.9 | 43.8 [36.4-50.3] (n=290) a6.9 w49.3 | 43.8 [37.6-50.0] (n=290) a5.9 w50.3 |
| cot | Generalized-text (Layout) | 25.4 [16.7-34.5] (n=118) a3.4 w71.2 | 34.7 [25.2-44.0] (n=118) a11.0 w54.2 | 49.2 [38.9-59.6] (n=118) a3.4 w47.5 | 54.2 [44.8-63.4] (n=118) a3.4 w42.4 |
| cot | Pure-text (Plain-text) | 32.4 [26.3-38.7] (n=287) a13.9 w53.7 | 42.3 [35.4-49.2] (n=286) a15.7 w42.0 | 51.0 [43.9-58.0] (n=286) a7.7 w41.3 | 46.2 [39.4-52.4] (n=286) a5.6 w48.3 |
| cot | Table | 37.5 [31.5-43.9] (n=208) a10.6 w51.9 | 48.6 [42.1-55.2] (n=208) a12.0 w39.4 | 51.4 [45.9-58.0] (n=208) a7.2 w41.3 | 44.0 [35.7-52.4] (n=207) a5.3 w50.7 |
| cot | (none) | 26.3 [5.6-47.1] (n=19) a21.1 w52.6† | 57.9 [37.5-77.8] (n=19) a10.5 w31.6† | 57.9 [36.3-81.2] (n=19) a15.8 w26.3† | 52.6 [30.0-75.0] (n=19) a10.5 w36.8† |
| cot | **All sources** | 26.9 [22.8-30.9] (n=834) a13.3 w59.8 | 34.1 [30.7-37.7] (n=833) a21.7 w44.2 | 50.2 [46.6-54.2] (n=833) a6.6 w43.2 | 46.9 [42.8-51.1] (n=832) a5.3 w47.8 |
| extract_cot | Chart | 13.1 [8.0-18.7] (n=176) a19.3 w67.6 | 16.3 [10.3-22.8] (n=178) a37.6 w46.1 | 36.6 [29.1-44.8] (n=175) a6.3 w57.1 | 35.6 [27.2-45.2] (n=177) a7.3 w57.1 |
| extract_cot | Figure | 10.3 [6.7-14.6] (n=290) a27.6 w62.1 | 20.1 [15.2-25.8] (n=288) a36.5 w43.4 | 43.3 [36.8-49.6] (n=289) a11.1 w45.7 | 39.4 [33.6-45.3] (n=289) a11.8 w48.8 |
| extract_cot | Generalized-text (Layout) | 21.2 [13.2-30.6] (n=118) a7.6 w71.2 | 34.2 [25.0-43.5] (n=117) a18.8 w47.0 | 51.3 [42.9-59.7] (n=117) a2.6 w46.2 | 51.7 [43.6-60.2] (n=118) a4.2 w44.1 |
| extract_cot | Pure-text (Plain-text) | 34.5 [27.4-41.1] (n=287) a17.1 w48.4 | 40.4 [33.8-47.1] (n=285) a19.3 w40.4 | 48.2 [41.2-54.9] (n=284) a9.9 w41.9 | 41.2 [34.5-48.3] (n=284) a11.6 w47.2 |
| extract_cot | Table | 37.7 [30.6-44.8] (n=207) a13.0 w49.3 | 46.2 [40.3-52.1] (n=208) a14.4 w39.4 | 49.0 [43.3-55.5] (n=208) a9.6 w41.3 | 36.9 [29.7-44.1] (n=206) a17.0 w46.1 |
| extract_cot | (none) | 42.1 [18.8-62.5] (n=19) a15.8 w42.1† | 47.4 [22.2-72.0] (n=19) a26.3 w26.3† | 57.9 [30.0-81.8] (n=19) a15.8 w26.3† | 42.1 [19.0-62.5] (n=19) a31.6 w26.3† |
| extract_cot | **All sources** | 26.1 [22.4-30.2] (n=832) a19.4 w54.6 | 33.5 [29.7-37.2] (n=830) a26.5 w40.0 | 47.5 [43.8-51.1] (n=828) a8.8 w43.7 | 41.6 [37.4-45.6] (n=829) a11.6 w46.8 |
| n (per col) | - | - | - | - | - |

### Faithfulness: where each outcome category's mass moves under the abstention instruction (answerable pool, oracle pages)

> **swept**: outcome category × direction (none→abstain, answerable pool, oracle pages, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **reading**: entered − left is that category's level change, so the block reconciles with faithfulness_answerable_accuracy row for row

_Paired on question_id at one rung: a question counts only when BOTH prompt modes produced a status==ok row there. `entered` is the share of the paired pool that was NOT in a category under the base mode and IS under the target one; `left` is the reverse. Both are percentages of the paired n, so `entered - left` is that category's level change in points and the three categories' nets sum to zero. Categories are `_common.outcome_rates`'s disjoint split, the same one the level tables carry as their `a`/`w` components: `correct`, `declined` (an abstention the judge did not credit), and `wrong`. On the unanswerable pool a credited refusal is CORRECT, so `correct` there is the declined share and `wrong` is answering anyway. Oracle pages under both modes; only the instruction changes._

| pool | category | none (%) | abstain (%) | entered (%) | left (%) | net (pts) | paired n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| answerable | correct | 49.5 | 40.0 | 2.5 (21) | 12.0 (100) | -9.5 | 833 |
| answerable | declined | 6.2 | 27.7 | 21.6 (180) | 0.1 (1) | +21.5 | 833 |
| answerable | wrong | 44.3 | 32.3 | 8.2 (68) | 20.2 (168) | -12.0 | 833 |

### Faithfulness: where each outcome category's mass moves under the abstention instruction (unanswerable pool, bm25 k=3 pages)

> **swept**: outcome category × direction (none→abstain, unanswerable pool, bm25 k=3, TLV) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: no gold page exists for an unanswerable question, so this runs on the bm25 k=3 page set and its levels are not comparable with the answerable table's · **page_selection**: similarity (bm25, k=3) · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's

_Paired on question_id at one rung: a question counts only when BOTH prompt modes produced a status==ok row there. `entered` is the share of the paired pool that was NOT in a category under the base mode and IS under the target one; `left` is the reverse. Both are percentages of the paired n, so `entered - left` is that category's level change in points and the three categories' nets sum to zero. Categories are `_common.outcome_rates`'s disjoint split, the same one the level tables carry as their `a`/`w` components: `correct`, `declined` (an abstention the judge did not credit), and `wrong`. On the unanswerable pool a credited refusal is CORRECT, so `correct` there is the declined share and `wrong` is answering anyway. An unanswerable question has no gold page, so this runs on the bm25 k=3 set and its levels are not comparable with the answerable table's._

| pool | category | none (%) | abstain (%) | entered (%) | left (%) | net (pts) | paired n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| unanswerable | correct | 45.5 | 74.6 | 31.1 (76) | 2.0 (5) | +29.1 | 244 |
| unanswerable | declined | 0.0 | 0.0 | 0.0 (0) | 0.0 (0) | +0.0 | 244 |
| unanswerable | wrong | 54.5 | 25.4 | 2.0 (5) | 31.1 (76) | -29.1 | 244 |

## Judge provenance

### Verdict transitions, original judge -> error-taxonomy judge (prompt = none)

> **swept**: verdict transition × rung (answerable pool, oracle pages, prompt = none) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **judge**: results.errcat.jsonl — judge label gemini-flash-errcat, the error-taxonomy prompt. Same model and same correctness rubric as the main report's judge, but 1.8-3.0 points stricter in practice; levels are not interchangeable with the main report's · **pairing**: on cell identity; a cell either judge missed is dropped, not counted as a change

_Shares (%) of the cells BOTH judges scored, paired on cell identity; a cell either judge missed is dropped rather than counted as a change. The correctness rubric is byte-identical between the two prompts and is pinned by a test, so `correct -> wrong` is the taxonomy prompt reading the same rubric more strictly, not a different rubric. The abstention rows are the intended change: the original prompt listed `abstained` as a verdict without defining it, so refusals were counted by string match and undercounted. The two abstention rows are not exclusive with the correctness rows above them and do not sum with them._

| transition | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| correct -> correct | 29.0 | 35.7 | 49.5 | 42.1 |
| correct -> wrong | 2.0 | 2.5 | 2.6 | 3.4 |
| wrong -> correct | 0.0 | 0.0 | 0.0 | 0.5 |
| wrong -> wrong | 68.9 | 61.8 | 47.9 | 54.0 |
| gained abstention | 18.8 | 13.9 | 4.8 | 6.0 |
| lost abstention | 0.0 | 0.0 | 0.0 | 0.0 |
| n (per col) | 834 | 833 | 833 | 833 |
