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
| **all** |  | **102770** | 99044 | 3270 | 456 | 3.2 |

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Headline: cost-ordered ladder accuracy by doc_type (oracle pages)

> **swept**: representation ladder T/TL/TV/TLV/V · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. _

| doc_type | T | TL | TV | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Locating | 4.7 [2.8-6.7] | 4.1 [2.4-6.2] | 3.2 [1.8-4.8] | 2.6 [1.3-4.3] | 3.5 [1.9-5.4] | T | 2959 |
| Reasoning | 18.8 [14.2-23.4] | 17.4 [13.0-22.5] | 19.8 [15.3-25.1] | 20.7 [15.9-26.0] | 16.1 [12.0-20.5] | T | 1678 |
| Understanding | 23.6 [20.3-27.0] | 23.2 [20.0-26.6] | 22.8 [20.0-25.7] | 23.0 [19.7-26.6] | 22.1 [19.3-24.7] | T | 5373 |
| **all doc_types** | **17.2 [15.0-19.4]** | **16.6 [14.4-19.1]** | **16.5 [14.5-18.6]** | **16.6 [14.4-18.9]** | **15.5 [13.5-17.7]** | **T** | **10010** |
| n (per col) | 2036 | 1980 | 2011 | 1943 | 2040 | - | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. _

| evidence_source | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| Figure | 21.7 [16.9-27.1] | 21.9 [17.3-27.4] | 23.2 [18.1-28.2] | 23.6 [18.8-29.3] | 20.9 [16.6-25.4] | 2463 |
| Layout | 12.2 [9.4-15.4] | 12.3 [9.2-15.6] | 11.2 [8.7-14.1] | 11.9 [8.9-15.2] | 11.2 [8.5-14.2] | 3269 |
| Others | 42.9 [0.0-87.5] | 57.1 [16.7-87.5] | 42.9 [0.0-87.5] | 28.6 [0.0-60.0] | 28.6 [0.0-44.4] | 35 |
| Table | 9.5 [7.5-11.7] | 8.3 [6.4-10.6] | 8.6 [6.7-10.6] | 7.8 [5.9-9.8] | 8.4 [6.5-10.5] | 3695 |
| Text | 27.2 [23.3-30.7] | 26.6 [22.8-30.5] | 26.2 [22.2-29.6] | 26.9 [23.0-30.8] | 23.9 [20.3-27.2] | 4327 |
| n (per col) | 2036 | 1980 | 2011 | 1943 | 2040 | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition x doc_type · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Each question carries exactly one doc_type, so unlike the evidence-source table the rows within a block are disjoint and the bolded All doc_types row closing it is their sum._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | Locating | 0.7 (4) | 1.9 (11) | 1.9 (11) | 95.5 (547) | 573 |
| TL->TLV | Reasoning | 6.0 (19) | 2.8 (9) | 14.7 (47) | 76.5 (244) | 319 |
| TL->TLV | Understanding | 3.2 (34) | 3.4 (36) | 19.8 (208) | 73.5 (773) | 1051 |
| TL->TLV | **All doc_types** | 2.9 (57) | 2.9 (56) | 13.7 (266) | 80.5 (1564) | 1943 |
| T->TL | Locating | 1.9 (11) | 2.2 (13) | 2.2 (13) | 93.7 (546) | 583 |
| T->TL | Reasoning | 2.1 (7) | 2.4 (8) | 15.3 (50) | 80.1 (262) | 327 |
| T->TL | Understanding | 3.5 (37) | 3.9 (42) | 19.8 (211) | 72.8 (778) | 1068 |
| T->TL | **All doc_types** | 2.8 (55) | 3.2 (63) | 13.9 (274) | 80.2 (1586) | 1978 |
| T->TLV | Locating | 0.9 (5) | 2.4 (14) | 1.7 (10) | 94.9 (543) | 572 |
| T->TLV | Reasoning | 6.6 (21) | 3.8 (12) | 14.1 (45) | 75.5 (241) | 319 |
| T->TLV | Understanding | 4.0 (42) | 4.9 (51) | 19.0 (200) | 72.1 (758) | 1051 |
| T->TLV | **All doc_types** | 3.5 (68) | 4.0 (77) | 13.1 (255) | 79.4 (1542) | 1942 |
| T->TV | Locating | 0.2 (1) | 1.7 (10) | 3.0 (18) | 95.1 (566) | 595 |
| T->TV | Reasoning | 3.8 (13) | 2.1 (7) | 15.9 (54) | 78.2 (265) | 339 |
| T->TV | Understanding | 3.3 (36) | 4.1 (44) | 19.5 (210) | 73.1 (787) | 1077 |
| T->TV | **All doc_types** | 2.5 (50) | 3.0 (61) | 14.0 (282) | 80.5 (1618) | 2011 |
| TV->TLV | Locating | 0.9 (5) | 1.1 (6) | 1.8 (10) | 96.3 (550) | 571 |
| TV->TLV | Reasoning | 3.8 (12) | 2.8 (9) | 16.7 (53) | 76.7 (244) | 318 |
| TV->TLV | Understanding | 3.2 (33) | 3.3 (35) | 19.9 (208) | 73.6 (771) | 1047 |
| TV->TLV | **All doc_types** | 2.6 (50) | 2.6 (50) | 14.0 (271) | 80.8 (1565) | 1936 |
| n (per col) | TL->TLV: 1943, T->TL: 1978, T->TLV: 1942, T->TV: 2011, TV->TLV: 1936 | - | - | - | - | - |

