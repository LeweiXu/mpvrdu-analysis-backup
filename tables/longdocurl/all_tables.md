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
| g1-quantization-full | G1_oracle_ladder | 5256 | 4961 | 295 | 0 | 5.6 |
| g1-quantization-scanned | G1_oracle_ladder | 1520 | 1488 | 32 | 0 | 2.1 |
| g1-reasoner-32b-matched | G1_oracle_ladder | 6776 | 6775 | 1 | 0 | 0.0 |
| g1-reasoner-full | G1_oracle_ladder | 7884 | 7525 | 359 | 0 | 4.6 |
| g1-reasoner-glm4v-9b | G1_oracle_ladder | 3388 | 3270 | 118 | 0 | 3.5 |
| g1-reasoner-scanned | G1_oracle_ladder | 2280 | 2239 | 41 | 0 | 1.8 |
| g1-representation-full | G1_oracle_ladder | 3388 | 3143 | 245 | 0 | 7.2 |
| g1-resolution-full | G1_oracle_ladder | 3942 | 3549 | 393 | 0 | 10.0 |
| g1-resolution-scanned | G1_oracle_ladder | 1140 | 1071 | 69 | 0 | 6.1 |
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
| g5c-gold1 | G5_selection | 1445 | 765 | 662 | 18 | 45.8 |
| g5c-gold2 | G5_selection | 492 | 200 | 282 | 10 | 57.3 |
| g6-strategies | G6_reasoning | 1694 | 1380 | 314 | 0 | 18.5 |
| g6-thinking | G6_reasoning | 847 | 735 | 112 | 0 | 13.2 |
| g7-models | G1_oracle_ladder | 10164 | 9493 | 671 | 0 | 6.6 |
| **all** |  | **120800** | 114887 | 5429 | 484 | 4.5 |

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Headline: cost-ordered ladder accuracy by task family (oracle pages)

> **swept**: representation ladder T/TL/TV/TLV/V · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. LongDocURL has no document-domain labels. `task_tag` is the coarsest question annotation it carries (Understanding / Locating / Reasoning) and is what the doc_type column of the rebuilt tables actually holds; this table names it honestly. `question_type` below is nested inside it: every type belongs to exactly one tag, so the two are the same partition at different resolutions. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. _

| task_tag | T | TL | TV | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Understanding | 74.1 [70.4-77.9] a1.3 w24.6 | 77.1 [74.2-80.0] a1.2 w21.7 | 81.7 [79.5-83.9] a0.2 w18.1 | 83.4 [81.1-85.4] a0.5 w16.1 | 74.6 [72.1-77.1] a0.4 w25.0 | TV | 6066 |
| Locating | 43.5 [37.6-49.5] a0.3 w56.2 | 51.6 [45.5-58.1] a0.4 w48.0 | 46.5 [41.8-51.7] a0.0 w53.5 | 50.0 [44.5-55.9] a0.0 w50.0 | 45.4 [40.2-50.6] a0.0 w54.6 | T | 3378 |
| Reasoning | 66.8 [61.3-72.1] a1.3 w31.9 | 67.5 [62.8-72.1] a0.6 w31.9 | 71.9 [66.8-76.3] a0.5 w27.6 | 73.3 [68.8-77.7] a0.6 w26.1 | 58.3 [53.2-63.4] a0.3 w41.5 | T | 1818 |
| **all doc_types** | **63.7 [60.3-66.9] a1.0 w35.3** | **68.0 [65.5-70.5] a0.9 w31.2** | **69.5 [67.1-71.8] a0.2 w30.3** | **71.9 [69.4-74.3] a0.4 w27.8** | **63.1 [60.4-65.9] a0.3 w36.6** | **TL** | **11262** |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - | - |

### Question type: ladder accuracy by LongDocURL question type (oracle pages)

> **swept**: question type (9 classes, nested inside task_tag) x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **grouping**: LongDocURL question_type, joined from the corpus: the result row does not carry it · **thin rows**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. The nine question types, printed grouped by the task_tag each belongs to (Understanding: extract | Locating: extract_fig2tab, topic2title, summary2title, summary2tab | Reasoning: calculate, count, compare, summarize). This is the finest question annotation either corpus carries and it is the reason for running LongDocURL: the types differ in what evidence they need, so a rung that helps `extract_fig2tab` need not help `calculate`. The tail types are thin (summarize is 13 questions in the corpus) — read the per-row n. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. _

| question_type | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| extract | 74.1 [70.4-77.9] a1.3 w24.6 | 77.1 [74.2-80.0] a1.2 w21.7 | 81.7 [79.5-83.9] a0.2 w18.1 | 83.4 [81.1-85.4] a0.5 w16.1 | 74.6 [72.1-77.1] a0.4 w25.0 | 6066 |
| extract_fig2tab | 58.4 [47.5-68.8] a0.0 w41.6 | 71.6 [62.4-79.9] a1.4 w27.0 | 54.5 [44.8-63.3] a0.0 w45.5 | 62.3 [52.5-72.2] a0.0 w37.7 | 55.4 [45.8-64.6] a0.0 w44.6 | 1135 |
| topic2title | 27.9 [20.3-36.0] a0.0 w72.1 | 28.8 [21.9-36.5] a0.0 w71.2 | 34.8 [28.0-42.3] a0.0 w65.2 | 35.1 [28.7-41.8] a0.0 w64.9 | 30.8 [24.6-37.3] a0.0 w69.2 | 992 |
| summary2title | 67.2 [58.1-75.4] a0.7 w32.1 | 81.1 [73.5-87.8] a0.0 w18.9 | 75.0 [66.9-83.1] a0.0 w25.0 | 77.2 [68.8-84.0] a0.0 w22.8 | 74.3 [66.7-81.8] a0.0 w25.7 | 661 |
| summary2tab | 14.9 [8.2-22.4] a0.8 w84.3 | 18.3 [10.3-27.9] a0.0 w81.7 | 19.0 [11.5-27.8] a0.0 w81.0 | 19.6 [9.7-30.7] a0.0 w80.4 | 19.0 [11.1-27.1] a0.0 w81.0 | 590 |
| calculate | 61.0 [50.4-72.1] a2.8 w36.2 | 66.7 [57.7-75.3] a0.8 w32.6 | 69.8 [62.4-78.1] a0.7 w29.5 | 72.8 [63.8-80.8] a0.0 w27.2 | 50.7 [42.2-60.1] a0.0 w49.3 | 678 |
| count | 57.9 [49.1-67.0] a0.9 w41.2 | 56.2 [46.1-66.0] a1.0 w42.9 | 64.2 [55.1-72.6] a0.0 w35.8 | 66.0 [57.0-75.7] a1.0 w33.0 | 58.0 [49.1-66.1] a0.0 w42.0 | 540 |
| compare | 81.1 [72.6-89.3] a0.0 w18.9 | 78.8 [70.7-86.7] a0.0 w21.2 | 81.8 [74.5-88.9] a0.9 w17.3 | 80.2 [73.3-87.5] a1.0 w18.8 | 65.2 [56.9-73.1] a0.9 w33.9 | 538 |
| summarize | 84.6 [61.5-100.0] a0.0 w15.4 | 76.9 [53.8-100.0] a0.0 w23.1 | 75.0 [50.0-100.0] a0.0 w25.0 | 81.8 [63.4-100.0] a0.0 w18.2 | 84.6 [61.5-100.0] a0.0 w15.4 | 62 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Answer format: ladder accuracy by expected answer shape (oracle pages)

