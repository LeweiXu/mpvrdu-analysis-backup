# Tables

The same tables as `all_tables.md`, condensed. **Levels are not comparable across datasets** (different document lengths, gold-page counts and answer styles); what is comparable is how each corpus responds to the same intervention, so read the deltas. What was left out of this report, and why, is in `../report.md`.

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Representation ladder, both datasets

> **swept**: representation ladder x dataset · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **pools**: MMLongBench complete answerable pool (847 questions); LongDocURL oracle ladder (ldu-representation)

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| dataset | T | TL | TV | TLV | V | best rung | T -> best (pts) | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MMLongBench-Doc | 31.9 a7.3 w60.8 (n=847) | 38.8 a3.2 w58.0 (n=847) | 51.6 a1.4 w47.0 (n=847) | 52.5 a1.4 w46.0 (n=847) | 45.6 a1.1 w53.4 (n=847) | TLV | +20.7 | 4235 |
| MMLongBench-Doc (digital) | 39.9 a3.0 w57.1 (n=657) | 40.5 a2.1 w57.4 (n=657) | 49.9 a1.2 w48.9 (n=657) | 50.1 a1.1 w48.9 (n=657) | 42.5 a0.8 w56.8 (n=657) | TLV | +10.2 | 3285 |
| LongDocURL | 63.7 a1.0 w35.3 (n=2295) | 68.0 a0.9 w31.2 (n=2225) | 69.5 a0.2 w30.3 (n=2270) | 71.9 a0.4 w27.8 (n=2168) | 63.1 a0.3 w36.6 (n=2304) | TLV | +8.1 | 11262 |

### Representation ladder by evidence source, both datasets

> **swept**: representation ladder x evidence source x dataset · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **evidence sources**: reconciled to four shared categories; MMLongBench Chart folded into Figure, (none)/Others excluded · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: page recall x retriever x depth x dataset · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **depths**: k present in both sweeps (1, 5, 10)

_READ DOWN A DATASET, NOT ACROSS ONE. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: integration gap (M-S) x rung x dataset · **datasets**: both datasets, on their own pools; levels are not comparable across datasets, the response to the intervention is · **hop**: from the question's gold evidence-page count, annotated the same way by both corpora

_MMLongBench-Doc is the complete answerable pool (g4-faithfulness-full prompt_mode=none plus the g1-tv-full TV rung, 847 questions, no OOM attrition); LongDocURL is its oracle ladder (ldu-representation). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| dataset | T | TL | TV | TLV | V | nS | nM |
| --- | --- | --- | --- | --- | --- | --- | --- |
| MMLongBench-Doc | -12.2 | -13.7 | -23.5 | -25.0 | -21.7 | 480 | 358 |
| MMLongBench-Doc (digital) | -12.1 | -15.7 | -24.9 | -26.8 | -22.9 | 382 | 268 |
| LongDocURL | -3.4 | -11.6 | -5.6 | -5.4 | -2.5 | 1093 | 1209 |
