# Tables

## ⚠ RECONCILIATION FAILED

```
reconciliation:
  [SKIP] headline T reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B T == headline (expected 31.9, got 31.9)
  [PASS] G4 none T reproduces the headline ladder (expected 31.9, got 31.9)
  [SKIP] headline TL reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B TL == headline (expected 39.4, got 39.4)
  [PASS] G4 none TL reproduces the headline ladder (expected 39.4, got 38.8)
  [SKIP] headline TLV reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B TLV == headline (expected 56.8, got 56.8)
  [FAIL] G4 none TLV reproduces the headline ladder (expected 56.8, got 52.5)
  [SKIP] headline V reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B V == headline (expected 45.9, got 45.9)
  [PASS] G4 none V reproduces the headline ladder (expected 45.9, got 45.6)
  [FAIL] G3 re-run none abstention reproduces the legacy rate (expected 16.9, got 13.5)
  [PASS] G3 re-run grounded abstention reproduces the legacy rate (expected 10.7, got 10.549999999999999)
  [PASS] G3 re-run abstain abstention reproduces the legacy rate (expected 80.7, got 79.29999999999998)
```

## Generation report (actual cells run)

| run_tag | task | cells | ok | oom | error | oom % |
| --- | --- | --- | --- | --- | --- | --- |
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
| g2-retrieval-full | G2_retrieval | 5703 | 4435 | 1268 | 0 | 22.2 |
| g3-faithfulness-full | G3_hallucination | 5856 | 5856 | 0 | 0 | 0.0 |
| g3-hallucination-full | G3_hallucination | 2928 | 2698 | 230 | 0 | 7.9 |
| g4-faithfulness-full | G4_faithfulness_answerable | 20328 | 20328 | 0 | 0 | 0.0 |
| g5a-drop-best | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-drop-worst | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-keep-best | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5a-keep-worst | G5_selection | 2864 | 2816 | 0 | 48 | 0.0 |
| g5b-gold1 | G5_selection | 7680 | 7584 | 0 | 96 | 0.0 |
| g5b-gold2 | G5_selection | 3936 | 3856 | 0 | 80 | 0.0 |
| g5b-gold3 | G5_selection | 640 | 640 | 0 | 0 | 0.0 |
| **all** |  | **94101** | 90463 | 3270 | 368 | 3.5 |

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## RQ1 — Error attribution (where the loss is)

### Headline: cost-ordered ladder accuracy by doc_type (oracle pages)

> **swept**: representation ladder T/TL/TLV/V · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| doc_type | T | TL | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 39.2 [28.8-48.3] | 37.7 [28.6-47.1] | 42.0 [31.6-51.3] | 31.4 [24.5-38.4] | T | 550 |
| Administration/Industry file | 50.0 [33.3-69.1] | 57.9 [48.4-70.2] | 74.5 [64.7-88.1] | 50.8 [43.9-59.2] | TLV | 233 |
| Brochure | 28.0 [17.1-39.7] | 32.9 [22.4-45.6] | 41.7 [28.0-56.0] | 45.5 [32.5-58.4] | TL | 300 |
| Financial report | 50.5 [40.4-59.8] | 64.3 [49.1-75.7] | 72.1 [66.0-79.4] | 36.1 [29.5-43.4] | TL | 353 |
| Guidebook | 35.0 [22.0-50.4] | 36.5 [23.8-49.5] | 51.8 [38.1-65.0] | 47.5 [35.5-59.7] | T | 463 |
| Research report / Introduction | 21.5 [13.4-29.6] | 26.7 [19.0-34.2] | 52.7 [43.5-60.5] | 46.9 [36.9-55.2] | TLV | 804 |
| Tutorial/Workshop | 13.4 [6.1-21.4] | 46.8 [39.0-54.0] | 76.6 [69.8-83.2] | 70.0 [63.8-76.1] | TLV | 440 |
| **all doc_types** | **31.9 [27.1-36.6]** | **39.4 [35.2-43.8]** | **56.8 [52.0-61.2]** | **45.9 [42.0-50.0]** | **TLV** | **3143** |
| n (per col) | 831 | 761 | 717 | 834 | - | - |

### Fidelity: paired within-question verdict transitions by evidence source

> **swept**: rung transition (TL→TLV, T→TL, T→TLV) × evidence source · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok · **transition columns**: percentages summing to 100 per row (parenthesised figure is the raw count) · **All sources row**: pooled over questions, each counted once; not a column sum, has its own paired n

_Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. A question citing several evidence sources is counted under each of them, so the per-source rows overlap and CANNOT be summed. The bolded All sources row closing each block is therefore computed fresh over every paired question in that pairing, each counted once, with its own paired n; it is a pooled total, not a column sum._

| pairing | evidence_source | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | (none) | 11.8 (2) | 5.9 (1) | 58.8 (10) | 23.5 (4) | 17 |
| TL->TLV | Chart | 32.1 (51) | 2.5 (4) | 17.0 (27) | 48.4 (77) | 159 |
| TL->TLV | Figure | 23.9 (63) | 1.5 (4) | 22.0 (58) | 52.7 (139) | 264 |
| TL->TLV | Generalized-text (Layout) | 16.3 (16) | 2.0 (2) | 38.8 (38) | 42.9 (42) | 98 |
| TL->TLV | Pure-text (Plain-text) | 10.6 (27) | 2.4 (6) | 47.5 (121) | 39.6 (101) | 255 |
| TL->TLV | Table | 6.7 (10) | 3.3 (5) | 54.0 (81) | 36.0 (54) | 150 |
| TL->TLV | **All sources** | 18.7 (134) | 2.4 (17) | 38.1 (273) | 40.9 (293) | 717 |
| T->TL | (none) | 11.8 (2) | 0.0 (0) | 52.9 (9) | 35.3 (6) | 17 |
| T->TL | Chart | 6.4 (11) | 5.8 (10) | 12.9 (22) | 74.9 (128) | 171 |
| T->TL | Figure | 13.8 (38) | 6.5 (18) | 9.1 (25) | 70.7 (195) | 276 |
| T->TL | Generalized-text (Layout) | 14.8 (16) | 3.7 (4) | 25.0 (27) | 56.5 (61) | 108 |
| T->TL | Pure-text (Plain-text) | 12.5 (34) | 4.0 (11) | 35.7 (97) | 47.8 (130) | 272 |
| T->TL | Table | 18.5 (29) | 4.5 (7) | 38.9 (61) | 38.2 (60) | 157 |
| T->TL | **All sources** | 12.8 (97) | 5.1 (39) | 26.8 (203) | 55.3 (419) | 758 |
| T->TLV | (none) | 23.5 (4) | 5.9 (1) | 47.1 (8) | 23.5 (4) | 17 |
| T->TLV | Chart | 33.3 (53) | 3.8 (6) | 15.7 (25) | 47.2 (75) | 159 |
| T->TLV | Figure | 34.6 (91) | 4.6 (12) | 11.4 (30) | 49.4 (130) | 263 |
| T->TLV | Generalized-text (Layout) | 30.9 (30) | 5.2 (5) | 24.7 (24) | 39.2 (38) | 97 |
| T->TLV | Pure-text (Plain-text) | 20.4 (52) | 3.1 (8) | 37.6 (96) | 38.8 (99) | 255 |
| T->TLV | Table | 22.0 (33) | 4.7 (7) | 38.7 (58) | 34.7 (52) | 150 |
| T->TLV | **All sources** | 27.9 (200) | 3.8 (27) | 28.9 (207) | 39.4 (282) | 716 |
| n (per col) | TL->TLV: 717, T->TL: 758, T->TLV: 716 | - | - | - | - | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition (TL→TLV, T→TL, T→TLV) × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok · **transition columns**: percentages summing to 100 per row (parenthesised figure is the raw count)

_Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Each question carries exactly one doc_type, so unlike the evidence-source table the rows within a block are disjoint and the bolded All doc_types row closing it is their sum._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | Academic paper | 9.2 (11) | 5.0 (6) | 32.8 (39) | 52.9 (63) | 119 |
| TL->TLV | Administration/Industry file | 16.4 (9) | 0.0 (0) | 58.2 (32) | 25.5 (14) | 55 |
| TL->TLV | Brochure | 13.9 (10) | 4.2 (3) | 27.8 (20) | 54.2 (39) | 72 |
| TL->TLV | Financial report | 10.3 (7) | 1.5 (1) | 61.8 (42) | 26.5 (18) | 68 |
| TL->TLV | Guidebook | 14.5 (16) | 0.9 (1) | 37.3 (41) | 47.3 (52) | 110 |
| TL->TLV | Research report / Introduction | 26.3 (49) | 2.2 (4) | 26.3 (49) | 45.2 (84) | 186 |
| TL->TLV | Tutorial/Workshop | 29.9 (32) | 1.9 (2) | 46.7 (50) | 21.5 (23) | 107 |
| TL->TLV | **All doc_types** | 18.7 (134) | 2.4 (17) | 38.1 (273) | 40.9 (293) | 717 |
| T->TL | Academic paper | 4.7 (6) | 9.4 (12) | 33.6 (43) | 52.3 (67) | 128 |
| T->TL | Administration/Industry file | 15.8 (9) | 7.0 (4) | 42.1 (24) | 35.1 (20) | 57 |
| T->TL | Brochure | 9.3 (7) | 4.0 (3) | 24.0 (18) | 62.7 (47) | 75 |
| T->TL | Financial report | 11.4 (8) | 4.3 (3) | 52.9 (37) | 31.4 (22) | 70 |
| T->TL | Guidebook | 5.2 (6) | 4.3 (5) | 31.3 (36) | 59.1 (68) | 115 |
| T->TL | Research report / Introduction | 10.9 (22) | 5.0 (10) | 15.8 (32) | 68.3 (138) | 202 |
| T->TL | Tutorial/Workshop | 35.1 (39) | 1.8 (2) | 11.7 (13) | 51.4 (57) | 111 |
| T->TL | **All doc_types** | 12.8 (97) | 5.1 (39) | 26.8 (203) | 55.3 (419) | 758 |
| T->TLV | Academic paper | 9.2 (11) | 10.1 (12) | 32.8 (39) | 47.9 (57) | 119 |
| T->TLV | Administration/Industry file | 25.5 (14) | 0.0 (0) | 49.1 (27) | 25.5 (14) | 55 |
| T->TLV | Brochure | 22.5 (16) | 7.0 (5) | 19.7 (14) | 50.7 (36) | 71 |
| T->TLV | Financial report | 16.2 (11) | 1.5 (1) | 55.9 (38) | 26.5 (18) | 68 |
| T->TLV | Guidebook | 16.4 (18) | 1.8 (2) | 35.5 (39) | 46.4 (51) | 110 |
| T->TLV | Research report / Introduction | 33.9 (63) | 3.8 (7) | 18.8 (35) | 43.5 (81) | 186 |
| T->TLV | Tutorial/Workshop | 62.6 (67) | 0.0 (0) | 14.0 (15) | 23.4 (25) | 107 |
| T->TLV | **All doc_types** | 27.9 (200) | 3.8 (27) | 28.9 (207) | 39.4 (282) | 716 |
| n (per col) | TL->TLV: 717, T->TL: 758, T->TLV: 716 | - | - | - | - | - |

### Fidelity (overall): paired verdict transitions per rung pairing

> **view**: summary — pooled across all doc_types · **swept**: rung transition (TL→TLV, T→TL, T→TLV) × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok · **transition columns**: percentages summing to 100 per row (parenthesised figure is the raw count)