> **swept**: expected answer format (String / List / Integer / Float / None) x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **grouping**: LongDocURL answer_format, joined from the corpus · **reading**: a confound, not a lever: a List answer must be produced complete to score right

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. The expected shape of the answer (String / List / Integer / Float / None), which LongDocURL annotates and MMLongBench does not. It is a confound worth seeing: a List answer must be produced complete to be scored right, so its accuracy sits below a String one for reasons that are not about the rung. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. _

| answer_format | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| String | 77.1 [73.5-80.5] a0.8 w22.1 | 81.4 [78.7-84.2] a0.9 w17.7 | 79.0 [75.6-82.2] a0.1 w20.9 | 81.5 [78.5-84.6] a0.1 w18.4 | 75.8 [72.7-78.9] a0.2 w24.0 | 4613 |
| List | 43.2 [38.4-47.6] a0.8 w56.0 | 47.5 [42.8-52.1] a0.4 w52.1 | 51.5 [47.3-55.9] a0.0 w48.5 | 53.8 [49.4-58.7] a0.0 w46.2 | 45.8 [41.1-50.3] a0.3 w53.9 | 3674 |
| Integer | 65.8 [60.4-71.2] a1.6 w32.6 | 70.4 [65.4-74.9] a1.7 w27.9 | 75.5 [71.6-79.5] a0.5 w24.0 | 77.6 [72.9-82.1] a1.3 w21.1 | 64.6 [59.8-69.7] a0.5 w34.9 | 2064 |
| Float | 74.3 [63.9-82.9] a1.6 w24.0 | 75.6 [68.6-82.1] a0.6 w23.9 | 80.8 [74.4-86.7] a1.1 w18.1 | 81.8 [75.6-87.0] a1.2 w17.1 | 65.9 [56.6-74.1] a0.0 w34.1 | 896 |
| None | 100.0 [100.0-100.0] a0.0 w0.0 | 100.0 [100.0-100.0] a0.0 w0.0 | 100.0 [100.0-100.0] a0.0 w0.0 | 100.0 [100.0-100.0] a0.0 w0.0 | 66.7 [33.3-100.0] a0.0 w33.3 | 15 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. _

| evidence_source | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| Figure | 62.5 [56.3-67.9] a1.4 w36.1 | 65.7 [60.1-70.7] a1.5 w32.8 | 67.9 [62.8-73.1] a0.2 w31.9 | 73.4 [68.5-78.4] a0.6 w26.0 | 65.2 [60.0-70.1] a0.2 w34.7 | 2746 |
| Layout | 48.7 [43.9-53.6] a0.5 w50.8 | 52.4 [47.8-57.7] a0.3 w47.3 | 56.4 [51.1-61.5] a0.3 w43.4 | 56.3 [51.1-61.2] a0.4 w43.2 | 52.2 [47.4-56.9] a0.4 w47.4 | 3725 |
| Others | 100.0 [100.0-100.0] a0.0 w0.0 | 100.0 [100.0-100.0] a0.0 w0.0 | 100.0 [100.0-100.0] a0.0 w0.0 | 87.5 [62.5-100.0] a0.0 w12.5 | 75.0 [55.6-100.0] a0.0 w25.0 | 40 |
| Table | 61.2 [55.5-67.1] a0.9 w37.9 | 69.5 [65.6-73.3] a1.1 w29.3 | 64.6 [60.1-69.3] a0.0 w35.4 | 68.2 [63.6-72.5] a0.3 w31.6 | 57.3 [52.6-61.9] a0.1 w42.6 | 4179 |
| Text | 75.3 [71.9-78.6] a1.2 w23.5 | 79.5 [77.0-82.3] a0.7 w19.8 | 80.5 [78.2-82.7] a0.4 w19.1 | 82.3 [79.8-84.5] a0.5 w17.2 | 74.0 [71.1-76.7] a0.3 w25.7 | 4852 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition x doc_type · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Each question carries exactly one doc_type, so unlike the evidence-source table the rows within a block are disjoint and the bolded All doc_types row closing it is their sum._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | Locating | 6.8 (44) | 9.0 (58) | 43.2 (280) | 41.0 (266) | 648 |
| TL->TLV | Reasoning | 12.5 (42) | 6.5 (22) | 60.8 (205) | 20.2 (68) | 337 |
| TL->TLV | Understanding | 8.5 (101) | 2.8 (33) | 74.9 (886) | 13.8 (163) | 1183 |
| TL->TLV | **All doc_types** | 8.6 (187) | 5.2 (113) | 63.2 (1371) | 22.9 (497) | 2168 |
| T->TL | Locating | 14.3 (95) | 6.8 (45) | 37.3 (248) | 41.7 (277) | 665 |
| T->TL | Reasoning | 10.0 (35) | 9.4 (33) | 57.5 (202) | 23.1 (81) | 351 |
| T->TL | Understanding | 10.1 (122) | 7.3 (88) | 67.0 (808) | 15.6 (188) | 1206 |
| T->TL | **All doc_types** | 11.3 (252) | 7.5 (166) | 56.6 (1258) | 24.6 (546) | 2222 |
| T->TLV | Locating | 14.4 (93) | 8.0 (52) | 35.6 (230) | 42.0 (271) | 646 |
| T->TLV | Reasoning | 14.5 (49) | 7.4 (25) | 58.8 (198) | 19.3 (65) | 337 |
| T->TLV | Understanding | 13.1 (155) | 4.3 (51) | 70.3 (832) | 12.3 (145) | 1183 |
| T->TLV | **All doc_types** | 13.7 (297) | 5.9 (128) | 58.2 (1260) | 22.2 (481) | 2166 |
| T->TV | Locating | 11.1 (76) | 7.9 (54) | 35.3 (241) | 45.6 (311) | 682 |
| T->TV | Reasoning | 11.4 (42) | 6.5 (24) | 60.5 (224) | 21.6 (80) | 370 |
| T->TV | Understanding | 11.2 (137) | 4.0 (49) | 70.4 (858) | 14.3 (174) | 1218 |
| T->TV | **All doc_types** | 11.2 (255) | 5.6 (127) | 58.3 (1323) | 24.9 (565) | 2270 |
| TV->TLV | Locating | 10.1 (65) | 6.8 (44) | 40.0 (258) | 43.1 (278) | 645 |
| TV->TLV | Reasoning | 10.1 (34) | 9.2 (31) | 63.1 (212) | 17.6 (59) | 336 |
| TV->TLV | Understanding | 5.1 (60) | 3.9 (46) | 78.4 (924) | 12.6 (149) | 1179 |
| TV->TLV | **All doc_types** | 7.4 (159) | 5.6 (121) | 64.5 (1394) | 22.5 (486) | 2160 |
| n (per col) | TL->TLV: 2168, T->TL: 2222, T->TLV: 2166, T->TV: 2270, TV->TLV: 2160 | - | - | - | - | - |

