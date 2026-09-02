# Tables

The same tables as `all_tables.md`, condensed: verbose columns dropped, large cross-tabs cut to their own pooled rows, confidence intervals removed. Documents run 51-149 pages (mean 89), roughly twice MMLongBench's. **This report is still filling in**: generation and judging are both in flight, so read the levels as direction and check each n.

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Headline: cost-ordered ladder accuracy by task family (oracle pages)

> **swept**: representation ladder T/TL/TV/TLV/V

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| task_tag | T | TL | TV | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Understanding | 74.1 a1.3 w24.6 | 77.1 a1.2 w21.7 | 81.7 a0.2 w18.1 | 83.4 a0.5 w16.1 | 74.6 a0.4 w25.0 | TV | 6066 |
| Locating | 43.5 a0.3 w56.2 | 51.6 a0.4 w48.0 | 46.5 a0.0 w53.5 | 50.0 a0.0 w50.0 | 45.4 a0.0 w54.6 | T | 3378 |
| Reasoning | 66.8 a1.3 w31.9 | 67.5 a0.6 w31.9 | 71.9 a0.5 w27.6 | 73.3 a0.6 w26.1 | 58.3 a0.3 w41.5 | T | 1818 |
| **all doc_types** | **63.7 a1.0 w35.3** | **68.0 a0.9 w31.2** | **69.5 a0.2 w30.3** | **71.9 a0.4 w27.8** | **63.1 a0.3 w36.6** | **TL** | **11262** |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - | - |

### Question type: ladder accuracy by LongDocURL question type (oracle pages)

> **swept**: question type (9 classes, nested inside task_tag) x rung · **grouping**: LongDocURL question_type, joined from the corpus: the result row does not carry it · **thin rows**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| question_type | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| extract | 74.1 a1.3 w24.6 | 77.1 a1.2 w21.7 | 81.7 a0.2 w18.1 | 83.4 a0.5 w16.1 | 74.6 a0.4 w25.0 | 6066 |
| extract_fig2tab | 58.4 a0.0 w41.6 | 71.6 a1.4 w27.0 | 54.5 a0.0 w45.5 | 62.3 a0.0 w37.7 | 55.4 a0.0 w44.6 | 1135 |
| topic2title | 27.9 a0.0 w72.1 | 28.8 a0.0 w71.2 | 34.8 a0.0 w65.2 | 35.1 a0.0 w64.9 | 30.8 a0.0 w69.2 | 992 |
| summary2title | 67.2 a0.7 w32.1 | 81.1 a0.0 w18.9 | 75.0 a0.0 w25.0 | 77.2 a0.0 w22.8 | 74.3 a0.0 w25.7 | 661 |
| summary2tab | 14.9 a0.8 w84.3 | 18.3 a0.0 w81.7 | 19.0 a0.0 w81.0 | 19.6 a0.0 w80.4 | 19.0 a0.0 w81.0 | 590 |
| calculate | 61.0 a2.8 w36.2 | 66.7 a0.8 w32.6 | 69.8 a0.7 w29.5 | 72.8 a0.0 w27.2 | 50.7 a0.0 w49.3 | 678 |
| count | 57.9 a0.9 w41.2 | 56.2 a1.0 w42.9 | 64.2 a0.0 w35.8 | 66.0 a1.0 w33.0 | 58.0 a0.0 w42.0 | 540 |
| compare | 81.1 a0.0 w18.9 | 78.8 a0.0 w21.2 | 81.8 a0.9 w17.3 | 80.2 a1.0 w18.8 | 65.2 a0.9 w33.9 | 538 |
| summarize | 84.6 a0.0 w15.4 | 76.9 a0.0 w23.1 | 75.0 a0.0 w25.0 | 81.8 a0.0 w18.2 | 84.6 a0.0 w15.4 | 62 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Answer format: ladder accuracy by expected answer shape (oracle pages)

