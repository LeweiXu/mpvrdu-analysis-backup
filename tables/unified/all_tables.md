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

### Representation ladder, both datasets

> **swept**: representation ladder x dataset · **dataset**: mmlongbench + longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **pools**: MMLongBench complete answerable pool (847 questions); LongDocURL oracle ladder (ldu-representation)

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). Both are oracle pages, one reasoner (Qwen3-VL-8B bf16, med resolution, paddleocrvl), no prompt instruction, so the rung is the only thing that varies. READ DOWN A DATASET, NOT ACROSS ONE. The two corpora differ in ways no column here controls: LongDocURL documents run 51-149 pages (mean 89) against MMLongBench's 47.5, its questions carry more gold pages, and 14.6% of them are multiple-choice or yes/no against MMLongBench's 1.4%, which puts a floor under its accuracy that MMLongBench has no equivalent of. A gap between the two rows is a dataset difference, not a method one. What IS comparable is the SHAPE of each dataset's response to the same intervention, which is why every table here carries a per-dataset delta rather than only levels. THE `(digital)` ROW IS THE SCAN CONTROL, and it is the row to compare against LongDocURL. MMLongBench-Doc is 29 of 135 documents scanned (190 of 847 answerable questions) against LongDocURL's 2 of 396 (5 of 2,317), so the unfiltered MMLongBench row prices OCR failure and the reasoning task together while the LongDocURL row beside it prices only the second. The asymmetry bites hardest at the text rungs: 24.5% of MMLongBench questions sit on an evidence page whose embedded text layer is EMPTY, against 0.8% on LongDocURL, so `T` is fed nothing at all on a quarter of the pool. `(digital)` is the same pool, same cells, restricted to documents PyMuPDF classes as born-digital (`annotations/auto_scan.csv`); it is a SUBSET of the row above it, not an independent run. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. `T -> best` is how much the best rung buys over text-only on that dataset, which is the quantity the two corpora can be compared on._

| dataset | T | TL | TV | TLV | V | best rung | T -> best (pts) | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MMLongBench-Doc | 31.9 a7.3 w60.8 (n=847) | 38.8 a3.2 w58.0 (n=847) | 51.6 a1.4 w47.0 (n=847) | 52.5 a1.4 w46.0 (n=847) | 45.6 a1.1 w53.4 (n=847) | TLV | +20.7 | 4235 |
| MMLongBench-Doc (digital) | 39.9 a3.0 w57.1 (n=657) | 40.5 a2.1 w57.4 (n=657) | 49.9 a1.2 w48.9 (n=657) | 50.1 a1.1 w48.9 (n=657) | 42.5 a0.8 w56.8 (n=657) | TLV | +10.2 | 3285 |
| LongDocURL | 63.7 a1.0 w35.3 (n=2295) | 68.0 a0.9 w31.2 (n=2225) | 69.5 a0.2 w30.3 (n=2270) | 71.9 a0.4 w27.8 (n=2168) | 63.1 a0.3 w36.6 (n=2304) | TLV | +8.1 | 11262 |

### Representation ladder by evidence source, both datasets