## Selection

### Retrieval accuracy (summary): best-F1 operating point per method

> **view**: summary — pooled across all doc_types · **swept**: retriever x k (page P/R/F1) · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. best_k = the depth k with the highest mean F1 for that method (all doc_types)._

| retriever | modality | best_k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 2 | 0.348 | 0.467 | 0.379 | 2317 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.579 | 0.558 | 0.533 | 2317 |
| bm25 | text | 1 | 0.496 | 0.356 | 0.397 | 2317 |
| bm25\|colmodernvbert | joint | 1 | 0.571 | 0.541 | 0.523 | 2317 |
| colmodernvbert | vision | 1 | 0.647 | 0.475 | 0.527 | 2317 |
| colqwen2.5 | vision | 1 | 0.681 | 0.493 | 0.549 | 2317 |
| colqwen3 | vision | 1 | 0.733 | 0.536 | 0.595 | 2317 |
| qwen3-embedding | text | 2 | 0.356 | 0.474 | 0.388 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.611 | 0.585 | 0.560 | 2317 |
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 by method (all doc_types)

> **swept**: retriever x k (overall P/R/F1) · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. _

| retriever | modality | k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.476 | 0.334 | 0.376 | 2317 |
| bge-m3 | text | 2 | 0.348 | 0.467 | 0.379 | 2317 |
| bge-m3 | text | 3 | 0.278 | 0.542 | 0.350 | 2317 |
| bge-m3 | text | 4 | 0.231 | 0.589 | 0.316 | 2317 |
| bge-m3 | text | 5 | 0.198 | 0.623 | 0.287 | 2317 |
| bge-m3 | text | 6 | 0.174 | 0.651 | 0.262 | 2317 |
| bge-m3 | text | 7 | 0.155 | 0.673 | 0.241 | 2317 |
| bge-m3 | text | 8 | 0.140 | 0.692 | 0.224 | 2317 |
| bge-m3 | text | 9 | 0.129 | 0.710 | 0.210 | 2317 |
| bge-m3 | text | 10 | 0.119 | 0.726 | 0.198 | 2317 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.579 | 0.558 | 0.533 | 2317 |
| bge-m3\|colqwen2.5 | joint | 3 | 0.272 | 0.757 | 0.379 | 2317 |
| bge-m3\|colqwen2.5 | joint | 5 | 0.182 | 0.820 | 0.285 | 2317 |
| bm25 | text | 1 | 0.496 | 0.356 | 0.397 | 2317 |
| bm25 | text | 2 | 0.352 | 0.479 | 0.386 | 2317 |
| bm25 | text | 3 | 0.270 | 0.539 | 0.343 | 2317 |
| bm25 | text | 4 | 0.222 | 0.583 | 0.308 | 2317 |
| bm25 | text | 5 | 0.190 | 0.611 | 0.277 | 2317 |
| bm25 | text | 6 | 0.166 | 0.637 | 0.253 | 2317 |
| bm25 | text | 7 | 0.148 | 0.656 | 0.233 | 2317 |
| bm25 | text | 8 | 0.135 | 0.672 | 0.216 | 2317 |
| bm25 | text | 9 | 0.123 | 0.685 | 0.201 | 2317 |
| bm25 | text | 10 | 0.113 | 0.695 | 0.187 | 2317 |
| bm25\|colmodernvbert | joint | 1 | 0.571 | 0.541 | 0.523 | 2317 |
| bm25\|colmodernvbert | joint | 3 | 0.255 | 0.728 | 0.359 | 2317 |
| bm25\|colmodernvbert | joint | 5 | 0.169 | 0.789 | 0.267 | 2317 |
| colmodernvbert | vision | 1 | 0.647 | 0.475 | 0.527 | 2317 |
| colmodernvbert | vision | 2 | 0.440 | 0.608 | 0.487 | 2317 |
| colmodernvbert | vision | 3 | 0.335 | 0.673 | 0.427 | 2317 |
| colmodernvbert | vision | 4 | 0.275 | 0.718 | 0.379 | 2317 |
| colmodernvbert | vision | 5 | 0.232 | 0.745 | 0.339 | 2317 |
| colmodernvbert | vision | 6 | 0.203 | 0.769 | 0.307 | 2317 |
| colmodernvbert | vision | 7 | 0.179 | 0.786 | 0.280 | 2317 |
| colmodernvbert | vision | 8 | 0.162 | 0.803 | 0.259 | 2317 |
| colmodernvbert | vision | 9 | 0.148 | 0.819 | 0.241 | 2317 |
| colmodernvbert | vision | 10 | 0.136 | 0.831 | 0.225 | 2317 |
| colqwen2.5 | vision | 1 | 0.681 | 0.493 | 0.549 | 2317 |
| colqwen2.5 | vision | 2 | 0.478 | 0.652 | 0.526 | 2317 |
| colqwen2.5 | vision | 3 | 0.358 | 0.706 | 0.452 | 2317 |
| colqwen2.5 | vision | 4 | 0.292 | 0.751 | 0.401 | 2317 |
| colqwen2.5 | vision | 5 | 0.248 | 0.780 | 0.359 | 2317 |
| colqwen2.5 | vision | 6 | 0.214 | 0.800 | 0.323 | 2317 |
| colqwen2.5 | vision | 7 | 0.189 | 0.815 | 0.294 | 2317 |
| colqwen2.5 | vision | 8 | 0.170 | 0.829 | 0.271 | 2317 |
| colqwen2.5 | vision | 9 | 0.154 | 0.839 | 0.250 | 2317 |
| colqwen2.5 | vision | 10 | 0.142 | 0.852 | 0.234 | 2317 |
| colqwen3 | vision | 1 | 0.733 | 0.536 | 0.595 | 2317 |
| colqwen3 | vision | 2 | 0.508 | 0.685 | 0.555 | 2317 |
| colqwen3 | vision | 3 | 0.382 | 0.745 | 0.481 | 2317 |
| colqwen3 | vision | 4 | 0.311 | 0.788 | 0.424 | 2317 |
| colqwen3 | vision | 5 | 0.259 | 0.811 | 0.375 | 2317 |
| colqwen3 | vision | 6 | 0.225 | 0.832 | 0.338 | 2317 |
| colqwen3 | vision | 7 | 0.198 | 0.846 | 0.307 | 2317 |
| colqwen3 | vision | 8 | 0.177 | 0.858 | 0.282 | 2317 |
| colqwen3 | vision | 9 | 0.161 | 0.870 | 0.261 | 2317 |
| colqwen3 | vision | 10 | 0.148 | 0.881 | 0.244 | 2317 |
| qwen3-embedding | text | 1 | 0.489 | 0.341 | 0.385 | 2317 |
| qwen3-embedding | text | 2 | 0.356 | 0.474 | 0.388 | 2317 |
| qwen3-embedding | text | 3 | 0.288 | 0.560 | 0.363 | 2317 |
| qwen3-embedding | text | 4 | 0.239 | 0.611 | 0.329 | 2317 |
| qwen3-embedding | text | 5 | 0.206 | 0.648 | 0.299 | 2317 |
| qwen3-embedding | text | 6 | 0.182 | 0.680 | 0.276 | 2317 |
| qwen3-embedding | text | 7 | 0.164 | 0.706 | 0.255 | 2317 |
| qwen3-embedding | text | 8 | 0.148 | 0.726 | 0.237 | 2317 |
| qwen3-embedding | text | 9 | 0.135 | 0.739 | 0.220 | 2317 |
| qwen3-embedding | text | 10 | 0.125 | 0.755 | 0.207 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.611 | 0.585 | 0.560 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 3 | 0.290 | 0.781 | 0.400 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 5 | 0.192 | 0.844 | 0.299 | 2317 |
| n (per col) | - | - | - | - | - | - |

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page-set rule (gold withheld / distractors added) x ranking source x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows group on the pageset condition grammar (ranking source, gold rule, distractor count); the robustness gold-count BLOCKS come from the corpus gold-page annotation (the +k design filters questions by exact gold count and feeds ALL their gold pages, so the block is a property of the question, not the rule). Each block's d=0 baseline is the bolded oracle row above it: all gold + no distractors IS the oracle condition, loaded from the G1 cache over the same questions, so the baseline is exact and was never re-generated. Read DOWN a block for the dilution slope at constant evidence; blocks are not comparable to each other (evidence and length both differ). Sufficiency rows withhold or isolate ONE gold page by the named ranker's ordering, on the hop=multi pool, and read against the bolded multi-pool oracle row. Per-cell n is load-bearing: OOM attrition is rung-dependent._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 62.2 [58.6-65.9] (n=1200) | 62.4 [58.9-66.2] (n=1147) | 69.3 [65.8-73.0] (n=1093) | 62.0 [58.3-65.5] (n=1209) | 5824 |
| drop bottom 1 | bm25 | 46.1 [42.2-50.7] (n=1212) | 48.0 [43.8-52.6] (n=1189) | 50.3 [46.1-54.7] (n=1176) | 46.2 [42.1-50.1] (n=1209) | 4786 |
| drop bottom 1 | colqwen3 | 47.2 [43.2-51.6] (n=1212) | 50.4 [46.2-54.8] (n=1186) | 52.5 [48.2-56.7] (n=1172) | 48.9 [44.8-52.9] (n=1209) | 4779 |
| drop top 1 | bm25 | 28.5 [25.2-32.2] (n=1211) | 29.5 [26.5-32.8] (n=1181) | 29.1 [25.8-32.6] (n=1161) | 27.0 [24.0-30.2] (n=1209) | 4762 |
| drop top 1 | colqwen3 | 28.0 [24.7-31.6] (n=1211) | 26.7 [23.7-29.8] (n=1185) | 27.8 [24.5-31.3] (n=1164) | 24.9 [22.0-28.2] (n=1209) | 4769 |
| keep bottom 1 | bm25 | 25.2 [22.1-28.4] (n=1222) | 25.3 [22.2-28.5] (n=1207) | 25.2 [22.1-28.2] (n=1200) | 23.3 [20.5-26.0] (n=1222) | 4851 |
| keep bottom 1 | colqwen3 | 24.5 [21.7-27.4] (n=1222) | 23.1 [20.1-26.2] (n=1206) | 24.3 [21.6-27.2] (n=1203) | 21.1 [18.5-23.7] (n=1222) | 4853 |
| keep top 1 | bm25 | 43.8 [39.9-48.0] (n=1222) | 44.2 [39.7-48.6] (n=1216) | 47.0 [42.6-51.4] (n=1216) | 42.8 [38.8-46.8] (n=1222) | 4876 |
| keep top 1 | colqwen3 | 44.8 [40.9-49.0] (n=1222) | 47.4 [43.3-51.7] (n=1217) | 49.1 [45.1-53.6] (n=1216) | 45.4 [41.5-49.5] (n=1222) | 4877 |
| **oracle (gold 1, d=0)** | - | 65.6 [60.6-70.5] (n=1093) | 74.0 [70.7-77.0] (n=1076) | 74.7 [71.4-77.9] (n=1073) | 64.5 [61.0-68.3] (n=1093) | 5428 |
| gold 1 + 1 distractors | colqwen3 | 65.4 [60.3-70.1] (n=1087) | 72.4 [69.1-75.8] (n=1028) | 74.4 [70.8-77.9] (n=988) | 63.0 [59.4-66.6] (n=1093) | 4196 |
| gold 1 + 2 distractors | colqwen3 | 65.1 [60.1-69.5] (n=1074) | 68.7 [64.7-72.5] (n=927) | 72.0 [67.8-76.2] (n=835) | 63.9 [60.4-67.4] (n=1093) | 3929 |
| gold 1 + 3 distractors | colqwen3 | 64.5 [59.9-69.0] (n=1060) | 68.0 [63.7-71.7] (n=827) | 68.4 [63.5-73.2] (n=681) | 62.1 [58.7-65.3] (n=1093) | 3661 |
| gold 1 + 4 distractors | colqwen3 | 63.5 [58.5-67.7] (n=1040) | 68.0 [63.8-72.4] (n=719) | 72.2 [67.2-76.9] (n=507) | 62.5 [58.9-66.0] (n=1093) | 3359 |
| gold 1 + 5 distractors | colqwen3 | 64.6 [59.5-69.4] (n=1004) | 69.1 [64.4-73.6] (n=624) | 70.2 [64.6-75.4] (n=342) | 60.8 [57.2-64.4] (n=1093) | 3063 |
| **oracle (gold 2, d=0)** | - | 62.2 [58.2-66.3] (n=898) | 63.4 [59.3-67.7] (n=871) | 70.4 [66.6-74.5] (n=846) | 61.5 [57.4-65.6] (n=906) | 4417 |
| gold 2 + 1 distractors | colqwen3 | 58.7 [54.4-63.1] (n=894) | 63.0 [58.6-67.6] (n=825) | 66.2 [61.9-70.6] (n=779) | 57.9 [53.9-62.2] (n=906) | 3404 |
| gold 2 + 2 distractors | colqwen3 | 58.9 [55.0-63.2] (n=884) | 62.2 [57.4-66.5] (n=781) | 66.4 [61.8-71.0] (n=679) | 57.4 [53.1-61.8] (n=906) | 3250 |
| gold 2 + 3 distractors | colqwen3 | 58.1 [54.2-62.3] (n=867) | 63.3 [58.7-68.3] (n=716) | 70.8 [65.1-75.8] (n=579) | 57.8 [53.6-62.2] (n=906) | 3068 |
| gold 2 + 4 distractors | colqwen3 | 57.8 [53.6-62.1] (n=843) | 63.2 [58.6-68.3] (n=661) | 68.3 [63.3-73.9] (n=458) | 57.1 [52.8-61.4] (n=906) | 2868 |
| n (per col) | - | 18487 | 16695 | 15356 | 18813 | - |