> **swept**: expected answer format (String / List / Integer / Float / None) x rung · **grouping**: LongDocURL answer_format, joined from the corpus · **reading**: a confound, not a lever: a List answer must be produced complete to score right

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| answer_format | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| String | 77.1 a0.8 w22.1 | 81.4 a0.9 w17.7 | 79.0 a0.1 w20.9 | 81.5 a0.1 w18.4 | 75.8 a0.2 w24.0 | 4613 |
| List | 43.2 a0.8 w56.0 | 47.5 a0.4 w52.1 | 51.5 a0.0 w48.5 | 53.8 a0.0 w46.2 | 45.8 a0.3 w53.9 | 3674 |
| Integer | 65.8 a1.6 w32.6 | 70.4 a1.7 w27.9 | 75.5 a0.5 w24.0 | 77.6 a1.3 w21.1 | 64.6 a0.5 w34.9 | 2064 |
| Float | 74.3 a1.6 w24.0 | 75.6 a0.6 w23.9 | 80.8 a1.1 w18.1 | 81.8 a1.2 w17.1 | 65.9 a0.0 w34.1 | 896 |
| None | 100.0 a0.0 w0.0 | 100.0 a0.0 w0.0 | 100.0 a0.0 w0.0 | 100.0 a0.0 w0.0 | 66.7 a0.0 w33.3 | 15 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source x rung · **blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| Figure | 62.5 a1.4 w36.1 | 65.7 a1.5 w32.8 | 67.9 a0.2 w31.9 | 73.4 a0.6 w26.0 | 65.2 a0.2 w34.7 | 2746 |
| Layout | 48.7 a0.5 w50.8 | 52.4 a0.3 w47.3 | 56.4 a0.3 w43.4 | 56.3 a0.4 w43.2 | 52.2 a0.4 w47.4 | 3725 |
| Others | 100.0 a0.0 w0.0 | 100.0 a0.0 w0.0 | 100.0 a0.0 w0.0 | 87.5 a0.0 w12.5 | 75.0 a0.0 w25.0 | 40 |
| Table | 61.2 a0.9 w37.9 | 69.5 a1.1 w29.3 | 64.6 a0.0 w35.4 | 68.2 a0.3 w31.6 | 57.3 a0.1 w42.6 | 4179 |
| Text | 75.3 a1.2 w23.5 | 79.5 a0.7 w19.8 | 80.5 a0.4 w19.1 | 82.3 a0.5 w17.2 | 74.0 a0.3 w25.7 | 4852 |
| n (per col) | 2295 | 2225 | 2270 | 2168 | 2304 | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition x doc_type · **pairing**: within-question, both rungs status==ok

_LongDocURL. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%)); confidence intervals removed. The full table is in `all_tables.md`._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | paired n |
| --- | --- | --- | --- | --- |
| TL->TLV | Locating | 6.8 (44) | 9.0 (58) | 648 |
| TL->TLV | Reasoning | 12.5 (42) | 6.5 (22) | 337 |
| TL->TLV | Understanding | 8.5 (101) | 2.8 (33) | 1183 |
| TL->TLV | **All doc_types** | 8.6 (187) | 5.2 (113) | 2168 |
| T->TL | Locating | 14.3 (95) | 6.8 (45) | 665 |
| T->TL | Reasoning | 10.0 (35) | 9.4 (33) | 351 |
| T->TL | Understanding | 10.1 (122) | 7.3 (88) | 1206 |
| T->TL | **All doc_types** | 11.3 (252) | 7.5 (166) | 2222 |
| T->TLV | Locating | 14.4 (93) | 8.0 (52) | 646 |
| T->TLV | Reasoning | 14.5 (49) | 7.4 (25) | 337 |
| T->TLV | Understanding | 13.1 (155) | 4.3 (51) | 1183 |
| T->TLV | **All doc_types** | 13.7 (297) | 5.9 (128) | 2166 |
| T->TV | Locating | 11.1 (76) | 7.9 (54) | 682 |
| T->TV | Reasoning | 11.4 (42) | 6.5 (24) | 370 |
| T->TV | Understanding | 11.2 (137) | 4.0 (49) | 1218 |
| T->TV | **All doc_types** | 11.2 (255) | 5.6 (127) | 2270 |
| TV->TLV | Locating | 10.1 (65) | 6.8 (44) | 645 |
| TV->TLV | Reasoning | 10.1 (34) | 9.2 (31) | 336 |
| TV->TLV | Understanding | 5.1 (60) | 3.9 (46) | 1179 |
| TV->TLV | **All doc_types** | 7.4 (159) | 5.6 (121) | 2160 |
| n (per col) | TL->TLV: 2168, T->TL: 2222, T->TLV: 2166, T->TV: 2270, TV->TLV: 2160 | - | - | - |