> **swept**: representation ladder x evidence source x dataset · **dataset**: mmlongbench + longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **evidence sources**: reconciled to four shared categories; MMLongBench Chart folded into Figure, (none)/Others excluded · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). Both are oracle pages, one reasoner (Qwen3-VL-8B bf16, med resolution, paddleocrvl), no prompt instruction, so the rung is the only thing that varies. READ DOWN A DATASET, NOT ACROSS ONE. The two corpora differ in ways no column here controls: LongDocURL documents run 51-149 pages (mean 89) against MMLongBench's 47.5, its questions carry more gold pages, and 14.6% of them are multiple-choice or yes/no against MMLongBench's 1.4%, which puts a floor under its accuracy that MMLongBench has no equivalent of. A gap between the two rows is a dataset difference, not a method one. What IS comparable is the SHAPE of each dataset's response to the same intervention, which is why every table here carries a per-dataset delta rather than only levels. THE `(digital)` ROW IS THE SCAN CONTROL, and it is the row to compare against LongDocURL. MMLongBench-Doc is 29 of 135 documents scanned (190 of 847 answerable questions) against LongDocURL's 2 of 396 (5 of 2,317), so the unfiltered MMLongBench row prices OCR failure and the reasoning task together while the LongDocURL row beside it prices only the second. The asymmetry bites hardest at the text rungs: 24.5% of MMLongBench questions sit on an evidence page whose embedded text layer is EMPTY, against 0.8% on LongDocURL, so `T` is fed nothing at all on a quarter of the pool. `(digital)` is the same pool, same cells, restricted to documents PyMuPDF classes as born-digital (`annotations/auto_scan.csv`); it is a SUBSET of the row above it, not an independent run. Cells read `accuracy [95% CI] a<declined> w<wrong>`, three percentages that sum to 100. `a` is the share the reasoner declined to answer, `w` the share it committed to a wrong answer. The split is disjoint by construction rather than `100 - accuracy - abstention`: a row can be flagged both correct and abstained, so `a` counts only abstentions that were not credited. On an unanswerable pool a correct abstention scores under accuracy instead, which is the definition the faithfulness tables already use. `a` is NOT simply an error rate on an answerable pool either: at `T` a scanned page has no embedded text, so declining is the right response to what that rung actually delivered. The faithfulness tables split `a` by scan status for exactly this reason. Evidence sources are reconciled onto four shared categories: MMLongBench's `Pure-text (Plain-text)` and LongDocURL's `Text` are one column, likewise `Generalized-text (Layout)`/`Layout`; MMLongBench's `Chart` is folded into `Figure`, which is the only join available because LongDocURL draws no chart/figure line. MMLongBench's `(none)` and LongDocURL's `Others` are excluded as non-corresponding. A question citing several sources is counted under each, so rows overlap and n does not sum to the pool._

| evidence source | dataset | T | TL | TV | TLV | V | T -> best (pts) | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Text | MMLongBench-Doc | 39.2 a4.1 w56.7 (n=291) | 47.8 a1.7 w50.5 (n=291) | 53.6 a1.4 w45.0 (n=291) | 55.3 a1.4 w43.3 (n=291) | 44.3 a0.3 w55.3 (n=291) | +16.2 | 1455 |
| Text | MMLongBench-Doc (digital) | 48.5 a1.3 w50.2 (n=231) | 51.5 a0.4 w48.1 (n=231) | 55.4 a1.3 w43.3 (n=231) | 56.7 a0.9 w42.4 (n=231) | 44.6 a0.0 w55.4 (n=231) | +8.2 | 1155 |
| Text | LongDocURL | 75.3 a1.2 w23.5 (n=984) | 79.5 a0.7 w19.8 (n=970) | 80.5 a0.4 w19.1 (n=971) | 82.3 a0.5 w17.2 (n=942) | 74.0 a0.3 w25.7 (n=985) | +7.0 | 4852 |
| Table | MMLongBench-Doc | 40.6 a6.0 w53.5 (n=217) | 48.4 a0.9 w50.7 (n=217) | 47.0 a2.8 w50.2 (n=217) | 48.4 a2.3 w49.3 (n=217) | 37.8 a1.8 w60.4 (n=217) | +7.8 | 1085 |
| Table | MMLongBench-Doc (digital) | 47.1 a1.6 w51.3 (n=187) | 46.5 a0.5 w52.9 (n=187) | 44.9 a2.1 w52.9 (n=187) | 44.9 a1.6 w53.5 (n=187) | 34.2 a1.1 w64.7 (n=187) | +0.0 | 935 |
| Table | LongDocURL | 61.2 a0.9 w37.9 (n=858) | 69.5 a1.1 w29.3 (n=811) | 64.6 a0.0 w35.4 (n=853) | 68.2 a0.3 w31.6 (n=789) | 57.3 a0.1 w42.6 (n=868) | +8.4 | 4179 |
| Layout | MMLongBench-Doc | 28.0 a1.7 w70.3 (n=118) | 37.3 a4.2 w58.5 (n=118) | 49.2 a0.8 w50.0 (n=118) | 50.8 a0.0 w49.2 (n=118) | 44.1 a0.8 w55.1 (n=118) | +22.9 | 590 |
| Layout | MMLongBench-Doc (digital) | 38.1 a1.2 w60.7 (n=84) | 41.7 a1.2 w57.1 (n=84) | 47.6 a0.0 w52.4 (n=84) | 46.4 a0.0 w53.6 (n=84) | 41.7 a0.0 w58.3 (n=84) | +9.5 | 420 |
| Layout | LongDocURL | 48.7 a0.5 w50.8 (n=762) | 52.4 a0.3 w47.3 (n=740) | 56.4 a0.3 w43.4 (n=747) | 56.3 a0.4 w43.2 (n=710) | 52.2 a0.4 w47.4 (n=766) | +7.7 | 3725 |
| Figure | MMLongBench-Doc | 16.8 a11.2 w71.9 (n=463) | 22.0 a5.0 w73.0 (n=463) | 44.1 a1.9 w54.0 (n=463) | 44.9 a2.4 w52.7 (n=463) | 41.3 a1.3 w57.5 (n=463) | +28.1 | 2315 |
| Figure | MMLongBench-Doc (digital) | 22.1 a5.7 w72.2 (n=317) | 20.5 a3.5 w76.0 (n=317) | 39.7 a1.6 w58.7 (n=317) | 39.7 a1.9 w58.4 (n=317) | 36.0 a0.6 w63.4 (n=317) | +17.7 | 1585 |
| Figure | LongDocURL | 62.6 a1.5 w35.9 (n=546) | 66.1 a1.5 w32.4 (n=537) | 67.8 a0.2 w32.0 (n=543) | 73.4 a0.6 w26.0 (n=534) | 64.8 a0.2 w35.0 (n=546) | +10.8 | 2706 |