### Withholding gold pages: verdict flips from the oracle page set, by evidence source

> **swept**: gold page withheld (drop best / drop worst) · **dataset**: longdocurl · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. Rung and ranker match the main text and the selection figure, so the All sources rows reproduce that figure's two flip columns exactly and these tables are its per-source breakdown. R→W is the share of oracle-correct cells the change breaks and W→R the share of oracle-wrong cells it repairs, both as percentages of that row's paired n, so the two columns are the loss and the gain of the same change and their difference is its net effect. A question citing several evidence sources appears under each, so the per-source rows OVERLAP and cannot be summed; the bolded All sources row is computed fresh over every paired cell counted once. † marks a row over fewer than 30 distinct questions._

| evidence_source | drop lowest gold R→W | drop lowest gold W→R | drop highest gold R→W | drop highest gold W→R | keep highest only R→W | keep highest only W→R | keep lowest only R→W | keep lowest only W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Figure | 22.7 | 4.4 | 44.2 | 2.8 | 26.3 | 5.6 | 48.2 | 2.4 | 251 | 245 |
| Layout | 20.1 | 2.7 | 36.5 | 1.6 | 23.4 | 2.3 | 40.7 | 1.8 | 513 | 513 |
| Others† | 0.0 | 0.0 | 25.0 | 25.0 | 0.0 | 0.0 | 25.0 | 25.0 | 4 | 4 |
| Table | 15.9 | 3.9 | 32.2 | 2.6 | 17.2 | 4.3 | 33.0 | 1.7 | 233 | 233 |
| Text | 15.8 | 4.3 | 48.1 | 2.1 | 19.3 | 3.7 | 52.3 | 2.4 | 621 | 621 |
| **All sources** | 19.6 | 3.6 | 43.2 | 2.0 | 22.2 | 3.5 | 46.5 | 1.8 | 1093 | 1093 |
| n (per col) | - | - | - | - | - | - | - | - | - | - |