## Selection

### Retrieval accuracy (summary): best-F1 operating point per method

> **view**: summary — pooled across all doc_types · **swept**: retriever x k (page P/R/F1)

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: retriever x k (overall P/R/F1)

_LongDocURL. SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| retriever | modality | k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.476 | 0.334 | 0.376 | 2317 |
| bge-m3 | text | 5 | 0.198 | 0.623 | 0.287 | 2317 |
| bge-m3 | text | 10 | 0.119 | 0.726 | 0.198 | 2317 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.579 | 0.558 | 0.533 | 2317 |
| bge-m3\|colqwen2.5 | joint | 5 | 0.182 | 0.820 | 0.285 | 2317 |
| bm25 | text | 1 | 0.496 | 0.356 | 0.397 | 2317 |
| bm25 | text | 5 | 0.190 | 0.611 | 0.277 | 2317 |
| bm25 | text | 10 | 0.113 | 0.695 | 0.187 | 2317 |
| bm25\|colmodernvbert | joint | 1 | 0.571 | 0.541 | 0.523 | 2317 |
| bm25\|colmodernvbert | joint | 5 | 0.169 | 0.789 | 0.267 | 2317 |
| colmodernvbert | vision | 1 | 0.647 | 0.475 | 0.527 | 2317 |
| colmodernvbert | vision | 5 | 0.232 | 0.745 | 0.339 | 2317 |
| colmodernvbert | vision | 10 | 0.136 | 0.831 | 0.225 | 2317 |
| colqwen2.5 | vision | 1 | 0.681 | 0.493 | 0.549 | 2317 |
| colqwen2.5 | vision | 5 | 0.248 | 0.780 | 0.359 | 2317 |
| colqwen2.5 | vision | 10 | 0.142 | 0.852 | 0.234 | 2317 |
| colqwen3 | vision | 1 | 0.733 | 0.536 | 0.595 | 2317 |
| colqwen3 | vision | 5 | 0.259 | 0.811 | 0.375 | 2317 |
| colqwen3 | vision | 10 | 0.148 | 0.881 | 0.244 | 2317 |
| qwen3-embedding | text | 1 | 0.489 | 0.341 | 0.385 | 2317 |
| qwen3-embedding | text | 5 | 0.206 | 0.648 | 0.299 | 2317 |
| qwen3-embedding | text | 10 | 0.125 | 0.755 | 0.207 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.611 | 0.585 | 0.560 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 5 | 0.192 | 0.844 | 0.299 | 2317 |
| n (per col) | - | - | - | - | - | - |

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page-set rule (gold withheld / distractors added) x ranking source x rung · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 62.2 (n=1200) | 62.4 (n=1147) | 69.3 (n=1093) | 62.0 (n=1209) | 5824 |
| drop bottom 1 | colqwen3 | 47.2 (n=1212) | 50.4 (n=1186) | 52.5 (n=1172) | 48.9 (n=1209) | 4779 |
| drop top 1 | colqwen3 | 28.0 (n=1211) | 26.7 (n=1185) | 27.8 (n=1164) | 24.9 (n=1209) | 4769 |
| keep bottom 1 | colqwen3 | 24.5 (n=1222) | 23.1 (n=1206) | 24.3 (n=1203) | 21.1 (n=1222) | 4853 |
| keep top 1 | colqwen3 | 44.8 (n=1222) | 47.4 (n=1217) | 49.1 (n=1216) | 45.4 (n=1222) | 4877 |
| **oracle (gold 1, d=0)** | - | 65.6 (n=1093) | 74.0 (n=1076) | 74.7 (n=1073) | 64.5 (n=1093) | 5428 |
| gold 1 + 1 distractors | colqwen3 | 65.4 (n=1087) | 72.4 (n=1028) | 74.4 (n=988) | 63.0 (n=1093) | 4196 |
| gold 1 + 2 distractors | colqwen3 | 65.1 (n=1074) | 68.7 (n=927) | 72.0 (n=835) | 63.9 (n=1093) | 3929 |
| gold 1 + 3 distractors | colqwen3 | 64.5 (n=1060) | 68.0 (n=827) | 68.4 (n=681) | 62.1 (n=1093) | 3661 |
| gold 1 + 4 distractors | colqwen3 | 63.5 (n=1040) | 68.0 (n=719) | 72.2 (n=507) | 62.5 (n=1093) | 3359 |
| gold 1 + 5 distractors | colqwen3 | 64.6 (n=1004) | 69.1 (n=624) | 70.2 (n=342) | 60.8 (n=1093) | 3063 |
| **oracle (gold 2, d=0)** | - | 62.2 (n=898) | 63.4 (n=871) | 70.4 (n=846) | 61.5 (n=906) | 4417 |
| gold 2 + 1 distractors | colqwen3 | 58.7 (n=894) | 63.0 (n=825) | 66.2 (n=779) | 57.9 (n=906) | 3404 |
| gold 2 + 2 distractors | colqwen3 | 58.9 (n=884) | 62.2 (n=781) | 66.4 (n=679) | 57.4 (n=906) | 3250 |
| gold 2 + 3 distractors | colqwen3 | 58.1 (n=867) | 63.3 (n=716) | 70.8 (n=579) | 57.8 (n=906) | 3068 |
| gold 2 + 4 distractors | colqwen3 | 57.8 (n=843) | 63.2 (n=661) | 68.3 (n=458) | 57.1 (n=906) | 2868 |
| n (per col) | - | 18487 | 16695 | 15356 | 18813 | - |

