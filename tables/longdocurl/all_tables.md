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

| doc_type | frontier | n |
| --- | --- | --- |
|  |  |  |
| **all doc_types** | - | **0** |
| n (per col) | - | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. _

| evidence_source | n |
| --- | --- |
|  |  |
| n (per col) | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition x doc_type · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Each question carries exactly one doc_type, so unlike the evidence-source table the rows within a block are disjoint and the bolded All doc_types row closing it is their sum._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |
| n (per col) | - | - | - | - | - | - |

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

## Integration

### Integration: accuracy by evidence hop, per doc_type and rung (oracle pages)

> **swept**: gold evidence-page count (single vs multi) x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| doc_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
| n (per col) | - | 0 | 0 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view._

| evidence pages | n |
| --- | --- |
|  |  |
| n (per col) | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: gold evidence-page bucket x rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **cells**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. `1 → 6+` is the accuracy of the last bucket minus the first, in points; negative means the rung degrades as evidence spreads. Read it against the per-cell n: TLV OOMs hardest at high page counts, so its tail buckets are a handful of surviving questions and its slope is not comparable to the text rungs'._

| rung | 1 → 6+ | n |
| --- | --- | --- |
|  |  |  |
| n (per col) | - | - |

## Deployment

### Mined: OOM rate by rung, resolution, and pages-fed

> **swept**: rung x pages fed · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none · **attrition**: OOM attrition is NESTED, not random: at TLV the questions that OOM at d=5 are a strict superset of those at d=4, and so on down. A cell at high distractor count is therefore the surviving lightest questions, so compare down a column only on the matched question set, never on the raw per-cell accuracy

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. rate = oom cells / all cells in the group, over the 16 GB V100 runs._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
| n (per col) | - | - | - | - | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: rung · **dataset**: longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: LongDocURL answerable pool, 2,317 questions over 395 documents (51-149 pages, mean 89) · **page_selection**: oracle · **prompt_mode**: none

_LongDocURL. Built by the same builder as the MMLongBench table of the same name, so the layout, groupings and per-cell n mean exactly what they do there. The pools are NOT comparable cell for cell: LongDocURL documents are 51-149 pages (mean 89) against MMLongBench's 47.5, and its questions carry more gold pages, so read a difference between the two reports as a dataset difference and not a method one. `prefill_ms` and `input_tokens` are the INPUT-bound cost, set by the representation. `decode_ms` and `output_tokens` are the OUTPUT-bound cost, set by the prompt and the decode budget, not by the rung: a rung appears to decode more only because a longer input tends to draw a longer answer. Read the two halves separately; their sum is not the end-to-end latency, which also carries scheduling and detokenisation. ⚠ These rows come from the prompt_mode=none run, which carries NO instruction at all (`config.PROMPT_MODES['none']` is the empty string), so the model rambles and `decode_ms` here is an upper bound, not a deployment figure. The per-prompt-mode decode table gives the instructed cost, on different hardware._

| doc_type | rung | prefill_ms | input_tokens | decode_ms | output_tokens | n |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |
| n (per col) | - | - | - | - | - | - |