### Adding distractor pages: verdict flips from the oracle page set, by evidence source

> **swept**: distractor count added to a complete gold set · **dataset**: longdocurl · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. Rung and ranker match the main text and the selection figure, so the All sources rows reproduce that figure's two flip columns exactly and these tables are its per-source breakdown. R→W is the share of oracle-correct cells the change breaks and W→R the share of oracle-wrong cells it repairs, both as percentages of that row's paired n, so the two columns are the loss and the gain of the same change and their difference is its net effect. A question citing several evidence sources appears under each, so the per-source rows OVERLAP and cannot be summed; the bolded All sources row is computed fresh over every paired cell counted once. † marks a row over fewer than 30 distinct questions._

| gold pages | evidence_source | +1 distractor R→W | +1 distractor W→R | +2 distractors R→W | +2 distractors W→R | +3 distractors R→W | +3 distractors W→R | +4 distractors R→W | +4 distractors W→R | +5 distractors R→W | +5 distractors W→R | +6 distractors R→W | +6 distractors W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 gold page | Figure | 10.6 | 9.5 | 11.2 | 7.2 | 16.4 | 8.2 | 12.7 | 10.8 | 14.1 | 7.6 | - | - | 273 | 271 |
| 1 gold page | Layout | 11.2 | 8.0 | 11.4 | 9.1 | 14.9 | 5.6 | 13.0 | 8.4 | 16.3 | 8.2 | - | - | 187 | 187 |
| 1 gold page | Others† | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | - | - | 4 | 4 |
| 1 gold page | Table | 8.9 | 9.3 | 9.0 | 8.2 | 12.6 | 8.4 | 10.7 | 12.9 | 11.3 | 11.3 | - | - | 482 | 482 |
| 1 gold page | Text | 4.8 | 7.0 | 7.4 | 6.1 | 8.0 | 5.8 | 8.6 | 5.9 | 9.0 | 6.0 | - | - | 314 | 314 |
| 1 gold page | **All sources** | 8.5 | 8.1 | 9.4 | 7.6 | 11.8 | 6.9 | 10.5 | 8.7 | 11.4 | 7.3 | - | - | 987 | 987 |
| 2-3 gold pages | Figure | 14.0 | 3.8 | 11.9 | 2.4 | 10.9 | 3.8 | 15.3 | 5.3 | - | - | - | - | 186 | 183 |
| 2-3 gold pages | Layout | 12.3 | 5.3 | 12.6 | 6.1 | 12.0 | 7.3 | 15.7 | 7.0 | - | - | - | - | 341 | 341 |
| 2-3 gold pages | Others† | 0.0 | 25.0 | 0.0 | 25.0 | 0.0 | 0.0 | 0.0 | 0.0 | - | - | - | - | 4 | 4 |
| 2-3 gold pages | Table | 10.6 | 5.0 | 11.3 | 4.7 | 8.2 | 14.8 | 11.1 | 16.7 | - | - | - | - | 161 | 161 |
| 2-3 gold pages | Text | 6.1 | 3.6 | 8.2 | 3.7 | 7.5 | 5.0 | 10.9 | 4.6 | - | - | - | - | 442 | 442 |
| 2-3 gold pages | **All sources** | 9.6 | 4.1 | 10.9 | 4.4 | 9.7 | 6.0 | 13.3 | 6.1 | - | - | - | - | 779 | 779 |
| n (per col) | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |

## Integration

### Integration: accuracy by evidence hop, per task family and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. LongDocURL has no document-domain labels. `task_tag` is the coarsest question annotation it carries (Understanding / Locating / Reasoning) and is what the doc_type column of the rebuilt tables actually holds; this table names it honestly. `question_type` below is nested inside it: every type belongs to exactly one tag, so the two are the same partition at different resolutions. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| task_tag | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Understanding | T | 74.3 [68.0-80.1] | 73.9 [69.6-78.1] | -0.4 | 1229 |
| Understanding | TL | 79.1 [75.9-82.3] | 75.1 [70.6-79.4] | -4.1 | 1207 |
| Understanding | TV | 83.5 [80.3-86.4] | 79.9 [76.7-82.9] | -3.6 | 1218 |
| Understanding | TLV | 82.9 [80.0-85.8] | 84.0 [80.4-87.5] | +1.0 | 1183 |
| Understanding | V | 74.2 [70.3-78.0] | 75.0 [71.4-78.4] | +0.9 | 1229 |
| Locating | T | 51.1 [42.5-59.8] | 37.0 [30.3-44.0] | -14.1 | 685 |
| Locating | TL | 64.6 [56.4-71.6] | 40.2 [34.0-46.6] | -24.5 | 665 |
| Locating | TV | 52.6 [44.9-59.8] | 41.2 [34.2-48.0] | -11.5 | 680 |
| Locating | TLV | 58.0 [49.6-66.3] | 42.8 [35.6-50.3] | -15.2 | 646 |
| Locating | V | 52.0 [44.5-59.3] | 39.8 [33.8-46.6] | -12.2 | 692 |
| Reasoning | T | 61.4 [52.3-70.2] | 70.6 [64.8-76.6] | +9.2 | 379 |
| Reasoning | TL | 72.5 [65.9-79.5] | 63.6 [57.1-70.6] | -8.9 | 351 |
| Reasoning | TV | 70.3 [63.2-77.6] | 73.1 [66.7-79.1] | +2.9 | 370 |
| Reasoning | TLV | 75.7 [69.1-81.7] | 71.4 [64.8-77.4] | -4.3 | 337 |
| Reasoning | V | 52.5 [43.9-60.4] | 62.3 [55.2-68.7] | +9.8 | 381 |
| **all task_tags** | **T** | **65.6 [60.6-70.5]** | **62.2 [58.6-65.9]** | **-3.4** | **2293** |
| **all task_tags** | **TL** | **74.0 [70.7-77.0]** | **62.4 [58.9-66.2]** | **-11.6** | **2223** |
| **all task_tags** | **TV** | **72.5 [68.8-76.0]** | **66.9 [63.8-70.1]** | **-5.6** | **2268** |
| **all task_tags** | **TLV** | **74.7 [71.4-77.9]** | **69.3 [65.8-73.0]** | **-5.4** | **2166** |
| **all task_tags** | **V** | **64.5 [61.0-68.3]** | **62.0 [58.3-65.5]** | **-2.5** | **2302** |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration: accuracy by evidence hop, per question type and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x question type x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **reading**: hop is shared by both corpora and question_type is LongDocURL's alone, so this pairing is what the second dataset is for · **thin rows**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. The nine question types, printed grouped by the task_tag each belongs to (Understanding: extract | Locating: extract_fig2tab, topic2title, summary2title, summary2tab | Reasoning: calculate, count, compare, summarize). This is the finest question annotation either corpus carries and it is the reason for running LongDocURL: the types differ in what evidence they need, so a rung that helps `extract_fig2tab` need not help `calculate`. The tail types are thin (summarize is 13 questions in the corpus) — read the per-row n. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| question_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| extract | T | 74.3 [68.0-80.1] | 73.9 [69.6-78.1] | -0.4 | 1229 |
| extract | TL | 79.1 [75.9-82.3] | 75.1 [70.6-79.4] | -4.1 | 1207 |
| extract | TV | 83.5 [80.3-86.4] | 79.9 [76.7-82.9] | -3.6 | 1218 |
| extract | TLV | 82.9 [80.0-85.8] | 84.0 [80.4-87.5] | +1.0 | 1183 |
| extract | V | 74.2 [70.3-78.0] | 75.0 [71.4-78.4] | +0.9 | 1229 |
| extract_fig2tab | T | 58.4 [47.5-68.8] | - | - | 231 |
| extract_fig2tab | TL | 71.6 [62.4-79.9] | - | - | 222 |
| extract_fig2tab | TV | 54.5 [44.8-63.3] | - | - | 231 |
| extract_fig2tab | TLV | 62.3 [52.5-72.2] | - | - | 220 |
| extract_fig2tab | V | 55.4 [45.8-64.6] | - | - | 231 |
| topic2title | T | 15.0 [7.5-24.6] | 33.8 [24.8-44.0] | +18.8 | 199 |
| topic2title | TL | 33.3 [21.0-46.4] | 27.2 [19.0-35.8] | -6.1 | 196 |
| topic2title | TV | 35.0 [21.2-50.0] | 35.3 [27.1-44.0] | +0.3 | 196 |
| topic2title | TLV | 36.7 [23.0-50.0] | 34.8 [26.3-43.7] | -1.8 | 192 |
| topic2title | V | 30.0 [17.9-42.2] | 31.7 [23.8-41.3] | +1.7 | 199 |
| summary2title | T | 79.2 [65.2-92.3] | 64.5 [54.3-73.5] | -14.6 | 134 |
| summary2title | TL | 87.5 [72.7-100.0] | 79.6 [70.8-87.5] | -7.9 | 132 |
| summary2title | TV | 87.5 [72.7-100.0] | 72.2 [62.4-81.3] | -15.3 | 132 |
| summary2title | TLV | 83.3 [68.0-96.0] | 75.7 [66.0-85.3] | -7.6 | 127 |
| summary2title | V | 79.2 [60.8-93.4] | 73.2 [64.2-81.6] | -6.0 | 136 |
| summary2tab | T | 25.0 [0.0-50.0] | 14.2 [6.7-22.1] | -10.8 | 121 |
| summary2tab | TL | 37.5 [14.3-57.2] | 16.8 [8.7-26.9] | -20.7 | 115 |
| summary2tab | TV | 25.0 [0.0-50.0] | 18.6 [10.4-27.2] | -6.4 | 121 |
| summary2tab | TLV | 25.0 [0.0-50.0] | 19.2 [9.7-30.0] | -5.8 | 107 |
| summary2tab | V | 37.5 [14.3-57.2] | 17.8 [10.2-26.2] | -19.7 | 126 |
| calculate | T | 58.4 [45.0-70.3] | 65.4 [51.9-80.0] | +7.0 | 141 |
| calculate | TL | 73.8 [63.7-83.5] | 53.3 [38.8-71.1] | -20.5 | 129 |
| calculate | TV | 67.4 [58.2-76.1] | 74.0 [60.0-87.5] | +6.6 | 139 |
| calculate | TLV | 76.2 [65.7-84.7] | 65.9 [51.2-80.9] | -10.3 | 125 |
| calculate | V | 46.1 [33.3-57.9] | 58.2 [41.4-73.2] | +12.1 | 144 |
| count | T | 61.5 [42.3-80.8] | 56.8 [46.7-66.3] | -4.7 | 114 |
| count | TL | 65.4 [46.2-84.6] | 53.2 [42.7-63.2] | -12.2 | 105 |
| count | TV | 73.1 [53.8-88.5] | 61.4 [50.7-71.1] | -11.6 | 109 |
| count | TLV | 72.0 [56.0-88.0] | 64.0 [52.7-74.0] | -8.0 | 100 |
| count | V | 65.4 [46.2-80.9] | 55.8 [46.3-66.0] | -9.6 | 112 |
| compare | T | 66.7 [52.8-80.0] | 88.0 [78.9-94.9] | +21.3 | 111 |
| compare | TL | 75.0 [60.6-87.9] | 80.9 [70.5-89.9] | +5.9 | 104 |
| compare | TV | 77.8 [62.9-89.5] | 83.8 [74.7-91.7] | +6.0 | 110 |
| compare | TLV | 75.0 [61.1-87.2] | 83.1 [73.1-91.2] | +8.1 | 101 |
| compare | V | 55.6 [38.2-72.2] | 69.7 [59.2-79.5] | +14.2 | 112 |
| summarize | T | 71.4 [42.9-100.0] | 100.0 [100.0-100.0] | +28.6 | 13 |
| summarize | TL | 71.4 [42.9-100.0] | 83.3 [50.0-100.0] | +11.9 | 13 |
| summarize | TV | 57.1 [28.6-85.7] | 100.0 [100.0-100.0] | +42.9 | 12 |
| summarize | TLV | 85.7 [57.1-100.0] | 75.0 [25.0-100.0] | -10.7 | 11 |
| summarize | V | 71.4 [28.6-100.0] | 100.0 [100.0-100.0] | +28.6 | 13 |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration: accuracy by evidence hop, per answer format and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x answer format x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. The expected shape of the answer (String / List / Integer / Float / None), which LongDocURL annotates and MMLongBench does not. It is a confound worth seeing: a List answer must be produced complete to be scored right, so its accuracy sits below a String one for reasons that are not about the rung. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| answer_format | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| String | T | 74.1 [68.0-79.9] | 79.8 [75.7-83.7] | +5.7 | 932 |
| String | TL | 81.2 [77.1-84.9] | 81.6 [77.6-85.5] | +0.4 | 920 |
| String | TV | 74.8 [68.7-80.4] | 82.7 [79.1-86.2] | +7.9 | 923 |
| String | TLV | 78.2 [72.9-83.0] | 84.6 [81.0-88.1] | +6.4 | 904 |
| String | V | 72.1 [66.7-77.6] | 79.1 [75.5-82.8] | +7.0 | 934 |
| List | T | 48.2 [40.4-56.3] | 39.9 [35.0-45.5] | -8.4 | 748 |
| List | TL | 58.1 [51.3-64.8] | 40.1 [34.9-45.9] | -18.0 | 722 |
| List | TV | 60.2 [53.6-66.9] | 45.5 [40.6-50.5] | -14.7 | 740 |
| List | TLV | 58.9 [52.0-66.2] | 50.2 [44.1-55.9] | -8.6 | 701 |
| List | V | 51.5 [44.3-58.4] | 42.1 [36.9-48.1] | -9.3 | 753 |
| Integer | T | 66.4 [58.7-74.0] | 65.2 [58.6-72.1] | -1.2 | 427 |
| Integer | TL | 76.5 [70.3-81.9] | 63.0 [55.5-70.4] | -13.5 | 402 |
| Integer | TV | 79.6 [75.0-84.3] | 70.6 [63.8-77.0] | -9.0 | 420 |
| Integer | TLV | 82.3 [76.5-87.4] | 71.4 [63.9-78.3] | -10.8 | 388 |
| Integer | V | 64.6 [57.3-72.5] | 64.7 [57.7-71.2] | +0.1 | 427 |
| Float | T | 77.7 [66.9-86.7] | 67.7 [55.4-79.6] | -9.9 | 183 |
| Float | TL | 83.1 [76.2-89.2] | 60.3 [45.3-72.6] | -22.7 | 176 |
| Float | TV | 81.8 [74.2-88.7] | 78.7 [68.3-87.7] | -3.1 | 182 |
| Float | TLV | 87.3 [80.8-92.6] | 69.2 [58.0-80.5] | -18.1 | 170 |
| Float | V | 70.2 [59.1-78.8] | 57.8 [46.4-67.9] | -12.4 | 185 |
| None | T | - | 100.0 [100.0-100.0] | - | 3 |
| None | TL | - | 100.0 [100.0-100.0] | - | 3 |
| None | TV | - | 100.0 [100.0-100.0] | - | 3 |
| None | TLV | - | 100.0 [100.0-100.0] | - | 3 |
| None | V | - | 66.7 [33.3-100.0] | - | 3 |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. _