### Withholding gold pages: verdict flips from the oracle page set, by evidence source

> **swept**: gold page withheld (drop best / drop worst) · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: distractor count added to a complete gold set · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: gold evidence-page count (single vs multi) x rung · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| task_tag | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Understanding | T | 74.3 | 73.9 | -0.4 | 1229 |
| Understanding | TL | 79.1 | 75.1 | -4.1 | 1207 |
| Understanding | TV | 83.5 | 79.9 | -3.6 | 1218 |
| Understanding | TLV | 82.9 | 84.0 | +1.0 | 1183 |
| Understanding | V | 74.2 | 75.0 | +0.9 | 1229 |
| Locating | T | 51.1 | 37.0 | -14.1 | 685 |
| Locating | TL | 64.6 | 40.2 | -24.5 | 665 |
| Locating | TV | 52.6 | 41.2 | -11.5 | 680 |
| Locating | TLV | 58.0 | 42.8 | -15.2 | 646 |
| Locating | V | 52.0 | 39.8 | -12.2 | 692 |
| Reasoning | T | 61.4 | 70.6 | +9.2 | 379 |
| Reasoning | TL | 72.5 | 63.6 | -8.9 | 351 |
| Reasoning | TV | 70.3 | 73.1 | +2.9 | 370 |
| Reasoning | TLV | 75.7 | 71.4 | -4.3 | 337 |
| Reasoning | V | 52.5 | 62.3 | +9.8 | 381 |
| **all task_tags** | **T** | **65.6** | **62.2** | **-3.4** | **2293** |
| **all task_tags** | **TL** | **74.0** | **62.4** | **-11.6** | **2223** |
| **all task_tags** | **TV** | **72.5** | **66.9** | **-5.6** | **2268** |
| **all task_tags** | **TLV** | **74.7** | **69.3** | **-5.4** | **2166** |
| **all task_tags** | **V** | **64.5** | **62.0** | **-2.5** | **2302** |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration: accuracy by evidence hop, per question type and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x question type x rung · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **reading**: hop is shared by both corpora and question_type is LongDocURL's alone, so this pairing is what the second dataset is for · **thin rows**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| question_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| extract | T | 74.3 | 73.9 | -0.4 | 1229 |
| extract | TL | 79.1 | 75.1 | -4.1 | 1207 |
| extract | TV | 83.5 | 79.9 | -3.6 | 1218 |
| extract | TLV | 82.9 | 84.0 | +1.0 | 1183 |
| extract | V | 74.2 | 75.0 | +0.9 | 1229 |
| extract_fig2tab | T | 58.4 | - | - | 231 |
| extract_fig2tab | TL | 71.6 | - | - | 222 |
| extract_fig2tab | TV | 54.5 | - | - | 231 |
| extract_fig2tab | TLV | 62.3 | - | - | 220 |
| extract_fig2tab | V | 55.4 | - | - | 231 |
| topic2title | T | 15.0 | 33.8 | +18.8 | 199 |
| topic2title | TL | 33.3 | 27.2 | -6.1 | 196 |
| topic2title | TV | 35.0 | 35.3 | +0.3 | 196 |
| topic2title | TLV | 36.7 | 34.8 | -1.8 | 192 |
| topic2title | V | 30.0 | 31.7 | +1.7 | 199 |
| summary2title | T | 79.2 | 64.5 | -14.6 | 134 |
| summary2title | TL | 87.5 | 79.6 | -7.9 | 132 |
| summary2title | TV | 87.5 | 72.2 | -15.3 | 132 |
| summary2title | TLV | 83.3 | 75.7 | -7.6 | 127 |
| summary2title | V | 79.2 | 73.2 | -6.0 | 136 |
| summary2tab | T | 25.0 | 14.2 | -10.8 | 121 |
| summary2tab | TL | 37.5 | 16.8 | -20.7 | 115 |
| summary2tab | TV | 25.0 | 18.6 | -6.4 | 121 |
| summary2tab | TLV | 25.0 | 19.2 | -5.8 | 107 |
| summary2tab | V | 37.5 | 17.8 | -19.7 | 126 |
| calculate | T | 58.4 | 65.4 | +7.0 | 141 |
| calculate | TL | 73.8 | 53.3 | -20.5 | 129 |
| calculate | TV | 67.4 | 74.0 | +6.6 | 139 |
| calculate | TLV | 76.2 | 65.9 | -10.3 | 125 |
| calculate | V | 46.1 | 58.2 | +12.1 | 144 |
| count | T | 61.5 | 56.8 | -4.7 | 114 |
| count | TL | 65.4 | 53.2 | -12.2 | 105 |
| count | TV | 73.1 | 61.4 | -11.6 | 109 |
| count | TLV | 72.0 | 64.0 | -8.0 | 100 |
| count | V | 65.4 | 55.8 | -9.6 | 112 |
| compare | T | 66.7 | 88.0 | +21.3 | 111 |
| compare | TL | 75.0 | 80.9 | +5.9 | 104 |
| compare | TV | 77.8 | 83.8 | +6.0 | 110 |
| compare | TLV | 75.0 | 83.1 | +8.1 | 101 |
| compare | V | 55.6 | 69.7 | +14.2 | 112 |
| summarize | T | 71.4 | 100.0 | +28.6 | 13 |
| summarize | TL | 71.4 | 83.3 | +11.9 | 13 |
| summarize | TV | 57.1 | 100.0 | +42.9 | 12 |
| summarize | TLV | 85.7 | 75.0 | -10.7 | 11 |
| summarize | V | 71.4 | 100.0 | +28.6 | 13 |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration: accuracy by evidence hop, per answer format and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x answer format x rung · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| answer_format | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| String | T | 74.1 | 79.8 | +5.7 | 932 |
| String | TL | 81.2 | 81.6 | +0.4 | 920 |
| String | TV | 74.8 | 82.7 | +7.9 | 923 |
| String | TLV | 78.2 | 84.6 | +6.4 | 904 |
| String | V | 72.1 | 79.1 | +7.0 | 934 |
| List | T | 48.2 | 39.9 | -8.4 | 748 |
| List | TL | 58.1 | 40.1 | -18.0 | 722 |
| List | TV | 60.2 | 45.5 | -14.7 | 740 |
| List | TLV | 58.9 | 50.2 | -8.6 | 701 |
| List | V | 51.5 | 42.1 | -9.3 | 753 |
| Integer | T | 66.4 | 65.2 | -1.2 | 427 |
| Integer | TL | 76.5 | 63.0 | -13.5 | 402 |
| Integer | TV | 79.6 | 70.6 | -9.0 | 420 |
| Integer | TLV | 82.3 | 71.4 | -10.8 | 388 |
| Integer | V | 64.6 | 64.7 | +0.1 | 427 |
| Float | T | 77.7 | 67.7 | -9.9 | 183 |
| Float | TL | 83.1 | 60.3 | -22.7 | 176 |
| Float | TV | 81.8 | 78.7 | -3.1 | 182 |
| Float | TLV | 87.3 | 69.2 | -18.1 | 170 |
| Float | V | 70.2 | 57.8 | -12.4 | 185 |
| None | T | - | 100.0 | - | 3 |
| None | TL | - | 100.0 | - | 3 |
| None | TV | - | 100.0 | - | 3 |
| None | TLV | - | 100.0 | - | 3 |
| None | V | - | 66.7 | - | 3 |
| n (per col) | - | 5428 | 5824 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: gold evidence-page bucket x rung · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence pages | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 65.6 a1.0 w33.4 (n=1093) | 74.0 a1.3 w24.7 (n=1076) | 72.5 a0.2 w27.4 (n=1093) | 74.7 a0.2 w25.2 (n=1073) | 64.5 a0.2 w35.3 (n=1093) | 5428 |
| 2 | 62.2 a1.0 w36.7 (n=898) | 63.4 a0.5 w36.2 (n=871) | 67.6 a0.3 w32.0 (n=896) | 70.4 a0.7 w28.8 (n=846) | 61.5 a0.4 w38.1 (n=906) | 4417 |
| 3 | 65.9 a1.1 w33.0 (n=182) | 63.8 a0.6 w35.6 (n=174) | 68.0 a0.0 w32.0 (n=178) | 69.1 a0.0 w30.9 (n=162) | 66.7 a0.0 w33.3 (n=183) | 879 |
| 4-5 | 53.9 a0.0 w46.1 (n=89) | 53.2 a0.0 w46.8 (n=79) | 57.0 a0.0 w43.0 (n=86) | 59.7 a0.0 w40.3 (n=72) | 60.7 a0.0 w39.3 (n=89) | 415 |
| 6+ | 61.3 a3.2 w35.5 (n=31) | 47.8 a0.0 w52.2 (n=23) | 66.7 a0.0 w33.3 (n=15) | 46.2 a0.0 w53.8 (n=13) | 51.6 a0.0 w48.4 (n=31) | 113 |
| n (per col) | 2293 | 2223 | 2268 | 2166 | 2302 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: gold evidence-page bucket x rung · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 65.6 (n=1093) | 62.2 (n=898) | 65.9 (n=182) | 53.9 (n=89) | 61.3 (n=31) | -4.3 | 2293 |
| TL | 74.0 (n=1076) | 63.4 (n=871) | 63.8 (n=174) | 53.2 (n=79) | 47.8 (n=23) | -26.2 | 2223 |
| TV | 72.5 (n=1093) | 67.6 (n=896) | 68.0 (n=178) | 57.0 (n=86) | 66.7 (n=15) | -5.8 | 2268 |
| TLV | 74.7 (n=1073) | 70.4 (n=846) | 69.1 (n=162) | 59.7 (n=72) | 46.2 (n=13) | -28.5 | 2166 |
| V | 64.5 (n=1093) | 61.5 (n=906) | 66.7 (n=183) | 60.7 (n=89) | 51.6 (n=31) | -12.9 | 2302 |
| n (per col) | 5428 | 4417 | 879 | 415 | 113 | - | - |