| pairing | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- |
| TL->TLV | 18.7 (134) | 2.4 (17) | 38.1 (273) | 40.9 (293) | 717 |
| T->TL | 12.8 (97) | 5.1 (39) | 26.8 (203) | 55.3 (419) | 758 |
| T->TLV | 27.9 (200) | 3.8 (27) | 28.9 (207) | 39.4 (282) | 716 |
| n (per col) | - | - | - | - | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| evidence_source | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| (none) | 52.6 [31.2-73.7] | 64.7 [40.0-87.5] | 70.6 [44.4-94.1] | 47.4 [27.7-66.7] | 72 |
| Chart | 18.3 [12.2-24.4] | 19.2 [12.4-26.5] | 49.1 [40.3-57.9] | 45.7 [36.7-54.7] | 679 |
| Figure | 15.4 [10.4-20.5] | 22.7 [17.1-28.4] | 45.8 [38.2-53.0] | 40.8 [34.4-47.0] | 1115 |
| Generalized-text (Layout) | 27.8 [18.2-38.1] | 39.4 [30.1-48.1] | 55.1 [45.2-64.7] | 49.6 [41.3-58.7] | 437 |
| Pure-text (Plain-text) | 39.2 [31.4-48.0] | 48.0 [40.4-55.1] | 58.0 [50.2-65.4] | 44.4 [37.9-51.5] | 1097 |
| Table | 40.5 [32.8-47.4] | 57.3 [49.0-65.2] | 60.7 [53.6-67.7] | 37.5 [31.1-44.5] | 738 |
| n (per col) | 831 | 761 | 717 | 834 | - |

### Source stratification: oracle accuracy by source dataset and rung

> **swept**: source_dataset stratum × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **strata**: loader dataset id only; no upstream QA provenance exists

_This table cannot separate inherited from native questions, and the blank is the finding. `metadata.source_dataset` is the loader's dataset identifier, not the upstream QA dataset a question came from, so every judged row reads `mmlongbench` and no inherited-minus-native gap column can be computed. MMLongBench-Doc does not publish per-question upstream provenance in the staged config (the parquet carries doc_id, doc_type, question, answer, evidence_pages, evidence_sources, answer_format and nothing else), and no annotation file supplies it. So the memorisation-suspect channel is UNMEASURABLE on current data, not measured and found absent; closing it needs hand-labelling of document origin, which no run spec can produce. The `(uncoded)` stratum is the cells whose metadata is empty because they OOMed before producing an answer; they are shown with their n and no accuracy rather than dropped or imputed._

| source_dataset | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| mmlongbench | 31.9 [27.1-36.6] | 39.4 [35.2-43.8] | 56.8 [52.0-61.2] | 45.9 [42.0-50.0] | 3143 |
| (uncoded) | 16 cells, no acc | 86 cells, no acc | 130 cells, no acc | 13 cells, no acc | 245 |
| n (per col) | 831 | 761 | 717 | 834 | - |

### Attribution: representation / retrieval / reasoning loss per rung (PROVISIONAL)

> **swept**: loss channel (representation / retrieval / reasoning) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **retrieval source**: g2-retrieval-full generation rows, loaded by the builder · **status**: PROVISIONAL (partial G2 pool)

_PROVISIONAL (partial G2 pool). The retrieval-loss columns are built on the g2-retrieval-full generation pool, which was only ~36% pulled before the cluster migration with judging still in flight, so every retrieval number here is provisional until a clean re-run. The reasoning residual is a RAW, UNCORRECTED UPPER BOUND: it is simply the shortfall of the best oracle rung from 100%, and it still contains judge false negatives and answers that are correct without matching the gold span. Neither correction exists in the data, so neither has been netted out. Do not read the residual as a reasoning-error estimate. T and TL carry no retrieval column because G2 never ran the text-only rungs; TLV above k=3 and all k>=7 are blank because OOM attrition leaves too few comparable cells. Retrieval loss is measured against the BEST in-scope retrieval setting for that rung, so it is the conservative (smallest defensible) retrieval charge, and it is computed within-question against the same questions' oracle rows._

| rung | oracle acc | representation loss | retrieval ref | retrieved acc | retrieval loss | reasoning residual (raw UB) | oracle n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 31.9 [27.1-36.6] | +24.9 | - | - | - | - | 831 |
| TL | 39.4 [35.2-43.8] | +17.3 | - | - | - | - | 761 |
| TLV | 56.8 [52.0-61.2] | 0.0 (best rung) | joint k1 (paired n=254) | 45.7 | +9.4 | +43.2 | 717 |
| V | 45.9 [42.0-50.0] | +10.8 | vision k5 (paired n=300) | 36.7 | +3.7 | - | 834 |
| n (per col) | 3143 | - | - | - | - | - | - |

### Parser comparison: TL/TLV accuracy by doc_type

> **swept**: parser (paddleocrvl / mineru / unlimited) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| doc_type | paddleocrvl TL | paddleocrvl TLV | mineru TL | mineru TLV | unlimited TL | unlimited TLV | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 37.7 [28.6-47.1] | 42.0 [31.6-51.3] | 20.5 [11.4-30.1] | 35.3 [22.9-48.7] | 39.0 [28.9-49.3] | 42.1 [32.3-50.9] | 151 |
| Administration/Industry file | 57.9 [48.4-70.2] | 74.5 [64.7-88.1] | 44.1 [33.9-58.8] | 66.7 [58.8-80.0] | 65.0 [57.1-75.0] | 70.9 [62.3-83.3] | 61 |
| Brochure | 32.9 [22.4-45.6] | 41.7 [28.0-56.0] | 16.7 [9.5-24.6] | 40.0 [25.8-55.2] | 36.8 [26.0-48.1] | 50.0 [35.9-63.4] | 76 |
| Financial report | 64.3 [49.1-75.7] | 72.1 [66.0-79.4] | 42.5 [28.3-54.1] | 48.0 [37.5-56.7] | 55.7 [45.6-63.5] | 55.3 [48.2-63.0] | 107 |
| Guidebook | 36.5 [23.8-49.5] | 51.8 [38.1-65.0] | 26.2 [15.8-36.5] | 51.6 [36.0-65.2] | 37.8 [24.8-51.5] | 51.8 [38.0-66.0] | 119 |
| Research report / Introduction | 26.7 [19.0-34.2] | 52.7 [43.5-60.5] | 21.2 [14.4-27.7] | 47.5 [38.6-55.4] | 27.5 [20.1-35.1] | 54.0 [43.9-62.8] | 208 |
| Tutorial/Workshop | 46.8 [39.0-54.0] | 76.6 [69.8-83.2] | 37.3 [28.4-47.7] | 71.4 [64.0-78.9] | 46.4 [37.9-55.4] | 74.1 [66.7-81.7] | 112 |
| n (per col) | 761 | 717 | 770 | 696 | 818 | 767 | - |

### Parser comparison (overall): TL/TLV accuracy per parser

> **view**: summary — pooled across all doc_types · **swept**: parser (paddleocrvl / mineru / unlimited) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| parser | TL | TLV | n |
| --- | --- | --- | --- |
| paddleocrvl | 39.4 [35.2-43.8] | 56.8 [52.0-61.2] | 761 |
| mineru | 28.3 [24.0-32.6] | 50.6 [45.9-55.1] | 770 |
| unlimited | 40.8 [36.6-45.1] | 55.5 [51.3-59.9] | 818 |
| n (per col) | 2349 | 2180 | - |

### Integration: accuracy by evidence hop, per doc_type and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| doc_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 36.9 [22.5-50.6] | 43.5 [30.0-58.6] | +6.6 | 146 |
| Academic paper | TL | 33.3 [22.0-44.2] | 46.8 [28.9-62.5] | +13.5 | 128 |
| Academic paper | TLV | 38.8 [27.4-50.0] | 48.6 [31.2-65.7] | +9.9 | 117 |
| Academic paper | V | 29.8 [19.5-39.7] | 34.3 [23.9-46.4] | +4.6 | 151 |
| Administration/Industry file | T | 58.5 [38.3-80.6] | 37.5 [13.3-57.9] | -21.0 | 57 |
| Administration/Industry file | TL | 68.3 [57.4-81.1] | 38.5 [0.0-72.2] | -29.8 | 54 |
| Administration/Industry file | TLV | 85.4 [73.8-100.0] | 54.5 [14.3-77.8] | -30.8 | 52 |
| Administration/Industry file | V | 65.9 [56.5-77.1] | 23.5 [10.0-33.3] | -42.3 | 58 |
| Brochure | T | 22.9 [11.9-34.2] | 37.0 [14.3-61.5] | +14.1 | 75 |
| Brochure | TL | 30.6 [20.0-43.2] | 37.0 [16.7-56.0] | +6.4 | 76 |
| Brochure | TLV | 44.9 [30.2-60.8] | 34.8 [11.5-60.0] | -10.1 | 72 |
| Brochure | V | 44.9 [27.5-60.8] | 46.4 [26.1-67.9] | +1.5 | 77 |
| Financial report | T | 60.3 [46.3-72.9] | 37.2 [25.0-48.6] | -23.1 | 106 |
| Financial report | TL | 68.3 [54.5-78.0] | 44.4 [11.1-77.8] | -23.9 | 69 |
| Financial report | TLV | 76.7 [71.0-83.9] | 42.9 [16.7-66.7] | -33.8 | 67 |
| Financial report | V | 47.6 [33.9-62.3] | 20.5 [12.5-31.6] | -27.2 | 107 |
| Guidebook | T | 41.1 [26.0-58.3] | 25.5 [10.4-41.3] | -15.6 | 120 |
| Guidebook | TL | 44.4 [30.4-57.9] | 23.3 [9.3-38.5] | -21.2 | 115 |
| Guidebook | TLV | 58.3 [44.1-71.4] | 39.5 [20.0-59.5] | -18.9 | 110 |
| Guidebook | V | 54.8 [41.4-67.5] | 35.6 [21.3-48.9] | -19.2 | 118 |
| Research report / Introduction | T | 28.0 [17.3-39.8] | 14.7 [7.8-22.2] | -13.3 | 209 |
| Research report / Introduction | TL | 32.7 [21.9-43.1] | 20.0 [11.2-29.2] | -12.7 | 202 |
| Research report / Introduction | TLV | 67.3 [54.9-77.8] | 32.9 [21.7-44.1] | -34.4 | 186 |
| Research report / Introduction | V | 64.5 [53.2-73.8] | 28.0 [16.3-38.3] | -36.5 | 207 |
| Tutorial/Workshop | T | 22.2 [8.9-34.8] | 0.0 [0.0-0.0] | -22.2 | 109 |
| Tutorial/Workshop | TL | 52.4 [38.5-65.5] | 40.0 [28.6-49.1] | -12.4 | 108 |
| Tutorial/Workshop | TLV | 85.7 [76.9-93.9] | 65.9 [53.1-77.3] | -19.9 | 104 |
| Tutorial/Workshop | V | 81.0 [71.9-89.5] | 56.8 [45.2-67.6] | -24.1 | 107 |
| **all doc_types** | **T** | **37.2 [31.1-43.2]** | **25.1 [19.5-30.5]** | **-12.1** | **822** |
| **all doc_types** | **TL** | **44.6 [38.7-50.2]** | **31.5 [25.5-37.7]** | **-13.1** | **752** |
| **all doc_types** | **TLV** | **64.0 [58.4-69.5]** | **43.6 [36.0-50.4]** | **-20.3** | **708** |
| **all doc_types** | **V** | **55.0 [49.7-60.2]** | **34.2 [28.5-40.2]** | **-20.8** | **825** |
| n (per col) | - | 1904 | 1203 | - | - |

### Integration: accuracy by evidence hop, per evidence source and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × evidence source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse. Blocks are the evidence modality a question draws on, replacing the document class of the doc_type integration table; the hop split, pins, and gap column are identical. A question can cite SEVERAL sources (e.g. Chart + Table) and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus. The bolded All sources rows pool every question exactly once and are therefore NOT a column sum of the blocks above them. Per-cell n rides inline on the single and multi columns: OOM attrition is rung-dependent and the multi cells at TLV are thin, where a small n reads as survivorship, not signal._