| evidence pages | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 65.6 [60.6-70.5] a1.0 w33.4 (n=1093) | 74.0 [70.7-77.0] a1.3 w24.7 (n=1076) | 72.5 [68.8-76.0] a0.2 w27.4 (n=1093) | 74.7 [71.4-77.9] a0.2 w25.2 (n=1073) | 64.5 [61.0-68.3] a0.2 w35.3 (n=1093) | 5428 |
| 2 | 62.2 [58.2-66.3] a1.0 w36.7 (n=898) | 63.4 [59.3-67.7] a0.5 w36.2 (n=871) | 67.6 [63.8-71.4] a0.3 w32.0 (n=896) | 70.4 [66.6-74.5] a0.7 w28.8 (n=846) | 61.5 [57.4-65.6] a0.4 w38.1 (n=906) | 4417 |
| 3 | 65.9 [58.0-73.4] a1.1 w33.0 (n=182) | 63.8 [55.4-72.0] a0.6 w35.6 (n=174) | 68.0 [60.2-75.8] a0.0 w32.0 (n=178) | 69.1 [61.5-76.7] a0.0 w30.9 (n=162) | 66.7 [59.5-74.1] a0.0 w33.3 (n=183) | 879 |
| 4-5 | 53.9 [41.9-65.9] a0.0 w46.1 (n=89) | 53.2 [43.1-63.4] a0.0 w46.8 (n=79) | 57.0 [45.8-67.9] a0.0 w43.0 (n=86) | 59.7 [48.5-71.0] a0.0 w40.3 (n=72) | 60.7 [48.7-71.1] a0.0 w39.3 (n=89) | 415 |
| 6+ | 61.3 [38.5-78.4] a3.2 w35.5 (n=31) | 47.8 [21.1-73.9] a0.0 w52.2 (n=23) | 66.7 [41.7-86.7] a0.0 w33.3 (n=15) | 46.2 [22.2-66.7] a0.0 w53.8 (n=13) | 51.6 [37.5-64.5] a0.0 w48.4 (n=31) | 113 |
| n (per col) | 2293 | 2223 | 2268 | 2166 | 2302 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason.  `1 → 6+` is the accuracy of the last bucket minus the first, in points; negative means the rung degrades as evidence spreads. Read it against the per-cell n: TLV OOMs hardest at high page counts, so its tail buckets are a handful of surviving questions and its slope is not comparable to the text rungs'._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 65.6 [60.6-70.5] (n=1093) | 62.2 [58.2-66.3] (n=898) | 65.9 [58.0-73.4] (n=182) | 53.9 [41.9-65.9] (n=89) | 61.3 [38.5-78.4] (n=31) | -4.3 | 2293 |
| TL | 74.0 [70.7-77.0] (n=1076) | 63.4 [59.3-67.7] (n=871) | 63.8 [55.4-72.0] (n=174) | 53.2 [43.1-63.4] (n=79) | 47.8 [21.1-73.9] (n=23) | -26.2 | 2223 |
| TV | 72.5 [68.8-76.0] (n=1093) | 67.6 [63.8-71.4] (n=896) | 68.0 [60.2-75.8] (n=178) | 57.0 [45.8-67.9] (n=86) | 66.7 [41.7-86.7] (n=15) | -5.8 | 2268 |
| TLV | 74.7 [71.4-77.9] (n=1073) | 70.4 [66.6-74.5] (n=846) | 69.1 [61.5-76.7] (n=162) | 59.7 [48.5-71.0] (n=72) | 46.2 [22.2-66.7] (n=13) | -28.5 | 2166 |
| V | 64.5 [61.0-68.3] (n=1093) | 61.5 [57.4-65.6] (n=906) | 66.7 [59.5-74.1] (n=183) | 60.7 [48.7-71.1] (n=89) | 51.6 [37.5-64.5] (n=31) | -12.9 | 2302 |
| n (per col) | 5428 | 4417 | 879 | 415 | 113 | - | - |