## Selection

### Retrieval accuracy (summary): best-F1 operating point per method

> **view**: summary — pooled across all doc_types · **swept**: retriever x k (page P/R/F1) · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. best_k = the depth k with the highest mean F1 for that method (all doc_types)._

| retriever | modality | best_k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 4 | 0.099 | 0.222 | 0.130 | 2317 |
| bge-m3\|colqwen2.5 | joint | 3 | 0.112 | 0.269 | 0.149 | 2317 |
| bm25 | text | 4 | 0.087 | 0.196 | 0.115 | 2317 |
| bm25\|colmodernvbert | joint | 3 | 0.097 | 0.234 | 0.130 | 2317 |
| colmodernvbert | vision | 5 | 0.096 | 0.269 | 0.134 | 2317 |
| colqwen2.5 | vision | 5 | 0.109 | 0.304 | 0.152 | 2317 |
| colqwen3 | vision | 4 | 0.122 | 0.271 | 0.159 | 2317 |
| qwen3-embedding | text | 4 | 0.103 | 0.232 | 0.136 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 3 | 0.117 | 0.276 | 0.155 | 2317 |
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 by method (all doc_types)

> **swept**: retriever x k (overall P/R/F1) · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. _

| retriever | modality | k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.104 | 0.056 | 0.069 | 2317 |
| bge-m3 | text | 2 | 0.114 | 0.129 | 0.115 | 2317 |
| bge-m3 | text | 3 | 0.108 | 0.184 | 0.128 | 2317 |
| bge-m3 | text | 4 | 0.099 | 0.222 | 0.130 | 2317 |
| bge-m3 | text | 5 | 0.091 | 0.256 | 0.128 | 2317 |
| bge-m3 | text | 6 | 0.086 | 0.295 | 0.127 | 2317 |
| bge-m3 | text | 7 | 0.081 | 0.321 | 0.123 | 2317 |
| bge-m3 | text | 8 | 0.076 | 0.343 | 0.118 | 2317 |
| bge-m3 | text | 9 | 0.072 | 0.366 | 0.115 | 2317 |
| bge-m3 | text | 10 | 0.069 | 0.390 | 0.112 | 2317 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.099 | 0.079 | 0.081 | 2317 |
| bge-m3\|colqwen2.5 | joint | 3 | 0.112 | 0.269 | 0.149 | 2317 |
| bge-m3\|colqwen2.5 | joint | 5 | 0.092 | 0.372 | 0.141 | 2317 |
| bm25 | text | 1 | 0.085 | 0.040 | 0.052 | 2317 |
| bm25 | text | 2 | 0.096 | 0.102 | 0.094 | 2317 |
| bm25 | text | 3 | 0.092 | 0.152 | 0.109 | 2317 |
| bm25 | text | 4 | 0.087 | 0.196 | 0.115 | 2317 |
| bm25 | text | 5 | 0.080 | 0.226 | 0.112 | 2317 |
| bm25 | text | 6 | 0.075 | 0.255 | 0.111 | 2317 |
| bm25 | text | 7 | 0.072 | 0.282 | 0.109 | 2317 |
| bm25 | text | 8 | 0.068 | 0.304 | 0.106 | 2317 |
| bm25 | text | 9 | 0.064 | 0.320 | 0.102 | 2317 |
| bm25 | text | 10 | 0.060 | 0.334 | 0.098 | 2317 |
| bm25\|colmodernvbert | joint | 1 | 0.085 | 0.063 | 0.067 | 2317 |
| bm25\|colmodernvbert | joint | 3 | 0.097 | 0.234 | 0.130 | 2317 |
| bm25\|colmodernvbert | joint | 5 | 0.080 | 0.337 | 0.124 | 2317 |
| colmodernvbert | vision | 1 | 0.085 | 0.041 | 0.053 | 2317 |
| colmodernvbert | vision | 2 | 0.108 | 0.116 | 0.106 | 2317 |
| colmodernvbert | vision | 3 | 0.106 | 0.177 | 0.126 | 2317 |
| colmodernvbert | vision | 4 | 0.099 | 0.222 | 0.130 | 2317 |
| colmodernvbert | vision | 5 | 0.096 | 0.269 | 0.134 | 2317 |
| colmodernvbert | vision | 6 | 0.091 | 0.305 | 0.133 | 2317 |
| colmodernvbert | vision | 7 | 0.086 | 0.339 | 0.131 | 2317 |
| colmodernvbert | vision | 8 | 0.081 | 0.367 | 0.127 | 2317 |
| colmodernvbert | vision | 9 | 0.077 | 0.391 | 0.123 | 2317 |
| colmodernvbert | vision | 10 | 0.074 | 0.417 | 0.121 | 2317 |
| colqwen2.5 | vision | 1 | 0.095 | 0.042 | 0.056 | 2317 |
| colqwen2.5 | vision | 2 | 0.124 | 0.133 | 0.121 | 2317 |
| colqwen2.5 | vision | 3 | 0.123 | 0.205 | 0.145 | 2317 |
| colqwen2.5 | vision | 4 | 0.116 | 0.257 | 0.151 | 2317 |
| colqwen2.5 | vision | 5 | 0.109 | 0.304 | 0.152 | 2317 |
| colqwen2.5 | vision | 6 | 0.102 | 0.343 | 0.149 | 2317 |
| colqwen2.5 | vision | 7 | 0.095 | 0.374 | 0.144 | 2317 |
| colqwen2.5 | vision | 8 | 0.089 | 0.399 | 0.139 | 2317 |
| colqwen2.5 | vision | 9 | 0.084 | 0.424 | 0.134 | 2317 |
| colqwen2.5 | vision | 10 | 0.080 | 0.449 | 0.130 | 2317 |
| colqwen3 | vision | 1 | 0.094 | 0.044 | 0.058 | 2317 |
| colqwen3 | vision | 2 | 0.133 | 0.143 | 0.130 | 2317 |
| colqwen3 | vision | 3 | 0.129 | 0.212 | 0.152 | 2317 |
| colqwen3 | vision | 4 | 0.122 | 0.271 | 0.159 | 2317 |
| colqwen3 | vision | 5 | 0.113 | 0.316 | 0.158 | 2317 |
| colqwen3 | vision | 6 | 0.107 | 0.360 | 0.157 | 2317 |
| colqwen3 | vision | 7 | 0.100 | 0.394 | 0.152 | 2317 |
| colqwen3 | vision | 8 | 0.093 | 0.418 | 0.145 | 2317 |
| colqwen3 | vision | 9 | 0.088 | 0.445 | 0.141 | 2317 |
| colqwen3 | vision | 10 | 0.084 | 0.472 | 0.137 | 2317 |
| qwen3-embedding | text | 1 | 0.102 | 0.054 | 0.067 | 2317 |
| qwen3-embedding | text | 2 | 0.112 | 0.123 | 0.111 | 2317 |
| qwen3-embedding | text | 3 | 0.111 | 0.186 | 0.132 | 2317 |
| qwen3-embedding | text | 4 | 0.103 | 0.232 | 0.136 | 2317 |
| qwen3-embedding | text | 5 | 0.095 | 0.270 | 0.134 | 2317 |
| qwen3-embedding | text | 6 | 0.091 | 0.307 | 0.134 | 2317 |
| qwen3-embedding | text | 7 | 0.086 | 0.338 | 0.131 | 2317 |
| qwen3-embedding | text | 8 | 0.081 | 0.367 | 0.128 | 2317 |
| qwen3-embedding | text | 9 | 0.077 | 0.392 | 0.124 | 2317 |
| qwen3-embedding | text | 10 | 0.073 | 0.412 | 0.119 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.098 | 0.073 | 0.078 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 3 | 0.117 | 0.276 | 0.155 | 2317 |
| qwen3-embedding\|colqwen3 | joint | 5 | 0.097 | 0.387 | 0.148 | 2317 |
| n (per col) | - | - | - | - | - | - |

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page-set rule (gold withheld / distractors added) x ranking source x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows group on the pageset condition grammar (ranking source, gold rule, distractor count); the robustness gold-count BLOCKS come from the corpus gold-page annotation (the +k design filters questions by exact gold count and feeds ALL their gold pages, so the block is a property of the question, not the rule). Each block's d=0 baseline is the bolded oracle row above it: all gold + no distractors IS the oracle condition, loaded from the G1 cache over the same questions, so the baseline is exact and was never re-generated. Read DOWN a block for the dilution slope at constant evidence; blocks are not comparable to each other (evidence and length both differ). Sufficiency rows withhold or isolate ONE gold page by the named ranker's ordering, on the hop=multi pool, and read against the bolded multi-pool oracle row. Per-cell n is load-bearing: OOM attrition is rung-dependent._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 25.5 [22.3-28.8] (n=1047) | 25.2 [21.6-28.8] (n=1011) | 26.0 [22.4-29.8] (n=976) | 22.3 [19.4-25.6] (n=1052) | 5109 |
| drop bottom 1 | bm25 | 22.2 [18.6-26.1] (n=585) | 22.4 [18.5-26.3] (n=572) | 23.1 [19.3-27.2] (n=562) | 20.6 [17.2-24.1] (n=583) | 2302 |
| drop bottom 1 | colqwen3 | 24.5 [20.6-28.6] (n=583) | 23.4 [19.5-27.5] (n=572) | 25.3 [21.3-29.7] (n=561) | 22.3 [18.6-25.7] (n=583) | 2299 |
| drop top 1 | bm25 | 16.9 [14.2-19.7] (n=1199) | 15.3 [12.7-18.0] (n=1177) | 14.5 [12.1-17.3] (n=1157) | 13.2 [10.9-15.6] (n=1198) | 4731 |
| drop top 1 | colqwen3 | 16.2 [13.6-18.9] (n=1198) | 13.9 [11.6-16.5] (n=1178) | 13.2 [10.9-15.9] (n=1161) | 12.3 [10.0-14.6] (n=1198) | 4735 |
| n (per col) | - | 3565 | 3499 | 3441 | 3562 | - |