| evidence_source | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 [42.9-85.7] (n=14) | 20.0 [0.0-60.0] (n=5) | -44.3 | 19 |
| (none) | TL | 78.6 [53.8-100.0] (n=14) | 0.0 [0.0-0.0] (n=3) | -78.6 | 17 |
| (none) | TLV | 85.7 [61.5-100.0] (n=14) | 0.0 [0.0-0.0] (n=3) | -85.7 | 17 |
| (none) | V | 57.1 [33.3-80.0] (n=14) | 20.0 [0.0-60.0] (n=5) | -37.1 | 19 |
| Chart | T | 20.4 [12.4-29.7] (n=98) | 15.8 [7.8-24.7] (n=76) | -4.6 | 174 |
| Chart | TL | 17.3 [10.0-25.3] (n=98) | 21.9 [12.7-32.1] (n=73) | +4.6 | 171 |
| Chart | TLV | 58.2 [44.8-69.2] (n=98) | 35.0 [22.2-48.2] (n=60) | -23.2 | 158 |
| Chart | V | 57.1 [44.9-68.1] (n=98) | 31.1 [20.3-43.3] (n=74) | -26.1 | 172 |
| Figure | T | 18.2 [12.1-25.3] (n=165) | 11.2 [5.6-18.5] (n=116) | -7.0 | 281 |
| Figure | TL | 24.7 [17.8-31.8] (n=166) | 19.6 [12.0-27.6] (n=107) | -5.1 | 273 |
| Figure | TLV | 49.4 [40.9-58.1] (n=166) | 40.9 [28.7-51.1] (n=93) | -8.5 | 259 |
| Figure | V | 45.2 [36.5-52.8] (n=166) | 35.3 [26.9-43.7] (n=116) | -9.8 | 282 |
| Generalized-text (Layout) | T | 34.5 [18.9-50.0] (n=55) | 22.4 [10.5-35.6] (n=58) | -12.1 | 113 |
| Generalized-text (Layout) | TL | 48.2 [35.4-62.1] (n=56) | 31.4 [17.3-44.9] (n=51) | -16.8 | 107 |
| Generalized-text (Layout) | TLV | 64.3 [51.9-76.9] (n=56) | 45.0 [28.9-61.4] (n=40) | -19.3 | 96 |
| Generalized-text (Layout) | V | 62.5 [48.9-75.5] (n=56) | 38.6 [26.8-50.0] (n=57) | -23.9 | 113 |
| Pure-text (Plain-text) | T | 46.8 [36.5-57.7] (n=154) | 31.0 [22.2-41.4] (n=126) | -15.8 | 280 |
| Pure-text (Plain-text) | TL | 56.2 [46.0-66.2] (n=153) | 38.5 [28.6-49.1] (n=117) | -17.7 | 270 |
| Pure-text (Plain-text) | TLV | 66.4 [55.3-76.1] (n=152) | 47.0 [35.6-58.7] (n=100) | -19.4 | 252 |
| Pure-text (Plain-text) | V | 55.8 [46.2-66.4] (n=154) | 31.8 [23.0-40.4] (n=129) | -24.1 | 283 |
| Table | T | 49.0 [38.6-58.5] (n=104) | 33.3 [24.8-42.0] (n=108) | -15.7 | 212 |
| Table | TL | 69.1 [59.8-77.1] (n=97) | 40.4 [27.6-54.5] (n=57) | -28.7 | 154 |
| Table | TLV | 70.8 [62.2-78.9] (n=96) | 43.1 [28.3-56.1] (n=51) | -27.7 | 147 |
| Table | V | 51.0 [41.7-59.6] (n=104) | 25.7 [17.7-35.3] (n=109) | -25.3 | 213 |
| **All sources** | **T** | **37.2 [31.1-43.2] (n=479)** | **25.1 [19.5-30.5] (n=343)** | **-12.1** | **822** |
| **All sources** | **TL** | **44.6 [38.7-50.2] (n=473)** | **31.5 [25.5-37.7] (n=279)** | **-13.1** | **752** |
| **All sources** | **TLV** | **64.0 [58.4-69.5] (n=472)** | **43.6 [36.0-50.4] (n=236)** | **-20.3** | **708** |
| **All sources** | **V** | **55.0 [49.7-60.2] (n=480)** | **34.2 [28.5-40.2] (n=345)** | **-20.8** | **825** |
| n (per col) | - | 1904 | 1203 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view._

| evidence pages | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| 1 | 37.2 [31.1-43.2] (n=479) | 44.6 [38.7-50.2] (n=473) | 64.0 [58.4-69.5] (n=472) | 55.0 [49.7-60.2] (n=480) | 1904 |
| 2 | 28.6 [22.3-35.0] (n=245) | 34.7 [27.7-41.9] (n=199) | 42.3 [34.7-49.8] (n=189) | 34.6 [27.9-41.2] (n=246) | 879 |
| 3 | 25.0 [10.2-41.5] (n=40) | 33.3 [18.2-50.0] (n=33) | 42.9 [25.9-61.5] (n=28) | 42.5 [24.3-57.8] (n=40) | 141 |
| 4-5 | 16.1 [3.1-32.4] (n=31) | 24.0 [8.7-38.5] (n=25) | 57.1 [27.3-80.0] (n=14) | 36.1 [20.0-51.4] (n=36) | 106 |
| 6+ | 3.7 [0.0-12.0] (n=27) | 9.1 [0.0-25.0] (n=22) | 60.0 [14.3-100.0] (n=5) | 13.0 [3.7-28.6] (n=23) | 77 |
| n (per col) | 822 | 752 | 708 | 825 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. `1 → 6+` is the accuracy of the last bucket minus the first, in points; negative means the rung degrades as evidence spreads. Read it against the per-cell n: TLV OOMs hardest at high page counts, so its tail buckets are a handful of surviving questions and its slope is not comparable to the text rungs'._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 37.2 [31.1-43.2] (n=479) | 28.6 [22.3-35.0] (n=245) | 25.0 [10.2-41.5] (n=40) | 16.1 [3.1-32.4] (n=31) | 3.7 [0.0-12.0] (n=27) | -33.5 | 822 |
| TL | 44.6 [38.7-50.2] (n=473) | 34.7 [27.7-41.9] (n=199) | 33.3 [18.2-50.0] (n=33) | 24.0 [8.7-38.5] (n=25) | 9.1 [0.0-25.0] (n=22) | -35.5 | 752 |
| TLV | 64.0 [58.4-69.5] (n=472) | 42.3 [34.7-49.8] (n=189) | 42.9 [25.9-61.5] (n=28) | 57.1 [27.3-80.0] (n=14) | 60.0 [14.3-100.0] (n=5) | -4.0 | 708 |
| V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 42.5 [24.3-57.8] (n=40) | 36.1 [20.0-51.4] (n=36) | 13.0 [3.7-28.6] (n=23) | -42.0 | 825 |
| n (per col) | 1904 | 879 | 141 | 106 | 77 | - | - |

### Integration cross-tab: accuracy by doc_type, rung, and evidence-page bucket (oracle pages)

> **swept**: doc_type × rung × evidence-page bucket (1 / 2 / 3+) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail

_Buckets are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it); zero-evidence questions are dropped. 3+ merges the finer 3 / 4-5 / 6+ buckets of the integration-detail table. Every cell carries its own n: OOM attrition is rung-dependent at high page counts (worst on TLV), so a thin cell reads as survivorship, not robustness — check the n before quoting the cell. The bolded All rows pool every doc_type._

| doc_type | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 36.9 [22.5-50.6] (n=84) | 44.7 [28.6-60.4] (n=47) | 40.0 [8.3-64.7] (n=15) | 146 |
| Academic paper | TL | 33.3 [22.0-44.2] (n=81) | 50.0 [30.3-67.7] (n=36) | 36.4 [9.1-66.7] (n=11) | 128 |
| Academic paper | TLV | 38.8 [27.4-50.0] (n=80) | 50.0 [30.8-68.6] (n=32) | 40.0 [0.0-85.7] (n=5) | 117 |
| Academic paper | V | 29.8 [19.5-39.7] (n=84) | 33.3 [18.7-47.6] (n=48) | 36.8 [12.5-57.1] (n=19) | 151 |
| Administration/Industry file | T | 58.5 [38.3-80.6] (n=41) | 18.2 [0.0-45.5] (n=11) | 80.0 [25.0-100.0] (n=5) | 57 |
| Administration/Industry file | TL | 68.3 [57.4-81.1] (n=41) | 30.0 [0.0-69.2] (n=10) | 66.7 [0.0-100.0] (n=3) | 54 |
| Administration/Industry file | TLV | 85.4 [73.8-100.0] (n=41) | 50.0 [14.3-72.7] (n=10) | 100.0 [100.0-100.0] (n=1) | 52 |
| Administration/Industry file | V | 65.9 [56.5-77.1] (n=41) | 18.2 [0.0-28.6] (n=11) | 33.3 [0.0-80.0] (n=6) | 58 |
| Brochure | T | 22.9 [11.9-34.2] (n=48) | 47.1 [21.0-75.0] (n=17) | 20.0 [0.0-50.0] (n=10) | 75 |
| Brochure | TL | 30.6 [20.0-43.2] (n=49) | 35.3 [12.5-60.0] (n=17) | 40.0 [12.5-63.6] (n=10) | 76 |
| Brochure | TLV | 44.9 [30.2-60.8] (n=49) | 20.0 [0.0-47.1] (n=15) | 62.5 [28.6-88.9] (n=8) | 72 |
| Brochure | V | 44.9 [27.5-60.8] (n=49) | 47.1 [18.8-76.5] (n=17) | 45.5 [11.1-72.7] (n=11) | 77 |
| Financial report | T | 60.3 [46.3-72.9] (n=63) | 36.6 [25.6-46.7] (n=41) | 50.0 [0.0-100.0] (n=2) | 106 |
| Financial report | TL | 68.3 [54.5-78.0] (n=60) | 44.4 [11.1-77.8] (n=9) | - (n=0) | 69 |
| Financial report | TLV | 76.7 [71.0-83.9] (n=60) | 42.9 [16.7-66.7] (n=7) | - (n=0) | 67 |
| Financial report | V | 47.6 [33.9-62.3] (n=63) | 22.0 [13.1-33.3] (n=41) | 0.0 [0.0-0.0] (n=3) | 107 |
| Guidebook | T | 41.1 [26.0-58.3] (n=73) | 37.5 [17.8-57.9] (n=32) | 0.0 [0.0-0.0] (n=15) | 120 |
| Guidebook | TL | 44.4 [30.4-57.9] (n=72) | 32.3 [12.0-48.6] (n=31) | 0.0 [0.0-0.0] (n=12) | 115 |
| Guidebook | TLV | 58.3 [44.1-71.4] (n=72) | 41.9 [19.2-63.2] (n=31) | 28.6 [0.0-66.7] (n=7) | 110 |
| Guidebook | V | 54.8 [41.4-67.5] (n=73) | 37.5 [17.2-55.3] (n=32) | 30.8 [7.7-54.5] (n=13) | 118 |
| Research report / Introduction | T | 28.0 [17.3-39.8] (n=107) | 17.1 [9.1-26.7] (n=70) | 9.4 [0.0-22.6] (n=32) | 209 |
| Research report / Introduction | TL | 32.7 [21.9-43.1] (n=107) | 24.6 [14.5-35.6] (n=69) | 7.7 [0.0-20.8] (n=26) | 202 |
| Research report / Introduction | TLV | 67.3 [54.9-77.8] (n=107) | 35.3 [23.3-47.4] (n=68) | 18.2 [0.0-40.0] (n=11) | 186 |
| Research report / Introduction | V | 64.5 [53.2-73.8] (n=107) | 30.0 [17.2-42.5] (n=70) | 23.3 [7.1-41.2] (n=30) | 207 |
| Tutorial/Workshop | T | 22.2 [8.9-34.8] (n=63) | 0.0 [0.0-0.0] (n=27) | 0.0 [0.0-0.0] (n=19) | 109 |
| Tutorial/Workshop | TL | 52.4 [38.5-65.5] (n=63) | 40.7 [27.3-52.0] (n=27) | 38.9 [17.6-57.1] (n=18) | 108 |
| Tutorial/Workshop | TLV | 85.7 [76.9-93.9] (n=63) | 61.5 [42.8-78.6] (n=26) | 73.3 [50.0-92.9] (n=15) | 104 |
| Tutorial/Workshop | V | 81.0 [71.9-89.5] (n=63) | 63.0 [43.5-79.2] (n=27) | 47.1 [26.7-66.7] (n=17) | 107 |
| **All** | T | 37.2 [31.1-43.2] (n=479) | 28.6 [22.3-35.0] (n=245) | 16.3 [7.7-26.3] (n=98) | 822 |
| **All** | TL | 44.6 [38.7-50.2] (n=473) | 34.7 [27.7-41.9] (n=199) | 23.8 [14.1-33.7] (n=80) | 752 |
| **All** | TLV | 64.0 [58.4-69.5] (n=472) | 42.3 [34.7-49.8] (n=189) | 48.9 [32.6-63.8] (n=47) | 708 |
| **All** | V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 33.3 [24.2-42.9] (n=99) | 825 |
| n (per col) | - | 1904 | 879 | 324 | - |