## Deployment

### Mined: OOM rate by rung, resolution, and pages-fed

> **swept**: rung x pages fed · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. rate = oom cells / all cells in the group, over the 16 GB V100 runs._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
| T | med | 1 | 0.0 | 0 | 1095 |
| T | med | 2-5 | 0.8 | 9 | 1178 |
| T | med | 6-10 | 10.3 | 3 | 29 |
| T | med | 11-20 | 66.7 | 6 | 9 |
| T | med | 21+ | 66.7 | 4 | 6 |
| TL | med | 1 | 1.6 | 17 | 1095 |
| TL | med | 2-5 | 4.6 | 54 | 1178 |
| TL | med | 6-10 | 34.5 | 10 | 29 |
| TL | med | 11-20 | 77.8 | 7 | 9 |
| TL | med | 21+ | 66.7 | 4 | 6 |
| TV | med | 1 | 0.0 | 0 | 1095 |
| TV | med | 2-5 | 1.5 | 18 | 1178 |
| TV | med | 6-10 | 48.3 | 14 | 29 |
| TV | med | 11-20 | 100.0 | 9 | 9 |
| TV | med | 21+ | 100.0 | 6 | 6 |
| TLV | med | 1 | 1.7 | 19 | 1095 |
| TLV | med | 2-5 | 8.3 | 98 | 1178 |
| TLV | med | 6-10 | 55.2 | 16 | 29 |
| TLV | med | 11-20 | 100.0 | 9 | 9 |
| TLV | med | 21+ | 100.0 | 6 | 6 |
| V | med | 1 | 0.0 | 0 | 1095 |
| V | med | 2-5 | 0.0 | 0 | 1178 |
| V | med | 6-10 | 0.0 | 0 | 29 |
| V | med | 11-20 | 77.8 | 7 | 9 |
| V | med | 21+ | 100.0 | 6 | 6 |
| n (per col) | - | - | - | - | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. `prefill_ms` and `input_tokens` are the INPUT-bound cost, set by the representation. `decode_ms` and `output_tokens` are the OUTPUT-bound cost, set by the prompt and the decode budget, not by the rung: a rung appears to decode more only because a longer input tends to draw a longer answer. Read the two halves separately; their sum is not the end-to-end latency, which also carries scheduling and detokenisation. ⚠ These rows come from the prompt_mode=none run, which carries NO instruction at all (`config.PROMPT_MODES['none']` is the empty string), so the model rambles and `decode_ms` here is an upper bound, not a deployment figure. The per-prompt-mode decode table gives the instructed cost, on different hardware._

| doc_type | rung | prefill_ms | input_tokens | decode_ms | output_tokens | n |
| --- | --- | --- | --- | --- | --- | --- |
| Locating | T | 1779 | 1037 | 1843 | 48 | 695 |
| Locating | TL | 2969 | 1664 | 2099 | 49 | 695 |
| Locating | TV | 27398 | 4138 | 1608 | 38 | 695 |
| Locating | TLV | 26957 | 4460 | 2059 | 44 | 695 |
| Locating | V | 26934 | 3342 | 1146 | 32 | 695 |
| Reasoning | T | 1885 | 1056 | 5941 | 145 | 384 |
| Reasoning | TL | 2901 | 1588 | 5968 | 132 | 384 |
| Reasoning | TV | 28848 | 4262 | 6920 | 152 | 384 |
| Reasoning | TLV | 26241 | 4295 | 6442 | 131 | 384 |
| Reasoning | V | 30094 | 3717 | 6484 | 165 | 384 |
| Understanding | T | 1529 | 872 | 4425 | 113 | 1238 |
| Understanding | TL | 2285 | 1278 | 4725 | 112 | 1238 |
| Understanding | TV | 26040 | 3834 | 4984 | 114 | 1238 |
| Understanding | TLV | 25737 | 4051 | 5000 | 108 | 1238 |
| Understanding | V | 25340 | 3128 | 4251 | 112 | 1238 |
| n (per col) | - | - | - | - | - | - |