### Withholding gold pages: verdict flips from the oracle page set, by evidence source

> **swept**: gold page withheld (drop best / drop worst) · **dataset**: longdocurl · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. Rung and ranker match the main text and the selection figure, so the All sources rows reproduce that figure's two flip columns exactly and these tables are its per-source breakdown. R→W is the share of oracle-correct cells the change breaks and W→R the share of oracle-wrong cells it repairs, both as percentages of that row's paired n, so the two columns are the loss and the gain of the same change and their difference is its net effect. A question citing several evidence sources appears under each, so the per-source rows OVERLAP and cannot be summed; the bolded All sources row is computed fresh over every paired cell counted once. † marks a row over fewer than 30 distinct questions._

| evidence_source | drop lowest gold R→W | drop lowest gold W→R | drop highest gold R→W | drop highest gold W→R | keep highest only R→W | keep highest only W→R | keep lowest only R→W | keep lowest only W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Figure | 3.6 | 3.6 | 22.9 | 3.1 | - | - | - | - | 223 | 217 |
| Layout | 2.8 | 2.8 | 8.4 | 0.9 | - | - | - | - | 443 | 443 |
| Others† | 0.0 | 0.0 | 66.7 | 0.0 | - | - | - | - | 3 | 3 |
| Table | 3.4 | 1.7 | 11.5 | 2.9 | - | - | - | - | 209 | 209 |
| Text | 5.1 | 2.7 | 19.2 | 3.3 | - | - | - | - | 553 | 553 |
| **All sources** | 3.5 | 2.8 | 14.7 | 2.3 | - | - | - | - | 962 | 962 |
| n (per col) | - | - | - | - | - | - | - | - | - | - |