## Selection

### Retrieval: page recall at shared depths, both datasets

> **swept**: page recall x retriever x depth x dataset · **dataset**: mmlongbench + longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **depths**: k present in both sweeps (1, 5, 10)

_READ DOWN A DATASET, NOT ACROSS ONE. The two corpora differ in ways no column here controls: LongDocURL documents run 51-149 pages (mean 89) against MMLongBench's 47.5, its questions carry more gold pages, and 14.6% of them are multiple-choice or yes/no against MMLongBench's 1.4%, which puts a floor under its accuracy that MMLongBench has no equivalent of. A gap between the two rows is a dataset difference, not a method one. What IS comparable is the SHAPE of each dataset's response to the same intervention, which is why every table here carries a per-dataset delta rather than only levels. THE `(digital)` ROW IS THE SCAN CONTROL, and it is the row to compare against LongDocURL. MMLongBench-Doc is 29 of 135 documents scanned (190 of 847 answerable questions) against LongDocURL's 2 of 396 (5 of 2,317), so the unfiltered MMLongBench row prices OCR failure and the reasoning task together while the LongDocURL row beside it prices only the second. The asymmetry bites hardest at the text rungs: 24.5% of MMLongBench questions sit on an evidence page whose embedded text layer is EMPTY, against 0.8% on LongDocURL, so `T` is fed nothing at all on a quarter of the pool. `(digital)` is the same pool, same cells, restricted to documents PyMuPDF classes as born-digital (`annotations/auto_scan.csv`); it is a SUBSET of the row above it, not an independent run. Page recall over each corpus's own pages, so the levels are not comparable across datasets (LongDocURL documents are roughly twice as long, and its questions carry more gold pages). The ORDERING of retrievers is, and it is the same ordering on both. Only retrievers and depths present in both sweeps are listed._