### Integration cross-tab: accuracy by evidence source, rung, and evidence-page bucket (oracle pages)

> **swept**: evidence source × rung × evidence-page bucket (1 / 2 / 3+) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail · **multi-source questions**: counted once in every source they cite, so the blocks overlap; the All rows pool each question once and are not a column sum

_The evidence-source companion to the doc_type integration cross-tab: same buckets, same rungs, the modality a question draws on replacing the document class. Buckets are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it); zero-evidence questions are dropped. 3+ merges the finer 3 / 4-5 / 6+ buckets of the integration-detail table. A question can cite several sources (e.g. Chart + Table) and is counted in each one it cites, so the source blocks overlap and their n do not sum to the corpus. The bolded All rows pool every question exactly once and are therefore NOT a column sum of the blocks above them. Every cell carries its own n: OOM attrition is rung-dependent at high page counts (worst on TLV), so a thin cell reads as survivorship, not robustness — check the n before quoting the cell. Read the 3+ column for trend, not precision: crossed with five sources it falls to single digits in places._

| evidence_source | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 [42.9-85.7] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| (none) | TL | 78.6 [53.8-100.0] (n=14) | 0.0 [0.0-0.0] (n=3) | - (n=0) | 17 |
| (none) | TLV | 85.7 [61.5-100.0] (n=14) | 0.0 [0.0-0.0] (n=3) | - (n=0) | 17 |
| (none) | V | 57.1 [33.3-80.0] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| Chart | T | 20.4 [12.4-29.7] (n=98) | 18.6 [9.2-29.8] (n=59) | 5.9 [0.0-18.8] (n=17) | 174 |
| Chart | TL | 17.3 [10.0-25.3] (n=98) | 22.8 [11.1-35.9] (n=57) | 18.8 [0.0-40.0] (n=16) | 171 |
| Chart | TLV | 58.2 [44.8-69.2] (n=98) | 34.5 [21.4-47.3] (n=55) | 40.0 [0.0-80.0] (n=5) | 158 |
| Chart | V | 57.1 [44.9-68.1] (n=98) | 33.9 [21.0-48.3] (n=59) | 20.0 [0.0-40.0] (n=15) | 172 |
| Figure | T | 18.2 [12.1-25.3] (n=165) | 12.9 [5.6-22.1] (n=70) | 8.7 [0.0-18.8] (n=46) | 281 |
| Figure | TL | 24.7 [17.8-31.8] (n=166) | 20.6 [10.6-31.0] (n=68) | 17.9 [8.1-28.6] (n=39) | 273 |
| Figure | TLV | 49.4 [40.9-58.1] (n=166) | 35.4 [21.9-48.6] (n=65) | 53.6 [33.3-69.2] (n=28) | 259 |
| Figure | V | 45.2 [36.5-52.8] (n=166) | 37.1 [25.0-48.7] (n=70) | 32.6 [18.6-46.0] (n=46) | 282 |
| Generalized-text (Layout) | T | 34.5 [18.9-50.0] (n=55) | 32.4 [17.5-51.4] (n=34) | 8.3 [0.0-21.7] (n=24) | 113 |
| Generalized-text (Layout) | TL | 48.2 [35.4-62.1] (n=56) | 34.4 [17.9-50.0] (n=32) | 26.3 [5.6-47.4] (n=19) | 107 |
| Generalized-text (Layout) | TLV | 64.3 [51.9-76.9] (n=56) | 41.9 [24.0-58.8] (n=31) | 55.6 [12.5-88.9] (n=9) | 96 |
| Generalized-text (Layout) | V | 62.5 [48.9-75.5] (n=56) | 41.2 [27.3-55.3] (n=34) | 34.8 [13.6-56.0] (n=23) | 113 |
| Pure-text (Plain-text) | T | 46.8 [36.5-57.7] (n=154) | 34.4 [22.7-46.7] (n=93) | 21.2 [6.2-38.7] (n=33) | 280 |
| Pure-text (Plain-text) | TL | 56.2 [46.0-66.2] (n=153) | 42.5 [30.8-53.9] (n=87) | 26.7 [7.7-45.2] (n=30) | 270 |
| Pure-text (Plain-text) | TLV | 66.4 [55.3-76.1] (n=152) | 49.4 [37.1-62.5] (n=83) | 35.3 [13.3-58.8] (n=17) | 252 |
| Pure-text (Plain-text) | V | 55.8 [46.2-66.4] (n=154) | 30.9 [20.0-42.2] (n=94) | 34.3 [18.7-50.0] (n=35) | 283 |
| Table | T | 49.0 [38.6-58.5] (n=104) | 32.0 [24.0-40.6] (n=97) | 45.5 [18.2-72.7] (n=11) | 212 |
| Table | TL | 69.1 [59.8-77.1] (n=97) | 39.6 [26.6-53.8] (n=53) | 50.0 [0.0-100.0] (n=4) | 154 |
| Table | TLV | 70.8 [62.2-78.9] (n=96) | 42.6 [28.8-56.5] (n=47) | 50.0 [0.0-100.0] (n=4) | 147 |
| Table | V | 51.0 [41.7-59.6] (n=104) | 25.5 [17.2-36.3] (n=98) | 27.3 [9.1-54.5] (n=11) | 213 |
| **All** | T | 37.2 [31.1-43.2] (n=479) | 28.6 [22.3-35.0] (n=245) | 16.3 [7.7-26.3] (n=98) | 822 |
| **All** | TL | 44.6 [38.7-50.2] (n=473) | 34.7 [27.7-41.9] (n=199) | 23.8 [14.1-33.7] (n=80) | 752 |
| **All** | TLV | 64.0 [58.4-69.5] (n=472) | 42.3 [34.7-49.8] (n=189) | 48.9 [32.6-63.8] (n=47) | 708 |
| **All** | V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 33.3 [24.2-42.9] (n=99) | 825 |
| n (per col) | - | 1904 | 879 | 324 | - |

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page_set condition (sufficiency / robustness) × ranking source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **pivot**: all-gold row loaded from g1-representation-full (oracle, hop=multi) by the builder · **status**: empty until the G5 runs are generated + judged

_Rows group on the pageset condition grammar (ranking source, gold rule, distractor count); the robustness gold-count BLOCKS come from the corpus gold-page annotation (the +k design filters questions by exact gold count and feeds ALL their gold pages, so the block is a property of the question, not the rule). Each block's d=0 baseline is the bolded oracle row above it: all gold + no distractors IS the oracle condition, loaded from the G1 cache over the same questions, so the baseline is exact and was never re-generated. Read DOWN a block for the dilution slope at constant evidence; blocks are not comparable to each other (evidence and length both differ). Sufficiency rows withhold or isolate ONE gold page by the named ranker's ordering, on the hop=multi pool, and read against the bolded multi-pool oracle row. Per-cell n is load-bearing: OOM attrition is rung-dependent._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 25.1 [19.5-30.5] (n=343) | 31.5 [25.5-37.7] (n=279) | 43.6 [36.0-50.4] (n=236) | 34.2 [28.5-40.2] (n=345) | 1203 |
| drop bottom 1 | bm25 | 10.2 [7.1-14.3] (n=352) | 11.4 [7.9-14.9] (n=352) | 15.9 [12.2-20.8] (n=352) | 13.4 [9.7-17.7] (n=352) | 1408 |
| drop bottom 1 | colqwen3 | 11.4 [8.0-15.1] (n=352) | 13.4 [9.7-17.5] (n=352) | 18.5 [13.7-24.0] (n=352) | 15.1 [10.9-19.8] (n=352) | 1408 |
| drop top 1 | bm25 | 11.9 [8.3-16.0] (n=352) | 13.6 [10.3-17.5] (n=352) | 15.9 [12.1-19.8] (n=352) | 14.2 [10.5-17.8] (n=352) | 1408 |
| drop top 1 | colqwen3 | 10.8 [7.5-15.0] (n=352) | 11.1 [7.9-14.8] (n=352) | 15.9 [12.2-19.9] (n=352) | 13.9 [10.4-17.6] (n=352) | 1408 |
| keep bottom 1 | bm25 | 9.1 [5.9-12.8] (n=352) | 9.9 [7.0-13.4] (n=352) | 11.1 [7.9-14.2] (n=352) | 10.5 [7.8-13.6] (n=352) | 1408 |
| keep bottom 1 | colqwen3 | 9.4 [6.4-13.1] (n=352) | 9.7 [6.7-13.2] (n=352) | 10.5 [7.5-14.0] (n=352) | 9.9 [7.2-13.2] (n=352) | 1408 |
| keep top 1 | bm25 | 9.1 [6.2-12.8] (n=352) | 8.5 [5.8-11.7] (n=352) | 12.2 [9.0-16.6] (n=352) | 9.4 [6.2-13.4] (n=352) | 1408 |
| keep top 1 | colqwen3 | 9.1 [6.1-12.4] (n=352) | 10.2 [6.9-14.1] (n=352) | 12.8 [8.9-17.6] (n=352) | 11.1 [7.5-15.4] (n=352) | 1408 |
| **oracle (gold 1, d=0)** | - | 37.2 [31.1-43.2] (n=479) | 44.6 [38.7-50.2] (n=473) | 64.0 [58.4-69.5] (n=472) | 55.0 [49.7-60.2] (n=480) | 1904 |
| gold 1 + 1 distractors | bm25 | 39.7 [33.5-45.7] (n=474) | 46.8 [41.3-52.4] (n=474) | 64.6 [59.2-69.5] (n=474) | 57.4 [52.1-62.4] (n=474) | 1896 |
| gold 1 + 1 distractors | colqwen3 | 39.5 [33.7-45.2] (n=474) | 48.9 [43.3-54.1] (n=474) | 63.7 [58.7-68.6] (n=474) | 55.7 [50.5-60.4] (n=474) | 1896 |
| gold 1 + 2 distractors | bm25 | 40.9 [34.8-47.2] (n=474) | 46.2 [40.8-51.7] (n=474) | 64.8 [59.6-69.9] (n=474) | 53.6 [48.4-58.7] (n=474) | 1896 |
| gold 1 + 2 distractors | colqwen3 | 38.8 [32.3-45.0] (n=474) | 47.9 [42.0-53.4] (n=474) | 64.3 [59.5-68.7] (n=474) | 56.1 [51.2-61.4] (n=474) | 1896 |
| **oracle (gold 2, d=0)** | - | 28.6 [22.3-35.0] (n=245) | 34.7 [27.7-41.9] (n=199) | 42.3 [34.7-49.8] (n=189) | 34.6 [27.9-41.2] (n=246) | 879 |
| gold 2 + 1 distractors | bm25 | 29.0 [22.2-35.8] (n=241) | 34.9 [29.0-40.6] (n=241) | 39.0 [31.7-46.5] (n=241) | 34.0 [27.2-41.0] (n=241) | 964 |
| gold 2 + 1 distractors | colqwen3 | 25.7 [19.6-32.0] (n=241) | 34.0 [27.8-40.7] (n=241) | 38.6 [31.2-46.3] (n=241) | 34.4 [27.7-41.7] (n=241) | 964 |
| gold 2 + 2 distractors | bm25 | 27.0 [20.7-33.5] (n=241) | 32.8 [26.2-39.2] (n=241) | 39.8 [32.7-46.8] (n=241) | 34.4 [28.2-40.9] (n=241) | 964 |
| gold 2 + 2 distractors | colqwen3 | 25.3 [18.9-32.2] (n=241) | 33.6 [27.3-40.3] (n=241) | 35.7 [28.3-43.0] (n=241) | 32.4 [25.9-39.6] (n=241) | 964 |
| **oracle (gold 3, d=0)** | - | 25.0 [10.2-41.5] (n=40) | 33.3 [18.2-50.0] (n=33) | 42.9 [25.9-61.5] (n=28) | 42.5 [24.3-57.8] (n=40) | 141 |
| gold 3 + 1 distractors | bm25 | 22.5 [9.8-38.5] (n=40) | 35.0 [20.5-50.0] (n=40) | 50.0 [34.1-65.9] (n=40) | 37.5 [21.4-54.1] (n=40) | 160 |
| gold 3 + 1 distractors | colqwen3 | 22.5 [7.9-39.0] (n=40) | 40.0 [23.7-56.8] (n=40) | 45.0 [28.2-61.0] (n=40) | 40.0 [25.0-54.1] (n=40) | 160 |
| gold 3 + 2 distractors | bm25 | 17.5 [5.1-32.5] (n=40) | 37.5 [21.1-53.8] (n=40) | 52.5 [35.1-67.4] (n=40) | 40.0 [25.6-55.0] (n=40) | 160 |
| gold 3 + 2 distractors | colqwen3 | 27.5 [12.8-43.9] (n=40) | 37.5 [22.5-53.7] (n=40) | 40.0 [23.7-55.8] (n=40) | 30.0 [16.2-44.2] (n=40) | 160 |
| n (per col) | - | 5836 | 5836 | 5836 | 5836 | - |