## Integration

### Integration: accuracy by evidence hop, per doc_type and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| doc_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Locating | T | 3.5 [1.5-5.9] | 5.8 [3.1-8.8] | +2.3 | 598 |
| Locating | TL | 2.2 [0.5-4.1] | 5.8 [3.0-9.1] | +3.7 | 583 |
| Locating | TV | 1.4 [0.0-3.0] | 4.9 [2.5-7.7] | +3.5 | 593 |
| Locating | TLV | 0.7 [0.0-2.1] | 4.4 [1.8-7.2] | +3.7 | 571 |
| Locating | V | 2.4 [0.7-4.6] | 4.4 [2.2-6.8] | +2.0 | 604 |
| Reasoning | T | 4.8 [1.9-8.3] | 28.9 [22.2-35.4] | +24.0 | 346 |
| Reasoning | TL | 4.2 [1.4-7.7] | 27.7 [20.5-34.8] | +23.5 | 327 |
| Reasoning | TV | 4.1 [1.3-7.7] | 31.4 [24.1-39.1] | +27.3 | 339 |
| Reasoning | TLV | 7.0 [3.2-11.5] | 31.8 [24.1-39.4] | +24.8 | 319 |
| Reasoning | V | 4.8 [1.5-8.4] | 24.3 [17.9-30.9] | +19.4 | 347 |
| Understanding | T | 11.9 [9.1-14.8] | 35.8 [31.1-40.3] | +23.9 | 1090 |
| Understanding | TL | 11.3 [8.7-14.1] | 35.8 [31.2-40.3] | +24.5 | 1068 |
| Understanding | TV | 10.8 [8.5-13.2] | 35.7 [31.0-40.0] | +24.9 | 1077 |
| Understanding | TLV | 10.4 [8.0-13.0] | 36.7 [32.0-41.4] | +26.3 | 1051 |
| Understanding | V | 12.3 [9.5-14.9] | 32.3 [27.9-36.6] | +20.1 | 1087 |
| n (per col) | - | 4891 | 5109 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view._