| retriever | dataset | R@1 | R@5 | R@10 | n |
| --- | --- | --- | --- | --- | --- |
| bge-m3 | MMLongBench-Doc | 0.255 | 0.482 | 0.611 | 847 |
| bge-m3 | MMLongBench-Doc (digital) | 0.322 | 0.593 | 0.713 | 657 |
| bge-m3 | LongDocURL | 0.334 | 0.623 | 0.726 | 2317 |
| bge-m3\|colqwen2.5 | MMLongBench-Doc | 0.552 | 0.798 | - | 847 |
| bge-m3\|colqwen2.5 | MMLongBench-Doc (digital) | 0.555 | 0.802 | - | 657 |
| bge-m3\|colqwen2.5 | LongDocURL | 0.558 | 0.820 | - | 2317 |
| bm25 | MMLongBench-Doc | 0.222 | 0.460 | 0.585 | 847 |
| bm25 | MMLongBench-Doc (digital) | 0.279 | 0.560 | 0.672 | 657 |
| bm25 | LongDocURL | 0.356 | 0.611 | 0.695 | 2317 |
| bm25\|colmodernvbert | MMLongBench-Doc | 0.512 | 0.776 | - | 847 |
| bm25\|colmodernvbert | MMLongBench-Doc (digital) | 0.517 | 0.782 | - | 657 |
| bm25\|colmodernvbert | LongDocURL | 0.541 | 0.789 | - | 2317 |
| colmodernvbert | MMLongBench-Doc | 0.460 | 0.725 | 0.817 | 847 |
| colmodernvbert | MMLongBench-Doc (digital) | 0.454 | 0.721 | 0.821 | 657 |
| colmodernvbert | LongDocURL | 0.475 | 0.745 | 0.831 | 2317 |
| colqwen2.5 | MMLongBench-Doc | 0.488 | 0.749 | 0.838 | 847 |
| colqwen2.5 | MMLongBench-Doc (digital) | 0.478 | 0.741 | 0.842 | 657 |
| colqwen2.5 | LongDocURL | 0.493 | 0.780 | 0.852 | 2317 |
| colqwen3 | MMLongBench-Doc | 0.541 | 0.806 | 0.874 | 847 |
| colqwen3 | MMLongBench-Doc (digital) | 0.542 | 0.811 | 0.882 | 657 |
| colqwen3 | LongDocURL | 0.536 | 0.811 | 0.881 | 2317 |

## Integration

### Integration gap (multi - single page accuracy) per rung, both datasets

> **swept**: integration gap (M-S) x rung x dataset · **dataset**: mmlongbench + longdocurl · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **hop**: from the question's gold evidence-page count, annotated the same way by both corpora

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). Both are oracle pages, one reasoner (Qwen3-VL-8B bf16, med resolution, paddleocrvl), no prompt instruction, so the rung is the only thing that varies. READ DOWN A DATASET, NOT ACROSS ONE. The two corpora differ in ways no column here controls: LongDocURL documents run 51-149 pages (mean 89) against MMLongBench's 47.5, its questions carry more gold pages, and 14.6% of them are multiple-choice or yes/no against MMLongBench's 1.4%, which puts a floor under its accuracy that MMLongBench has no equivalent of. A gap between the two rows is a dataset difference, not a method one. What IS comparable is the SHAPE of each dataset's response to the same intervention, which is why every table here carries a per-dataset delta rather than only levels. THE `(digital)` ROW IS THE SCAN CONTROL, and it is the row to compare against LongDocURL. MMLongBench-Doc is 29 of 135 documents scanned (190 of 847 answerable questions) against LongDocURL's 2 of 396 (5 of 2,317), so the unfiltered MMLongBench row prices OCR failure and the reasoning task together while the LongDocURL row beside it prices only the second. The asymmetry bites hardest at the text rungs: 24.5% of MMLongBench questions sit on an evidence page whose embedded text layer is EMPTY, against 0.8% on LongDocURL, so `T` is fed nothing at all on a quarter of the pool. `(digital)` is the same pool, same cells, restricted to documents PyMuPDF classes as born-digital (`annotations/auto_scan.csv`); it is a SUBSET of the row above it, not an independent run. M-S in points, negative = multi-page questions are answered worse. `hop` is derived from the question's gold evidence-page count, which both corpora annotate the same way, so this is the most directly comparable quantity in the unified report._

| dataset | T | TL | TV | TLV | V | nS | nM |
| --- | --- | --- | --- | --- | --- | --- | --- |
| MMLongBench-Doc | -12.2 | -13.7 | -23.5 | -25.0 | -21.7 | 480 | 358 |
| MMLongBench-Doc (digital) | -12.1 | -15.7 | -24.9 | -26.8 | -22.9 | 382 | 268 |
| LongDocURL | -3.4 | -11.6 | -5.6 | -5.4 | -2.5 | 1093 | 1209 |