## Deployment

### Mined: OOM rate by rung, resolution, and pages-fed

> **swept**: rung x pages fed · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
| T | med | 2-5 | 0.8 | 9 | 1178 |
| T | med | 6-10 | 10.3 | 3 | 29 |
| T | med | 11-20 | 66.7 | 6 | 9 |
| T | med | 21+ | 66.7 | 4 | 6 |
| TL | med | 1 | 1.6 | 17 | 1095 |
| TL | med | 2-5 | 4.6 | 54 | 1178 |
| TL | med | 6-10 | 34.5 | 10 | 29 |
| TL | med | 11-20 | 77.8 | 7 | 9 |
| TL | med | 21+ | 66.7 | 4 | 6 |
| TV | med | 2-5 | 1.5 | 18 | 1178 |
| TV | med | 6-10 | 48.3 | 14 | 29 |
| TV | med | 11-20 | 100.0 | 9 | 9 |
| TV | med | 21+ | 100.0 | 6 | 6 |
| TLV | med | 1 | 1.7 | 19 | 1095 |
| TLV | med | 2-5 | 8.3 | 98 | 1178 |
| TLV | med | 6-10 | 55.2 | 16 | 29 |
| TLV | med | 11-20 | 100.0 | 9 | 9 |
| TLV | med | 21+ | 100.0 | 6 | 6 |
| V | med | 11-20 | 77.8 | 7 | 9 |
| V | med | 21+ | 100.0 | 6 | 6 |
| n (per col) | - | - | - | - | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: rung

_LongDocURL. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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