| evidence pages | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 8.4 [6.6-10.4] (n=987) | 7.7 [6.0-9.6] (n=967) | 7.1 [5.6-8.8] (n=986) | 7.2 [5.5-8.9] (n=965) | 8.3 [6.6-10.3] (n=986) | 4891 |
| 2 | 25.4 [21.9-29.0] (n=776) | 24.7 [21.2-28.5] (n=756) | 25.7 [22.3-29.5] (n=773) | 25.9 [22.0-29.7] (n=745) | 22.5 [19.4-25.9] (n=783) | 3833 |
| 3 | 24.1 [18.1-30.6] (n=162) | 27.6 [19.9-35.9] (n=156) | 25.0 [18.4-31.8] (n=160) | 27.8 [20.0-35.6] (n=151) | 23.5 [16.9-30.1] (n=162) | 791 |
| 4-5 | 30.5 [18.2-42.2] (n=82) | 26.3 [15.0-39.8] (n=76) | 26.6 [15.3-39.1] (n=79) | 23.2 [11.9-35.7] (n=69) | 22.0 [12.7-31.6] (n=82) | 388 |
| 6+ | 22.2 [6.9-40.9] (n=27) | 21.7 [8.0-42.1] (n=23) | 18.2 [0.0-38.5] (n=11) | 27.3 [7.7-54.5] (n=11) | 12.0 [0.0-26.1] (n=25) | 97 |
| n (per col) | 2034 | 1978 | 2009 | 1941 | 2038 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. `1 → 6+` is the accuracy of the last bucket minus the first, in points; negative means the rung degrades as evidence spreads. Read it against the per-cell n: TLV OOMs hardest at high page counts, so its tail buckets are a handful of surviving questions and its slope is not comparable to the text rungs'._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 8.4 [6.6-10.4] (n=987) | 25.4 [21.9-29.0] (n=776) | 24.1 [18.1-30.6] (n=162) | 30.5 [18.2-42.2] (n=82) | 22.2 [6.9-40.9] (n=27) | +13.8 | 2034 |
| TL | 7.7 [6.0-9.6] (n=967) | 24.7 [21.2-28.5] (n=756) | 27.6 [19.9-35.9] (n=156) | 26.3 [15.0-39.8] (n=76) | 21.7 [8.0-42.1] (n=23) | +14.1 | 1978 |
| TV | 7.1 [5.6-8.8] (n=986) | 25.7 [22.3-29.5] (n=773) | 25.0 [18.4-31.8] (n=160) | 26.6 [15.3-39.1] (n=79) | 18.2 [0.0-38.5] (n=11) | +11.1 | 2009 |
| TLV | 7.2 [5.5-8.9] (n=965) | 25.9 [22.0-29.7] (n=745) | 27.8 [20.0-35.6] (n=151) | 23.2 [11.9-35.7] (n=69) | 27.3 [7.7-54.5] (n=11) | +20.1 | 1941 |
| V | 8.3 [6.6-10.3] (n=986) | 22.5 [19.4-25.9] (n=783) | 23.5 [16.9-30.1] (n=162) | 22.0 [12.7-31.6] (n=82) | 12.0 [0.0-26.1] (n=25) | +3.7 | 2038 |
| n (per col) | 4891 | 3833 | 791 | 388 | 97 | - | - |