### Hallucination: abstention rate on unanswerable questions by prompt

> **swept**: prompt_mode (none / generic / targeted; legacy names of the six-mode set) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

| prompt_condition | abstention_rate | answered | n |
| --- | --- | --- | --- |
| none | 16.9 | 750 | 902 |
| generic | 10.7 | 802 | 898 |
| targeted | 80.7 | 173 | 898 |
| n (per col) | - | - | - |

### Mined: abstention rate on unanswerable questions by prompt mode and doc_type

> **swept**: prompt_mode × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

| doc_type | none | generic | targeted | n_none | n_generic | n_targeted |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 7.3 | 4.7 | 73.6 | 150 | 148 | 148 |
| Administration/Industry file | 15.9 | 14.3 | 71.4 | 63 | 63 | 63 |
| Brochure | 13.0 | 9.8 | 65.2 | 92 | 92 | 92 |
| Financial report | 8.0 | 8.0 | 72.0 | 25 | 25 | 25 |
| Guidebook | 16.9 | 7.1 | 87.9 | 142 | 141 | 141 |
| Research report / Introduction | 22.0 | 11.2 | 82.6 | 322 | 321 | 321 |
| Tutorial/Workshop | 20.4 | 21.3 | 96.3 | 108 | 108 | 108 |
| n (per col) | 902 | 898 | 898 | - | - | - |

## RQ2 — Deployment feasibility (what can be run)

### Reasoner: precision / scale / matched budget / family / reasoning variant

> **swept**: reasoner block (precision / scale / matched budget / family / reasoning variant) · **dataset**: mmlongbench · **scan**: mixed pools by run; compare within a block · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **memory**: weight footprint, not peak VRAM · **note**: thinking/llama/32B rows appear when their runs land

_Weight footprint (MB, `~` = derived for quantized variants) replaces peak VRAM: the measured figure is device-0 only. Every accuracy cell carries its own n because OOM attrition is not random with respect to the question pool: it tracks document length and page count, which track the multi-page questions, so a thin cell compares an easier surviving subset. The reasoning-variant block reports M−S per rung (multi minus single accuracy, negative = multi worse), NOT pooled accuracy: the Thinking variant's value is entirely its hop-split behaviour. Blocks share the 8B bf16 baseline row wherever it is the comparison point; pool composition differs by run (scan filters), so compare within a block._

| block | model_spec | weights_mb | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| precision | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.6] (n=831) | 39.4 [35.2-43.8] (n=761) | 56.8 [52.0-61.2] (n=717) | 45.9 [42.0-50.0] (n=834) | 3143 |
| precision | qwen3vl-8b-local-8bit | 10285~ | 32.4 [27.5-37.1] (n=837) | 39.4 [35.1-44.0] (n=786) | 57.5 [52.8-61.7] (n=743) | 46.0 [41.9-50.3] (n=839) | 3205 |
| precision | qwen3vl-8b-local-4bit | 6775~ | 31.8 [27.1-36.6] (n=839) | 40.2 [36.3-44.1] (n=800) | 55.1 [50.6-59.4] (n=762) | 45.6 [41.2-49.9] (n=843) | 3244 |
| scale | qwen3vl-2b-local | 4255 | 24.6 [20.7-28.2] (n=843) | 32.1 [28.6-35.4] (n=833) | 39.2 [35.6-42.8] (n=821) | 32.0 [28.4-35.7] (n=845) | 3342 |
| scale | qwen3vl-4b-local | 8876 | 32.4 [27.4-37.2] (n=839) | 39.8 [35.6-44.0] (n=800) | 53.4 [49.4-57.4] (n=761) | 42.3 [38.1-46.8] (n=842) | 3242 |
| scale | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.6] (n=831) | 39.4 [35.2-43.8] (n=761) | 56.8 [52.0-61.2] (n=717) | 45.9 [42.0-50.0] (n=834) | 3143 |
| scale | qwen3vl-32b-local | 66715 | 35.5 [30.4-40.6] (n=847) | 43.9 [39.9-48.1] (n=847) | 59.6 [55.2-63.9] (n=846) | 56.7 [52.5-60.9] (n=847) | 3387 |
| matched budget (~17 GB) | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.6] (n=831) | 39.4 [35.2-43.8] (n=761) | 56.8 [52.0-61.2] (n=717) | 45.9 [42.0-50.0] (n=834) | 3143 |
| matched budget (~17 GB) | qwen3vl-32b-local-4bit | 19951~ | 37.0 [32.0-41.4] (n=847) | 42.1 [37.9-46.2] (n=847) | 59.1 [54.7-63.2] (n=847) | 52.3 [47.9-57.0] (n=847) | 3388 |
| family | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.6] (n=831) | 39.4 [35.2-43.8] (n=761) | 56.8 [52.0-61.2] (n=717) | 45.9 [42.0-50.0] (n=834) | 3143 |
| family | internvl3-8b-local | 15889 | 19.6 [16.1-23.1] (n=831) | 27.3 [23.8-31.1] (n=762) | 34.6 [30.2-38.9] (n=742) | 24.1 [20.2-28.4] (n=845) | 3180 |
| reasoning variant (M−S) | qwen3vl-8b-local | 17534 | -12.1 (nS=479, nM=343) | -13.1 (nS=473, nM=279) | -20.3 (nS=472, nM=236) | -20.8 (nS=480, nM=345) | 3143 |
| n (per col) | - | - | 6714 | 6436 | 6239 | 6742 | - |

### Scale: accuracy vs VRAM/latency across reasoner specs

> **swept**: reasoner_spec (size + family) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 8b bf16 baseline from the representation run

_latency_ms is end-to-end and decode-inflated (~20x by the verbose-answer change); prefill_ms is the clean cost signal, and reads `-` for a backend that cannot measure a prefill/decode split. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| model_spec | T | TL | TLV | V | weights_mb | peak_vram_mb | prefill_ms | latency_ms | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| internvl3-8b-local | 19.6 [16.1-23.1] | 27.3 [23.8-31.1] | 34.6 [30.2-38.9] | 24.1 [20.2-28.4] | 15889 | 13303 | - | 5261 | 3180 |
| qwen3vl-2b-local | 24.6 [20.7-28.2] | 32.1 [28.6-35.4] | 39.2 [35.6-42.8] | 32.0 [28.4-35.7] | 4255 | 14264 | 18234 | 24047 | 3342 |
| qwen3vl-4b-local | 32.4 [27.4-37.2] | 39.8 [35.6-44.0] | 53.4 [49.4-57.4] | 42.3 [38.1-46.8] | 8876 | 15058 | 18126 | 25041 | 3242 |
| qwen3vl-8b-local | 31.9 [27.1-36.6] | 39.4 [35.2-43.8] | 56.8 [52.0-61.2] | 45.9 [42.0-50.0] | 17534 | 14240 | 14499 | 21045 | 3143 |
| n (per col) | 3344 | 3156 | 3041 | 3366 | - | - | - | - | - |

### Mined: quantization sensitivity (accuracy + VRAM delta) by doc_type

> **swept**: quantization (bf16 / 8bit / 4bit) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 16-bit baseline from the representation run

_delta is vs the 16-bit baseline of the same model; blank when no baseline is in the cache._

| doc_type | quant | accuracy | vram_mb | acc_delta_vs_16bit | vram_delta_mb | n |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 4bit | 37.2 | 12190 | -0.1 | -1702 | 567 |
| Academic paper | 8bit | 37.6 | 12115 | +0.3 | -1777 | 561 |
| Academic paper | 16bit | 37.3 | 13892 | +0.0 | +0 | 550 |
| Administration/Industry file | 4bit | 59.0 | 10790 | +1.1 | -2761 | 239 |
| Administration/Industry file | 8bit | 59.1 | 11855 | +1.1 | -1696 | 237 |
| Administration/Industry file | 16bit | 57.9 | 13551 | +0.0 | +0 | 233 |
| Brochure | 4bit | 37.6 | 11254 | +0.6 | -1930 | 306 |
| Brochure | 8bit | 37.4 | 12963 | +0.4 | -221 | 305 |
| Brochure | 16bit | 37.0 | 13184 | +0.0 | +0 | 300 |
| Financial report | 4bit | 50.9 | 12488 | -2.1 | -1198 | 391 |
| Financial report | 8bit | 52.7 | 12895 | -0.3 | -791 | 374 |
| Financial report | 16bit | 53.0 | 13686 | +0.0 | +0 | 353 |
| Guidebook | 4bit | 44.0 | 12670 | +1.4 | -656 | 473 |
| Guidebook | 8bit | 43.8 | 11269 | +1.3 | -2057 | 468 |
| Guidebook | 16bit | 42.5 | 13326 | +0.0 | +0 | 463 |
| Research report / Introduction | 4bit | 35.2 | 13555 | -1.4 | -686 | 822 |
| Research report / Introduction | 8bit | 35.8 | 13201 | -0.7 | -1040 | 815 |
| Research report / Introduction | 16bit | 36.6 | 14240 | +0.0 | +0 | 804 |
| Tutorial/Workshop | 4bit | 51.6 | 11490 | +0.2 | -2046 | 446 |
| Tutorial/Workshop | 8bit | 52.8 | 10835 | +1.4 | -2701 | 445 |
| Tutorial/Workshop | 16bit | 51.4 | 13536 | +0.0 | +0 | 440 |
| n (per col) | - | - | - | - | - | - |

### Quantization sensitivity (overall): accuracy per rung + VRAM per quant