## Deployment

### Mined: OOM rate by rung, resolution, and pages-fed

> **swept**: rung x pages fed · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. rate = oom cells / all cells in the group, over the 16 GB V100 runs._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
| T | med | 1 | 0.0 | 0 | 1109 |
| T | med | 2-5 | 0.9 | 10 | 1164 |
| T | med | 6-10 | 3.4 | 1 | 29 |
| T | med | 11-20 | 66.7 | 6 | 9 |
| T | med | 21+ | 66.7 | 4 | 6 |
| TL | med | 1 | 1.9 | 21 | 1109 |
| TL | med | 2-5 | 4.1 | 48 | 1164 |
| TL | med | 6-10 | 13.8 | 4 | 29 |
| TL | med | 11-20 | 77.8 | 7 | 9 |
| TL | med | 21+ | 66.7 | 4 | 6 |
| TV | med | 1 | 0.1 | 1 | 1109 |
| TV | med | 2-5 | 1.6 | 19 | 1164 |
| TV | med | 6-10 | 51.7 | 15 | 29 |
| TV | med | 11-20 | 100.0 | 9 | 9 |
| TV | med | 21+ | 100.0 | 6 | 6 |
| TLV | med | 1 | 2.1 | 23 | 1109 |
| TLV | med | 2-5 | 6.2 | 72 | 1164 |
| TLV | med | 6-10 | 55.2 | 16 | 29 |
| TLV | med | 11-20 | 100.0 | 9 | 9 |
| TLV | med | 21+ | 100.0 | 6 | 6 |
| V | med | 1 | 0.0 | 0 | 1109 |
| V | med | 2-5 | 0.0 | 0 | 1164 |
| V | med | 6-10 | 0.0 | 0 | 29 |
| V | med | 11-20 | 77.8 | 7 | 9 |
| V | med | 21+ | 100.0 | 6 | 6 |
| n (per col) | - | - | - | - | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. `prefill_ms` and `input_tokens` are the INPUT-bound cost, set by the representation. `decode_ms` and `output_tokens` are the OUTPUT-bound cost, set by the prompt and the decode budget, not by the rung: a rung appears to decode more only because a longer input tends to draw a longer answer. Read the two halves separately; their sum is not the end-to-end latency, which also carries scheduling and detokenisation. ⚠ These rows come from the prompt_mode=none run, which carries NO instruction at all (`config.PROMPT_MODES['none']` is the empty string), so the model rambles and `decode_ms` here is an upper bound, not a deployment figure. The per-prompt-mode decode table gives the instructed cost, on different hardware._

| doc_type | rung | prefill_ms | input_tokens | decode_ms | output_tokens | n |
| --- | --- | --- | --- | --- | --- | --- |
| Locating | T | 1653 | 962 | 2537 | 66 | 695 |
| Locating | TL | 2486 | 1405 | 2876 | 71 | 695 |
| Locating | TV | 26733 | 4024 | 2369 | 58 | 695 |
| Locating | TLV | 26473 | 4278 | 2698 | 61 | 695 |
| Locating | V | 26464 | 3310 | 1928 | 53 | 695 |
| Reasoning | T | 1669 | 939 | 6080 | 151 | 384 |
| Reasoning | TL | 2491 | 1376 | 6030 | 138 | 384 |
| Reasoning | TV | 28582 | 4179 | 7254 | 163 | 384 |
| Reasoning | TLV | 26616 | 4236 | 6826 | 144 | 384 |
| Reasoning | V | 29839 | 3689 | 6347 | 161 | 384 |
| Understanding | T | 1483 | 843 | 5525 | 140 | 1238 |
| Understanding | TL | 2066 | 1156 | 5819 | 140 | 1238 |
| Understanding | TV | 25540 | 3768 | 6245 | 144 | 1238 |
| Understanding | TLV | 25453 | 3976 | 6287 | 138 | 1238 |
| Understanding | V | 24951 | 3119 | 5242 | 137 | 1238 |
| n (per col) | - | - | - | - | - | - |