> **view**: summary — pooled across all doc_types · **swept**: quantization (bf16 / 8bit / 4bit) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 16-bit baseline from the representation run

_One row per quantization level, so accuracy is directly comparable across the rungs within a level. Each rung cell is that cell's accuracy with, in parentheses, its delta against the 16-bit baseline AT THE SAME RUNG, which is what isolates the quantization effect from the rung mix. The trailing columns are that level's aggregates over all its rows, not sums or means of the rung columns. `overall acc` is its pooled correctness rate and `acc_delta_vs_16bit` compares pooled to pooled; OOM attrition differs by rung and by level (16-bit TLV survives 717 cells against 4-bit's 762), so the pooled figures mix slightly different rung compositions and the per-rung cells are the cleaner comparison. `weights_mb` is WEIGHTS ONLY, with no activations and no device-0 truncation: it is a static property of the checkpoint (summed safetensors tensor bytes), so it needs no re-run and is complete. The 16-bit figure is exact; a trailing `~` marks a derived figure, computed by applying bitsandbytes' layout to the real tensor shapes (int8 or packed NF4 plus double-quant constants for the 2D Linear weights, compute dtype for embeddings, lm_head, norms and biases) rather than measured on a loaded model. Regenerate with ops/scripts/model_weight_sizes.py. `vram_mb` is the MAXIMUM peak over the level's rows, not an average, because it is a headroom figure and the binding cell is what matters. Compare it against `weights_mb` only with the caveat below in mind. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| quant | T | TL | TLV | V | overall acc | weights_mb | vram_mb (max) | acc_delta_vs_16bit | vram_delta_mb | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 4bit | 31.8 (-0.1) | 40.2 (+0.8) | 55.1 (-1.6) | 45.6 (-0.4) | 42.9 | 6775~ | 13555 | -0.2 | -686 | 3244 |
| 8bit | 32.4 (+0.5) | 39.4 (+0.0) | 57.5 (+0.7) | 46.0 (+0.1) | 43.5 | 10285~ | 13201 | +0.4 | -1040 | 3205 |
| 16bit | 31.9 (+0.0) | 39.4 (+0.0) | 56.8 (+0.0) | 45.9 (+0.0) | 43.1 | 17534 | 14240 | +0.0 | +0 | 3143 |
| n (per col) | 2507 | 2347 | 2222 | 2516 | - | - | - | - | - | - |

### Mined: peak-VRAM headroom vs the 16 GB V100 ceiling

> **swept**: spec / rung / resolution (peak VRAM) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: pooled across all G1 runs

_headroom_mb = 16384 - peak_vram_mb_max; a negative value means the config OOMs a V100. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| model_spec | rung | resolution | peak_vram_mb_max | peak_vram_mb_p95 | headroom_mb | n |
| --- | --- | --- | --- | --- | --- | --- |
| internvl3-8b-local | T | med | 12848 | 9454 | 3536 | 831 |
| internvl3-8b-local | TL | med | 13170 | 10671 | 3214 | 762 |
| internvl3-8b-local | TLV | med | 13303 | 11167 | 3081 | 742 |
| internvl3-8b-local | V | med | 11994 | 7927 | 4390 | 845 |
| qwen3vl-2b-local | T | med | 11610 | 3647 | 4774 | 843 |
| qwen3vl-2b-local | TL | med | 14264 | 6591 | 2120 | 833 |
| qwen3vl-2b-local | TLV | med | 14192 | 8528 | 2192 | 821 |
| qwen3vl-2b-local | V | med | 10111 | 3249 | 6273 | 845 |
| qwen3vl-4b-local | T | med | 15058 | 7116 | 1326 | 839 |
| qwen3vl-4b-local | TL | med | 14880 | 10400 | 1504 | 800 |
| qwen3vl-4b-local | TLV | med | 14897 | 11178 | 1487 | 761 |
| qwen3vl-4b-local | V | med | 15021 | 6489 | 1363 | 842 |
| qwen3vl-8b-local | T | med | 13862 | 10225 | 2522 | 831 |
| qwen3vl-8b-local | TL | med | 14240 | 11477 | 2144 | 761 |
| qwen3vl-8b-local | TLV | high | 14033 | 12429 | 2351 | 681 |
| qwen3vl-8b-local | TLV | low | 13974 | 11904 | 2410 | 732 |
| qwen3vl-8b-local | TLV | med | 14143 | 12134 | 2241 | 1436 |
| qwen3vl-8b-local | V | high | 12824 | 9839 | 3560 | 810 |
| qwen3vl-8b-local | V | low | 13321 | 8769 | 3063 | 844 |
| qwen3vl-8b-local | V | med | 14115 | 9315 | 2269 | 1668 |
| qwen3vl-8b-local-4bit | T | med | 12637 | 4764 | 3747 | 839 |
| qwen3vl-8b-local-4bit | TL | med | 12276 | 8015 | 4108 | 800 |
| qwen3vl-8b-local-4bit | TLV | med | 12809 | 8857 | 3575 | 762 |
| qwen3vl-8b-local-4bit | V | med | 13555 | 4179 | 2829 | 843 |
| qwen3vl-8b-local-8bit | T | med | 12963 | 6380 | 3421 | 837 |
| qwen3vl-8b-local-8bit | TL | med | 13201 | 8377 | 3183 | 786 |
| qwen3vl-8b-local-8bit | TLV | med | 12731 | 9209 | 3653 | 743 |
| qwen3vl-8b-local-8bit | V | med | 11341 | 5264 | 5043 | 839 |
| n (per col) | - | - | - | - | - | - |

### VRAM headroom (overall): worst-case peak per model_spec

> **view**: summary — pooled across all doc_types · **swept**: spec / rung / resolution (peak VRAM) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: pooled across all G1 runs

_peak = max over all rungs/resolutions; negative headroom means the spec OOMs a V100 at its heaviest config. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| model_spec | peak_vram_mb_max | headroom_mb | n |
| --- | --- | --- | --- |
| internvl3-8b-local | 13303 | 3081 | 3180 |
| qwen3vl-2b-local | 14264 | 2120 | 3342 |
| qwen3vl-4b-local | 15058 | 1326 | 3242 |
| qwen3vl-8b-local | 14240 | 2144 | 7763 |
| qwen3vl-8b-local-4bit | 13555 | 2829 | 3244 |
| qwen3vl-8b-local-8bit | 13201 | 3183 | 3205 |
| n (per col) | - | - | - |

### Mined: OOM rate by rung, resolution, and pages-fed

> **swept**: rung / resolution / pages-fed (OOM rate) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: OOM from status rows, pooled across all G1 runs

_rate = oom cells / all cells in the group, over the 16 GB V100 runs._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
| T | med | 1 | 0.1 | 2 | 2928 |
| T | med | 2-5 | 0.8 | 16 | 1896 |
| T | med | 6-10 | 16.7 | 29 | 174 |
| T | med | 11-20 | 50.0 | 15 | 30 |
| T | med | 21+ | 0.0 | 0 | 12 |
| T | med | 0 | 0.0 | 0 | 42 |
| TL | med | 1 | 0.7 | 21 | 2928 |
| TL | med | 2-5 | 13.0 | 246 | 1896 |
| TL | med | 6-10 | 27.0 | 47 | 174 |
| TL | med | 11-20 | 46.7 | 14 | 30 |
| TL | med | 21+ | 100.0 | 12 | 12 |
| TL | med | 0 | 0.0 | 0 | 42 |
| TLV | high | 1 | 2.7 | 13 | 488 |
| TLV | high | 2-5 | 37.0 | 117 | 316 |
| TLV | high | 6-10 | 100.0 | 29 | 29 |
| TLV | high | 11-20 | 100.0 | 5 | 5 |
| TLV | high | 21+ | 100.0 | 2 | 2 |
| TLV | high | 0 | 0.0 | 0 | 7 |
| TLV | low | 1 | 1.6 | 8 | 488 |
| TLV | low | 2-5 | 25.9 | 82 | 316 |
| TLV | low | 6-10 | 62.1 | 18 | 29 |
| TLV | low | 11-20 | 100.0 | 5 | 5 |
| TLV | low | 21+ | 100.0 | 2 | 2 |
| TLV | low | 0 | 0.0 | 0 | 7 |
| TLV | med | 1 | 1.0 | 33 | 3416 |
| TLV | med | 2-5 | 20.7 | 458 | 2212 |
| TLV | med | 6-10 | 61.6 | 125 | 203 |
| TLV | med | 11-20 | 97.1 | 34 | 35 |
| TLV | med | 21+ | 100.0 | 14 | 14 |
| TLV | med | 0 | 0.0 | 0 | 49 |
| V | high | 1 | 0.0 | 0 | 488 |
| V | high | 2-5 | 0.3 | 1 | 316 |
| V | high | 6-10 | 100.0 | 29 | 29 |
| V | high | 11-20 | 100.0 | 5 | 5 |
| V | high | 21+ | 100.0 | 2 | 2 |
| V | high | 0 | 0.0 | 0 | 7 |
| V | low | 1 | 0.0 | 0 | 488 |
| V | low | 2-5 | 0.0 | 0 | 316 |
| V | low | 6-10 | 0.0 | 0 | 29 |
| V | low | 11-20 | 20.0 | 1 | 5 |
| V | low | 21+ | 100.0 | 2 | 2 |
| V | low | 0 | 0.0 | 0 | 7 |
| V | med | 1 | 0.0 | 0 | 3416 |
| V | med | 2-5 | 0.0 | 0 | 2212 |
| V | med | 6-10 | 6.4 | 13 | 203 |
| V | med | 11-20 | 57.1 | 20 | 35 |
| V | med | 21+ | 100.0 | 14 | 14 |
| V | med | 0 | 0.0 | 0 | 49 |
| n (per col) | - | - | - | - | - |

### OOM frontier (overall): OOM rate by rung and resolution

> **view**: summary — pooled across all doc_types · **swept**: rung / resolution / pages-fed (OOM rate) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: OOM from status rows, pooled across all G1 runs

_rate = oom cells / all cells; pooled over page buckets and G1 runs._

| rung | high | low | med | n_total |
| --- | --- | --- | --- | --- |
| T | - | - | 1.2 | 5082 |
| TL | - | - | 6.7 | 5082 |
| TLV | 19.6 | 13.6 | 11.2 | 7623 |
| V | 4.4 | 0.4 | 0.8 | 7623 |
| n (per col) | 1694 | 1694 | 22022 | - |

### Mined: prefill cost per rung per doc_type (clean cost axis)

> **swept**: representation (prefill / input tokens) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

_prefill latency + input tokens are unaffected by the verbose-answer inflation._

| doc_type | rung | prefill_ms | input_tokens | n |
| --- | --- | --- | --- | --- |
| Academic paper | T | 2781 | 1616 | 148 |
| Academic paper | TL | 2940 | 1697 | 130 |
| Academic paper | TLV | 24666 | 4026 | 119 |
| Academic paper | V | 27539 | 3201 | 153 |
| Administration/Industry file | T | 1539 | 867 | 60 |
| Administration/Industry file | TL | 1510 | 860 | 57 |
| Administration/Industry file | TLV | 20710 | 3013 | 55 |
| Administration/Industry file | V | 24313 | 2827 | 61 |
| Brochure | T | 1022 | 565 | 75 |
| Brochure | TL | 1423 | 808 | 76 |
| Brochure | TLV | 27298 | 3523 | 72 |
| Brochure | V | 28097 | 3114 | 77 |
| Financial report | T | 1920 | 1140 | 107 |
| Financial report | TL | 3280 | 1878 | 70 |
| Financial report | TLV | 20855 | 3844 | 68 |
| Financial report | V | 23207 | 2709 | 108 |
| Guidebook | T | 1004 | 557 | 120 |
| Guidebook | TL | 1451 | 828 | 115 |
| Guidebook | TLV | 22818 | 3118 | 110 |
| Guidebook | V | 24237 | 2735 | 118 |
| Research report / Introduction | T | 1197 | 639 | 209 |
| Research report / Introduction | TL | 1520 | 866 | 202 |
| Research report / Introduction | TLV | 29156 | 3503 | 186 |
| Research report / Introduction | V | 34775 | 3530 | 207 |
| Tutorial/Workshop | T | 272 | 53 | 112 |
| Tutorial/Workshop | TL | 719 | 371 | 111 |
| Tutorial/Workshop | TLV | 32465 | 3326 | 107 |
| Tutorial/Workshop | V | 33952 | 3247 | 110 |
| **all doc_types** | **T** | **1428** | **797** | **831** |
| **all doc_types** | **TL** | **1787** | **1017** | **761** |
| **all doc_types** | **TLV** | **26311** | **3501** | **717** |
| **all doc_types** | **V** | **28968** | **3124** | **834** |
| n (per col) | - | - | - | - |

## RQ3 — Recoverable loss (which levers help)

### Resolution sweep: TLV/V accuracy by doc_type and preset

> **swept**: visual_resolution (low / med / high) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **representation**: TLV/V only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| doc_type | rung | low | med | high | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | TLV | 38.5 [27.2-47.5] | 42.9 [32.3-52.2] | 50.9 [41.6-59.2] | 347 |
| Academic paper | V | 19.5 [12.7-26.7] | 30.7 [22.8-38.2] | 38.9 [29.9-47.8] | 456 |
| Administration/Industry file | TLV | 66.1 [51.8-80.9] | 72.7 [63.5-85.7] | 72.2 [60.0-86.0] | 165 |
| Administration/Industry file | V | 42.9 [31.1-53.3] | 52.5 [44.6-63.0] | 63.3 [53.2-73.8] | 184 |
| Brochure | TLV | 40.5 [28.9-52.2] | 43.1 [28.6-58.0] | 48.6 [35.1-63.2] | 216 |
| Brochure | V | 39.0 [28.0-51.3] | 45.5 [32.5-58.4] | 49.3 [36.8-63.0] | 229 |
| Financial report | TLV | 72.1 [62.7-81.0] | 72.1 [66.0-79.4] | 71.0 [66.2-75.3] | 198 |
| Financial report | V | 21.3 [11.9-28.6] | 36.1 [29.5-43.4] | 46.3 [38.9-53.2] | 324 |
| Guidebook | TLV | 47.3 [34.3-60.6] | 50.9 [37.5-64.2] | 54.3 [39.8-69.5] | 327 |
| Guidebook | V | 38.7 [29.1-47.7] | 47.5 [35.5-59.7] | 48.7 [37.0-60.5] | 354 |
| Research report / Introduction | TLV | 45.8 [35.7-54.5] | 53.7 [43.8-62.2] | 55.6 [44.6-64.7] | 558 |
| Research report / Introduction | V | 38.4 [29.4-46.6] | 48.3 [38.3-56.6] | 51.3 [41.9-58.7] | 613 |
| Tutorial/Workshop | TLV | 71.8 [63.1-80.2] | 76.6 [69.8-83.2] | 76.0 [69.6-81.7] | 321 |
| Tutorial/Workshop | V | 74.1 [67.7-81.2] | 69.1 [62.5-75.5] | 73.6 [66.7-80.2] | 328 |
| **all doc_types** | **TLV** | **52.2 [47.0-56.9]** | **57.0 [52.3-61.6]** | **59.8 [55.2-64.2]** | **2132** |
| **all doc_types** | **V** | **37.9 [33.5-42.6]** | **46.2 [42.1-50.5]** | **51.6 [47.7-55.5]** | **2488** |
| n (per col) | - | 1576 | 1553 | 1491 | - |

### Matched vs cross: accuracy by retrieval modality and doc_type (TLV)

> **swept**: retrieval modality (matched vs cross) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **prompt_mode**: none · **inference arms**: spec ran bge-m3 text / colqwen2.5 vision / joint; BASELINE captions the text arm as bm25 (the config default the spec overrode) — cite the spec · **status**: PROVISIONAL (partial G2 pool)

| doc_type | text | vision | joint | n |
| --- | --- | --- | --- | --- |
| Academic paper | 14.6 [6.4-23.9] | 20.1 [10.4-28.9] | 22.3 [13.1-31.1] | 591 |
| Administration/Industry file | 41.0 [24.5-48.2] | 46.2 [36.4-54.2] | 43.5 [25.0-52.6] | 294 |
| Brochure | 19.4 [8.1-26.7] | 26.7 [22.5-32.8] | 28.1 [23.3-35.0] | 383 |
| Financial report | 15.2 [15.2-15.2] | 31.2 [31.2-31.2] | 44.4 [44.4-44.4] | 130 |
| Guidebook | 28.7 [13.9-43.5] | 33.5 [19.1-45.3] | 36.7 [22.2-48.8] | 558 |
| Research report / Introduction | 16.1 [9.0-24.1] | 34.7 [26.5-42.2] | 34.5 [27.3-40.9] | 1778 |
| Tutorial/Workshop | 29.9 [15.7-45.9] | 59.2 [51.3-70.0] | 62.5 [50.9-78.0] | 577 |
| n (per col) | 1523 | 1538 | 1250 | - |

### Top-k sweep: accuracy vs retrieval depth by modality

> **swept**: retrieval depth k · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **prompt_mode**: none · **inference arms**: spec ran bge-m3 text / colqwen2.5 vision / joint; BASELINE captions the text arm as bm25 (the config default the spec overrode) — cite the spec · **status**: PROVISIONAL (partial G2 pool)

| k | text | vision | joint | n |
| --- | --- | --- | --- | --- |
| 1 | 18.0 [13.1-23.3] | 32.7 [26.7-38.5] | 36.4 [31.5-41.2] | 1779 |
| 3 | 24.3 [18.7-30.5] | 37.6 [32.2-43.3] | 37.6 [31.6-43.7] | 1490 |
| 5 | 22.3 [16.7-29.0] | 38.1 [31.8-44.4] | 36.8 [29.7-44.2] | 1024 |
| 7 | 42.9 [42.9-42.9] | 28.6 [28.6-28.6] | 50.0 [50.0-50.0] | 18 |
| n (per col) | 1523 | 1538 | 1250 | - |

### Routing policies: accuracy vs latency

> **swept**: routing policy · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: assembled from G1 ladder rows + G3 classifier price

_assembled from G1 ladder rows + G3 classifier price. latency_ms is end-to-end and decode-inflated (~20x by the verbose-answer change); prefill_ms is the clean ingestion cost._

| policy | accuracy | prefill_ms | latency_ms | note |
| --- | --- | --- | --- | --- |
| uniform_cheapest_T | 31.9 | 1428 | 7161 |  |
| uniform_strongest_TLV | 56.8 | 26311 | 33013 |  |
| oracle_routing | 51.3 | 14312 | 20876 | per-doc_type frontier rung |
| predicted_routing | 51.3 | 14312 | 49726 | oracle rung choice + classifier latency |
| n (per col) | - | - | - | - |

### Levers: what each inference-time intervention does, where data exists

> **swept**: inference-time lever × effect · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **sources**: each lever row loads its own run_tag(s) in the builder; blank rows await their runs · **retrieval depth**: PROVISIONAL (partial G2 pool)

_One row per lever: the measured baseline, the lever value, and the delta in points, each with its n. A blank row means the lever's run has not landed; a populated row is never imputed across pools. Metrics differ by row (accuracy at the named rung, or abstention rate on the unanswerable pool) and are named per row: read the metric column, not just the delta. The retrieval-depth row is PROVISIONAL (partial G2 pool). The abstention row reads the ORIGINAL three-mode G3 run (targeted vs none); its six-mode re-run replaces it when judged. Deltas across different pools/runs are directional findings, not matched comparisons._

| lever | targets | metric | baseline | lever value | delta | n (base/lever) |
| --- | --- | --- | --- | --- | --- | --- |
| resolution med→high | E3 fidelity | acc @ TLV | 57.0 | 59.8 | +2.7 | 719/681 |
| interleaving TLV→TLVi | E4 reasoning | acc @ TLV | 52.8 | 55.0 | +2.2 | 847/847 |
| CoT prompt (grounded→cot) | E4 reasoning | acc @ TLV | 45.7 | 53.1 | +7.4 | 847/847 |
| extraction (grounded→extract_cot) | E4 reasoning | acc @ TLV | 45.7 | 50.2 | +4.5 | 847/846 |
| abstention prompt (none→targeted) | E5 faithfulness | abstention @ TLV (unanswerable) | 15.9 | 77.7 | +61.8 | 195/193 |
| retrieval depth k1→k5 (vision) | E2 selection | acc @ V (PROVISIONAL) | 28.9 | 36.2 | +7.2 | 304/304 |
| model swap 8B→InternVL3-8B | reasoner | acc @ TLV | 56.8 | 34.6 | -22.1 | 717/742 |
| thinking variant (M−S) | E4 reasoning | M−S @ TLV | - | - | - | - |
| n (per col) | - | - | - | - | - | - |

## Appendix — not mapped to an RQ, retained

### Abstention detection scope: extracted final answer vs whole generation

> **swept**: abstention detection scope (extracted answer vs whole generation) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **prompt_mode**: none · **delimiter**: Answer: (configured by the faithfulness specs)

_Same judged rows, two detection scopes. A positive delta means the whole generation carries abstention wording that the post-delimiter answer drops, so the configured scope reports fewer abstentions._

| prompt_mode | scored (extracted) | whole text | delta | delimiter in answer | n |
| --- | --- | --- | --- | --- | --- |
| none | 13.5 | 16.4 | +2.9 | 230 (24%) | 976 |
| grounded | 10.6 | 10.6 | +0.0 | 0 (0%) | 976 |
| abstain | 79.3 | 79.3 | +0.0 | 0 (0%) | 976 |
| abstain_balanced | 74.5 | 74.5 | +0.0 | 0 (0%) | 976 |
| cot | 10.0 | 19.0 | +8.9 | 893 (91%) | 976 |
| extract_cot | 15.9 | 17.5 | +1.6 | 822 (84%) | 976 |
| n (per col) | - | - | - | - | 5856 |

### Pool coverage: cells the earlier V100 run lost to OOM, recovered on the H100

> **swept**: cell pool coverage (shared with the earlier ladder vs recovered) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none (the condition both runs share)

_`shared cells` are the same question/rung pairs the earlier ladder scored and should reproduce it; `recovered cells` are the ones it never completed. A lower recovered column means the pool the earlier run lost was the harder part of it, so a pooled comparison against the earlier number is not like-for-like._

| rung | earlier run | shared cells | recovered cells | new run (all) | n shared / recovered |
| --- | --- | --- | --- | --- | --- |
| T | 31.9 | 31.9 | 31.2 | 31.9 | 831 / 16 |
| TL | 39.4 | 39.9 | 29.1 | 38.8 | 761 / 86 |
| TLV | 56.8 | 57.0 | 27.7 | 52.5 | 717 / 130 |
| V | 45.9 | 46.0 | 15.4 | 45.6 | 834 / 13 |

### Retrieval accuracy (summary): best-F1 operating point per method

> **view**: summary — pooled across all doc_types · **swept**: retriever × k (page P/R/F1) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

_best_k = the depth k with the highest mean F1 for that method (all doc_types)._

| retriever | modality | best_k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.338 | 0.255 | 0.279 | 847 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.485 | 0.552 | 0.486 | 847 |
| bm25 | text | 1 | 0.295 | 0.222 | 0.242 | 847 |
| bm25\|colmodernvbert | joint | 1 | 0.442 | 0.512 | 0.445 | 847 |
| colmodernvbert | vision | 1 | 0.588 | 0.460 | 0.496 | 847 |
| colqwen2.5 | vision | 1 | 0.633 | 0.488 | 0.528 | 847 |
| colqwen3 | vision | 1 | 0.702 | 0.541 | 0.586 | 847 |
| qwen3-embedding | text | 1 | 0.335 | 0.255 | 0.279 | 847 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.519 | 0.587 | 0.517 | 847 |
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 by method (all doc_types)

> **swept**: retriever × k (overall P/R/F1) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

| retriever | modality | k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.338 | 0.255 | 0.279 | 847 |
| bge-m3 | text | 3 | 0.187 | 0.388 | 0.239 | 847 |
| bge-m3 | text | 5 | 0.147 | 0.482 | 0.212 | 847 |
| bge-m3 | text | 7 | 0.120 | 0.532 | 0.184 | 847 |
| bge-m3 | text | 10 | 0.100 | 0.611 | 0.163 | 847 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.485 | 0.552 | 0.486 | 847 |
| bge-m3\|colqwen2.5 | joint | 3 | 0.234 | 0.728 | 0.332 | 847 |
| bge-m3\|colqwen2.5 | joint | 5 | 0.167 | 0.798 | 0.259 | 847 |
| bm25 | text | 1 | 0.295 | 0.222 | 0.242 | 847 |
| bm25 | text | 3 | 0.185 | 0.378 | 0.234 | 847 |
| bm25 | text | 5 | 0.140 | 0.460 | 0.201 | 847 |
| bm25 | text | 7 | 0.114 | 0.508 | 0.175 | 847 |
| bm25 | text | 10 | 0.095 | 0.585 | 0.154 | 847 |
| bm25\|colmodernvbert | joint | 1 | 0.442 | 0.512 | 0.445 | 847 |
| bm25\|colmodernvbert | joint | 3 | 0.223 | 0.698 | 0.316 | 847 |
| bm25\|colmodernvbert | joint | 5 | 0.159 | 0.776 | 0.248 | 847 |
| colmodernvbert | vision | 1 | 0.588 | 0.460 | 0.496 | 847 |
| colmodernvbert | vision | 3 | 0.315 | 0.646 | 0.396 | 847 |
| colmodernvbert | vision | 5 | 0.227 | 0.725 | 0.322 | 847 |
| colmodernvbert | vision | 7 | 0.179 | 0.772 | 0.271 | 847 |
| colmodernvbert | vision | 10 | 0.140 | 0.817 | 0.222 | 847 |
| colqwen2.5 | vision | 1 | 0.633 | 0.488 | 0.528 | 847 |
| colqwen2.5 | vision | 3 | 0.338 | 0.683 | 0.425 | 847 |
| colqwen2.5 | vision | 5 | 0.236 | 0.749 | 0.335 | 847 |
| colqwen2.5 | vision | 7 | 0.185 | 0.792 | 0.279 | 847 |
| colqwen2.5 | vision | 10 | 0.144 | 0.838 | 0.229 | 847 |
| colqwen3 | vision | 1 | 0.702 | 0.541 | 0.586 | 847 |
| colqwen3 | vision | 3 | 0.368 | 0.739 | 0.460 | 847 |
| colqwen3 | vision | 5 | 0.255 | 0.806 | 0.361 | 847 |
| colqwen3 | vision | 7 | 0.199 | 0.839 | 0.299 | 847 |
| colqwen3 | vision | 10 | 0.152 | 0.874 | 0.241 | 847 |
| qwen3-embedding | text | 1 | 0.335 | 0.255 | 0.279 | 847 |
| qwen3-embedding | text | 3 | 0.199 | 0.413 | 0.254 | 847 |
| qwen3-embedding | text | 5 | 0.150 | 0.494 | 0.217 | 847 |
| qwen3-embedding\|colqwen3 | joint | 1 | 0.519 | 0.587 | 0.517 | 847 |
| qwen3-embedding\|colqwen3 | joint | 3 | 0.255 | 0.779 | 0.360 | 847 |
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 by method and render DPI

> **swept**: render dpi × retriever × k · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none

| retriever | modality | k | dpi | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 200 | 0.338 | 0.255 | 0.279 | 847 |
| bge-m3 | text | 3 | 200 | 0.187 | 0.388 | 0.239 | 847 |
| bge-m3 | text | 5 | 200 | 0.147 | 0.482 | 0.212 | 847 |
| bge-m3 | text | 7 | 200 | 0.120 | 0.532 | 0.184 | 847 |
| bge-m3 | text | 10 | 200 | 0.100 | 0.611 | 0.163 | 847 |
| bge-m3\|colqwen2.5 | joint | 1 | 200 | 0.485 | 0.552 | 0.486 | 847 |
| bge-m3\|colqwen2.5 | joint | 3 | 200 | 0.234 | 0.728 | 0.332 | 847 |
| bge-m3\|colqwen2.5 | joint | 5 | 200 | 0.167 | 0.798 | 0.259 | 847 |
| bm25 | text | 1 | 200 | 0.295 | 0.222 | 0.242 | 847 |
| bm25 | text | 3 | 200 | 0.185 | 0.378 | 0.234 | 847 |
| bm25 | text | 5 | 200 | 0.140 | 0.460 | 0.201 | 847 |
| bm25 | text | 7 | 200 | 0.114 | 0.508 | 0.175 | 847 |
| bm25 | text | 10 | 200 | 0.095 | 0.585 | 0.154 | 847 |
| bm25\|colmodernvbert | joint | 1 | 200 | 0.442 | 0.512 | 0.445 | 847 |
| bm25\|colmodernvbert | joint | 3 | 200 | 0.223 | 0.698 | 0.316 | 847 |
| bm25\|colmodernvbert | joint | 5 | 200 | 0.159 | 0.776 | 0.248 | 847 |
| colmodernvbert | vision | 1 | 200 | 0.588 | 0.460 | 0.496 | 847 |
| colmodernvbert | vision | 3 | 200 | 0.315 | 0.646 | 0.396 | 847 |
| colmodernvbert | vision | 5 | 200 | 0.227 | 0.725 | 0.322 | 847 |
| colmodernvbert | vision | 7 | 200 | 0.179 | 0.772 | 0.271 | 847 |
| colmodernvbert | vision | 10 | 200 | 0.140 | 0.817 | 0.222 | 847 |
| colqwen2.5 | vision | 1 | 200 | 0.633 | 0.488 | 0.528 | 847 |
| colqwen2.5 | vision | 3 | 200 | 0.338 | 0.683 | 0.425 | 847 |
| colqwen2.5 | vision | 5 | 200 | 0.236 | 0.749 | 0.335 | 847 |
| colqwen2.5 | vision | 7 | 200 | 0.185 | 0.792 | 0.279 | 847 |
| colqwen2.5 | vision | 10 | 200 | 0.144 | 0.838 | 0.229 | 847 |
| colqwen3 | vision | 1 | 200 | 0.702 | 0.541 | 0.586 | 847 |
| colqwen3 | vision | 3 | 200 | 0.368 | 0.739 | 0.460 | 847 |
| colqwen3 | vision | 5 | 200 | 0.255 | 0.806 | 0.361 | 847 |
| colqwen3 | vision | 7 | 200 | 0.199 | 0.839 | 0.299 | 847 |
| colqwen3 | vision | 10 | 200 | 0.152 | 0.874 | 0.241 | 847 |
| qwen3-embedding | text | 1 | 200 | 0.335 | 0.255 | 0.279 | 847 |
| qwen3-embedding | text | 3 | 200 | 0.199 | 0.413 | 0.254 | 847 |
| qwen3-embedding | text | 5 | 200 | 0.150 | 0.494 | 0.217 | 847 |
| qwen3-embedding\|colqwen3 | joint | 1 | 200 | 0.519 | 0.587 | 0.517 | 847 |
| qwen3-embedding\|colqwen3 | joint | 3 | 200 | 0.255 | 0.779 | 0.360 | 847 |
| n (per col) | - | - | - | - | - | - | - |

### Mined: ladder accuracy, scanned vs digital, by doc_type and rung

> **swept**: scan (digital vs scanned), all rungs · **dataset**: mmlongbench · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **scan**: split: digital vs scanned

_oracle pages, primary reasoner. Empty T on scans is by design (no embedded text)._

| doc_type | rung | digital | scanned | n_digital | n_scanned |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 39.2 [28.8-48.3] | - | 148 | 0 |
| Academic paper | TL | 37.7 [28.6-47.1] | - | 130 | 0 |
| Academic paper | TLV | 42.0 [31.6-51.3] | - | 119 | 0 |
| Academic paper | V | 31.4 [24.5-38.4] | - | 153 | 0 |
| Administration/Industry file | T | 61.2 [50.0-77.1] | 0.0 [0.0-0.0] | 49 | 11 |
| Administration/Industry file | TL | 58.7 [47.7-72.7] | 54.5 [42.9-75.0] | 46 | 11 |
| Administration/Industry file | TLV | 75.0 [63.2-92.1] | 72.7 [71.4-75.0] | 44 | 11 |
| Administration/Industry file | V | 50.0 [42.4-61.8] | 54.5 [50.0-57.1] | 50 | 11 |
| Brochure | T | 32.3 [21.9-44.8] | 0.0 [0.0-0.0] | 65 | 10 |
| Brochure | TL | 33.3 [20.9-48.3] | 30.0 [20.0-40.0] | 66 | 10 |
| Brochure | TLV | 40.3 [26.8-55.2] | 50.0 [20.0-80.0] | 62 | 10 |
| Brochure | V | 44.8 [31.1-58.6] | 50.0 [20.0-80.0] | 67 | 10 |
| Financial report | T | 50.5 [40.4-59.8] | - | 107 | 0 |
| Financial report | TL | 64.3 [49.1-75.7] | - | 70 | 0 |
| Financial report | TLV | 72.1 [66.0-79.4] | - | 68 | 0 |
| Financial report | V | 36.1 [29.5-43.4] | - | 108 | 0 |
| Guidebook | T | 38.2 [24.7-52.5] | 0.0 [0.0-0.0] | 110 | 10 |
| Guidebook | TL | 38.7 [25.4-52.0] | 11.1 [0.0-20.0] | 106 | 9 |
| Guidebook | TLV | 53.4 [40.0-66.4] | 28.6 [20.0-50.0] | 103 | 7 |
| Guidebook | V | 49.5 [37.5-61.1] | 22.2 [20.0-25.0] | 109 | 9 |
| Research report / Introduction | T | 34.4 [25.0-43.8] | 1.2 [0.0-3.8] | 128 | 81 |
| Research report / Introduction | TL | 32.8 [23.0-43.0] | 16.9 [9.0-24.7] | 125 | 77 |
| Research report / Introduction | TLV | 52.2 [40.5-63.6] | 53.4 [39.1-65.2] | 113 | 73 |
| Research report / Introduction | V | 43.4 [31.7-54.3] | 52.6 [36.9-65.1] | 129 | 78 |
| Tutorial/Workshop | T | 34.8 [28.6-38.5] | 7.9 [2.3-14.4] | 23 | 89 |
| Tutorial/Workshop | TL | 47.8 [28.6-57.7] | 46.6 [37.7-55.7] | 23 | 88 |
| Tutorial/Workshop | TLV | 72.7 [57.1-83.3] | 77.6 [69.3-84.5] | 22 | 85 |
| Tutorial/Workshop | V | 68.2 [57.1-75.0] | 70.5 [63.5-77.4] | 22 | 88 |
| **all doc_types** | **T** | **40.8 [36.0-45.8]** | **4.0 [1.0-7.4]** | **630** | **201** |
| **all doc_types** | **TL** | **41.7 [36.6-47.0]** | **32.8 [26.0-40.0]** | **566** | **195** |
| **all doc_types** | **TLV** | **54.0 [48.9-59.1]** | **64.5 [56.4-72.0]** | **531** | **186** |
| **all doc_types** | **V** | **41.8 [37.3-46.0]** | **59.2 [51.0-66.3]** | **638** | **196** |
| n (per col) | - | 2365 | 778 | - | - |
