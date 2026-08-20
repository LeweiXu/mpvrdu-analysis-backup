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
| g1-reasoner-thinking | G1_oracle_ladder | 1847 | 1834 | 13 | 0 | 0.7 |
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
| **all** |  | **104617** | 100878 | 3283 | 456 | 3.1 |

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Headline: cost-ordered ladder accuracy by doc_type (oracle pages)

> **swept**: representation ladder T/TL/TV/TLV/V · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. _

| doc_type | T | TL | TV | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 36.4 [27.7-44.1] | 33.1 [24.5-42.2] | 44.8 [36.4-52.8] | 42.9 [34.7-51.3] | 33.8 [25.3-41.7] | T | 770 |
| Administration/Industry file | 50.0 [33.3-67.9] | 56.2 [47.7-66.0] | 67.2 [57.8-79.2] | 67.2 [60.3-76.3] | 54.7 [47.8-63.6] | T | 320 |
| Brochure | 28.6 [17.6-40.3] | 32.5 [21.5-46.0] | 45.5 [33.3-57.9] | 45.5 [32.9-58.8] | 40.3 [27.6-54.3] | TL | 385 |
| Financial report | 49.1 [41.2-57.4] | 52.8 [41.4-61.9] | 50.0 [42.2-59.7] | 51.9 [44.0-60.0] | 38.9 [29.6-50.0] | T | 540 |
| Guidebook | 35.8 [22.5-50.9] | 40.0 [27.2-54.1] | 49.2 [36.7-61.7] | 51.7 [38.3-64.9] | 45.0 [33.3-57.0] | T | 600 |
| Research report / Introduction | 22.6 [14.2-31.5] | 27.4 [20.5-34.3] | 46.7 [37.0-54.7] | 47.6 [38.8-55.5] | 45.3 [36.1-53.8] | TV | 1060 |
| Tutorial/Workshop | 14.3 [6.2-22.7] | 48.2 [39.5-57.0] | 69.6 [64.0-75.0] | 73.2 [64.9-81.7] | 67.9 [62.5-73.5] | TV | 560 |
| **all doc_types** | **31.9 [27.3-36.5]** | **38.8 [34.5-43.0]** | **51.6 [48.0-55.3]** | **52.5 [48.5-56.5]** | **45.6 [41.7-49.5]** | **TV** | **4235** |
| n (per col) | 847 | 847 | 847 | 847 | 847 | - | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Each question carries exactly one doc_type, so unlike the evidence-source table the rows within a block are disjoint and the bolded All doc_types row closing it is their sum._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | Academic paper | 13.6 (21) | 3.9 (6) | 29.2 (45) | 53.2 (82) | 154 |
| TL->TLV | Administration/Industry file | 14.1 (9) | 3.1 (2) | 53.1 (34) | 29.7 (19) | 64 |
| TL->TLV | Brochure | 15.6 (12) | 2.6 (2) | 29.9 (23) | 51.9 (40) | 77 |
| TL->TLV | Financial report | 8.3 (9) | 9.3 (10) | 43.5 (47) | 38.9 (42) | 108 |
| TL->TLV | Guidebook | 13.3 (16) | 1.7 (2) | 38.3 (46) | 46.7 (56) | 120 |
| TL->TLV | Research report / Introduction | 24.5 (52) | 4.2 (9) | 23.1 (49) | 48.1 (102) | 212 |
| TL->TLV | Tutorial/Workshop | 26.8 (30) | 1.8 (2) | 46.4 (52) | 25.0 (28) | 112 |
| TL->TLV | **All doc_types** | 17.6 (149) | 3.9 (33) | 34.9 (296) | 43.6 (369) | 847 |
| T->TL | Academic paper | 5.2 (8) | 8.4 (13) | 27.9 (43) | 58.4 (90) | 154 |
| T->TL | Administration/Industry file | 14.1 (9) | 7.8 (5) | 42.2 (27) | 35.9 (23) | 64 |
| T->TL | Brochure | 9.1 (7) | 5.2 (4) | 23.4 (18) | 62.3 (48) | 77 |
| T->TL | Financial report | 13.0 (14) | 9.3 (10) | 39.8 (43) | 38.0 (41) | 108 |
| T->TL | Guidebook | 7.5 (9) | 3.3 (4) | 32.5 (39) | 56.7 (68) | 120 |
| T->TL | Research report / Introduction | 9.9 (21) | 5.2 (11) | 17.5 (37) | 67.5 (143) | 212 |
| T->TL | Tutorial/Workshop | 33.9 (38) | 0.0 (0) | 14.3 (16) | 51.8 (58) | 112 |
| T->TL | **All doc_types** | 12.5 (106) | 5.5 (47) | 26.3 (223) | 55.6 (471) | 847 |
| T->TLV | Academic paper | 13.6 (21) | 7.1 (11) | 29.2 (45) | 50.0 (77) | 154 |
| T->TLV | Administration/Industry file | 20.3 (13) | 3.1 (2) | 46.9 (30) | 29.7 (19) | 64 |
| T->TLV | Brochure | 22.1 (17) | 5.2 (4) | 23.4 (18) | 49.4 (38) | 77 |
| T->TLV | Financial report | 13.0 (14) | 10.2 (11) | 38.9 (42) | 38.0 (41) | 108 |
| T->TLV | Guidebook | 17.5 (21) | 1.7 (2) | 34.2 (41) | 46.7 (56) | 120 |
| T->TLV | Research report / Introduction | 29.7 (63) | 4.7 (10) | 17.9 (38) | 47.6 (101) | 212 |
| T->TLV | Tutorial/Workshop | 58.9 (66) | 0.0 (0) | 14.3 (16) | 26.8 (30) | 112 |
| T->TLV | **All doc_types** | 25.4 (215) | 4.7 (40) | 27.2 (230) | 42.7 (362) | 847 |
| T->TV | Academic paper | 12.3 (19) | 3.9 (6) | 32.5 (50) | 51.3 (79) | 154 |
| T->TV | Administration/Industry file | 18.8 (12) | 1.6 (1) | 48.4 (31) | 31.2 (20) | 64 |
| T->TV | Brochure | 19.5 (15) | 2.6 (2) | 26.0 (20) | 51.9 (40) | 77 |
| T->TV | Financial report | 11.1 (12) | 10.2 (11) | 38.9 (42) | 39.8 (43) | 108 |
| T->TV | Guidebook | 15.0 (18) | 1.7 (2) | 34.2 (41) | 49.2 (59) | 120 |
| T->TV | Research report / Introduction | 28.3 (60) | 4.2 (9) | 18.4 (39) | 49.1 (104) | 212 |
| T->TV | Tutorial/Workshop | 55.4 (62) | 0.0 (0) | 14.3 (16) | 30.4 (34) | 112 |
| T->TV | **All doc_types** | 23.4 (198) | 3.7 (31) | 28.2 (239) | 44.7 (379) | 847 |
| TV->TLV | Academic paper | 7.8 (12) | 9.7 (15) | 35.1 (54) | 47.4 (73) | 154 |
| TV->TLV | Administration/Industry file | 4.7 (3) | 4.7 (3) | 62.5 (40) | 28.1 (18) | 64 |
| TV->TLV | Brochure | 9.1 (7) | 9.1 (7) | 36.4 (28) | 45.5 (35) | 77 |
| TV->TLV | Financial report | 5.6 (6) | 3.7 (4) | 46.3 (50) | 44.4 (48) | 108 |
| TV->TLV | Guidebook | 5.0 (6) | 2.5 (3) | 46.7 (56) | 45.8 (55) | 120 |
| TV->TLV | Research report / Introduction | 7.1 (15) | 6.1 (13) | 40.6 (86) | 46.2 (98) | 212 |
| TV->TLV | Tutorial/Workshop | 8.0 (9) | 4.5 (5) | 65.2 (73) | 22.3 (25) | 112 |
| TV->TLV | **All doc_types** | 6.8 (58) | 5.9 (50) | 45.7 (387) | 41.6 (352) | 847 |
| n (per col) | TL->TLV: 847, T->TL: 847, T->TLV: 847, T->TV: 847, TV->TLV: 847 | - | - | - | - | - |

### Fidelity (overall): paired verdict transitions per rung pairing

> **view**: summary — pooled across all doc_types · **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. _

| pairing | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- |
| TL->TLV | 17.6 (149) | 3.9 (33) | 34.9 (296) | 43.6 (369) | 847 |
| T->TL | 12.5 (106) | 5.5 (47) | 26.3 (223) | 55.6 (471) | 847 |
| T->TLV | 25.4 (215) | 4.7 (40) | 27.2 (230) | 42.7 (362) | 847 |
| T->TV | 23.4 (198) | 3.7 (31) | 28.2 (239) | 44.7 (379) | 847 |
| TV->TLV | 6.8 (58) | 5.9 (50) | 45.7 (387) | 41.6 (352) | 847 |
| n (per col) | - | - | - | - | - |

### Fidelity: paired within-question verdict transitions by evidence source

> **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × evidence source · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **pairing**: within-question, both rungs status==ok · **All sources row**: pooled over questions, each counted once; not a column sum, has its own paired n

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. Paired on question_id over the same oracle pages: a question counts only when BOTH rungs produced a status==ok row, so the paired n is well below the pool and is the discount signal. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. A question citing several evidence sources is counted under each of them, so the per-source rows overlap and CANNOT be summed. The bolded All sources row closing each block is therefore computed fresh over every paired question in that pairing, each counted once, with its own paired n; it is a pooled total, not a column sum._

| pairing | evidence_source | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| TL->TLV | (none) | 10.5 (2) | 0.0 (0) | 63.2 (12) | 26.3 (5) | 19 |
| TL->TLV | Chart | 29.8 (53) | 3.4 (6) | 15.7 (28) | 51.1 (91) | 178 |
| TL->TLV | Figure | 22.4 (65) | 1.4 (4) | 22.4 (65) | 53.8 (156) | 290 |
| TL->TLV | Generalized-text (Layout) | 16.9 (20) | 3.4 (4) | 33.9 (40) | 45.8 (54) | 118 |
| TL->TLV | Pure-text (Plain-text) | 10.3 (30) | 2.7 (8) | 45.0 (131) | 41.9 (122) | 291 |
| TL->TLV | Table | 7.8 (17) | 7.8 (17) | 40.6 (88) | 43.8 (95) | 217 |
| TL->TLV | **All sources** | 17.6 (149) | 3.9 (33) | 34.9 (296) | 43.6 (369) | 847 |
| T->TL | (none) | 10.5 (2) | 0.0 (0) | 52.6 (10) | 36.8 (7) | 19 |
| T->TL | Chart | 6.2 (11) | 5.6 (10) | 12.9 (23) | 75.3 (134) | 178 |
| T->TL | Figure | 13.4 (39) | 5.2 (15) | 10.3 (30) | 71.0 (206) | 290 |
| T->TL | Generalized-text (Layout) | 14.4 (17) | 5.1 (6) | 22.9 (27) | 57.6 (68) | 118 |
| T->TL | Pure-text (Plain-text) | 12.7 (37) | 4.1 (12) | 35.1 (102) | 48.1 (140) | 291 |
| T->TL | Table | 16.1 (35) | 8.3 (18) | 32.3 (70) | 43.3 (94) | 217 |
| T->TL | **All sources** | 12.5 (106) | 5.5 (47) | 26.3 (223) | 55.6 (471) | 847 |
| T->TLV | (none) | 21.1 (4) | 0.0 (0) | 52.6 (10) | 26.3 (5) | 19 |
| T->TLV | Chart | 30.9 (55) | 3.9 (7) | 14.6 (26) | 50.6 (90) | 178 |
| T->TLV | Figure | 33.1 (96) | 3.8 (11) | 11.7 (34) | 51.4 (149) | 290 |
| T->TLV | Generalized-text (Layout) | 28.8 (34) | 5.9 (7) | 22.0 (26) | 43.2 (51) | 118 |
| T->TLV | Pure-text (Plain-text) | 19.2 (56) | 3.1 (9) | 36.1 (105) | 41.6 (121) | 291 |
| T->TLV | Table | 18.0 (39) | 10.1 (22) | 30.4 (66) | 41.5 (90) | 217 |
| T->TLV | **All sources** | 25.4 (215) | 4.7 (40) | 27.2 (230) | 42.7 (362) | 847 |
| T->TV | (none) | 15.8 (3) | 0.0 (0) | 52.6 (10) | 31.6 (6) | 19 |
| T->TV | Chart | 26.4 (47) | 2.8 (5) | 15.7 (28) | 55.1 (98) | 178 |
| T->TV | Figure | 32.4 (94) | 2.4 (7) | 13.1 (38) | 52.1 (151) | 290 |
| T->TV | Generalized-text (Layout) | 25.4 (30) | 4.2 (5) | 23.7 (28) | 46.6 (55) | 118 |
| T->TV | Pure-text (Plain-text) | 17.5 (51) | 3.1 (9) | 36.1 (105) | 43.3 (126) | 291 |
| T->TV | Table | 15.2 (33) | 8.8 (19) | 31.8 (69) | 44.2 (96) | 217 |
| T->TV | **All sources** | 23.4 (198) | 3.7 (31) | 28.2 (239) | 44.7 (379) | 847 |
| TV->TLV | (none) | 5.3 (1) | 0.0 (0) | 68.4 (13) | 26.3 (5) | 19 |
| TV->TLV | Chart | 9.6 (17) | 6.2 (11) | 36.0 (64) | 48.3 (86) | 178 |
| TV->TLV | Figure | 7.6 (22) | 8.3 (24) | 37.2 (108) | 46.9 (136) | 290 |
| TV->TLV | Generalized-text (Layout) | 8.5 (10) | 6.8 (8) | 42.4 (50) | 42.4 (50) | 118 |
| TV->TLV | Pure-text (Plain-text) | 5.2 (15) | 3.4 (10) | 50.2 (146) | 41.2 (120) | 291 |
| TV->TLV | Table | 6.0 (13) | 4.6 (10) | 42.4 (92) | 47.0 (102) | 217 |
| TV->TLV | **All sources** | 6.8 (58) | 5.9 (50) | 45.7 (387) | 41.6 (352) | 847 |
| n (per col) | TL->TLV: 847, T->TL: 847, T->TLV: 847, T->TV: 847, TV->TLV: 847 | - | - | - | - | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. _

| evidence_source | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| (none) | 52.6 [31.2-73.7] | 63.2 [38.9-83.3] | 68.4 [44.4-88.9] | 73.7 [52.6-91.3] | 52.6 [29.4-70.8] | 95 |
| Chart | 18.5 [12.3-24.6] | 19.1 [13.1-25.5] | 42.1 [33.1-51.5] | 45.5 [37.3-54.3] | 43.3 [34.4-52.4] | 890 |
| Figure | 15.5 [11.1-20.5] | 23.8 [17.8-30.5] | 45.5 [39.4-51.4] | 44.8 [38.0-51.7] | 40.3 [34.2-46.4] | 1450 |
| Generalized-text (Layout) | 28.0 [18.1-37.6] | 37.3 [27.3-47.4] | 49.2 [40.7-57.3] | 50.8 [42.3-59.2] | 44.1 [35.7-52.8] | 590 |
| Pure-text (Plain-text) | 39.2 [31.5-47.6] | 47.8 [41.1-55.3] | 53.6 [46.0-61.2] | 55.3 [48.8-62.8] | 44.3 [37.7-51.3] | 1455 |
| Table | 40.6 [33.8-46.4] | 48.4 [40.3-55.2] | 47.0 [40.4-53.5] | 48.4 [41.4-55.4] | 37.8 [31.0-44.3] | 1085 |
| n (per col) | 847 | 847 | 847 | 847 | 847 | - |

### Vision margin: paired bootstrap on best-image minus best-text, by doc_type

> **swept**: vision margin (best image rung − best text rung) × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question across all five rungs; a question enters only if scored at every rung

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. One bootstrap interval per group on a DIFFERENCE, not two marginal intervals read against each other. The margin is `max(TV, TLV, V) - max(T, TL)`: what attaching the page image is worth to that group, whichever image rung and whichever text rung happens to win it. Both maxima are recomputed whole on every resample, so the interval carries the cost of choosing the winning rungs instead of pretending it was named in advance. Convention matches the marginal CIs exactly (scoring.paired reuses scoring.accuracy's quantiles): documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles. Pairing is per question across ALL FIVE rungs at once: a question enters only if it is scored at every rung, so `n (paired)` is the five-way intersection and the two sides of the difference share their per-question difficulty rather than being treated as independent samples. `best image` and `best text` name the rungs the point estimate picked; a resample may pick different ones. `excludes 0` is the whole interval sitting on one side of zero; a group that does not exclude zero does not support the claim that vision buys it anything._

| doc_type | Δ vision (points) | CI low | CI high | best image | best text | n (paired) | excludes 0 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | +8.4 | +3.3 | +13.9 | TV | T | 154 | yes |
| Administration/Industry file | +10.9 | +4.1 | +21.1 | TV | TL | 64 | yes |
| Brochure | +13.0 | +3.7 | +25.4 | TV | TL | 77 | yes |
| Financial report | -0.9 | -8.0 | +8.5 | TLV | TL | 108 | no |
| Guidebook | +11.7 | +6.4 | +18.6 | TLV | TL | 120 | yes |
| Research report / Introduction | +20.3 | +12.7 | +29.1 | TLV | TL | 212 | yes |
| Tutorial/Workshop | +25.0 | +17.0 | +34.7 | TLV | TL | 112 | yes |
| all doc_types | +13.7 | +10.5 | +17.6 | TLV | TL | 847 | yes |

### Vision margin: paired bootstrap on best-image minus best-text, by evidence source

> **swept**: vision margin (best image rung − best text rung) × evidence source · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question across all five rungs; a question enters only if scored at every rung

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. One bootstrap interval per group on a DIFFERENCE, not two marginal intervals read against each other. The margin is `max(TV, TLV, V) - max(T, TL)`: what attaching the page image is worth to that group, whichever image rung and whichever text rung happens to win it. Both maxima are recomputed whole on every resample, so the interval carries the cost of choosing the winning rungs instead of pretending it was named in advance. Convention matches the marginal CIs exactly (scoring.paired reuses scoring.accuracy's quantiles): documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles. Pairing is per question across ALL FIVE rungs at once: a question enters only if it is scored at every rung, so `n (paired)` is the five-way intersection and the two sides of the difference share their per-question difficulty rather than being treated as independent samples. `best image` and `best text` name the rungs the point estimate picked; a resample may pick different ones. `excludes 0` is the whole interval sitting on one side of zero; a group that does not exclude zero does not support the claim that vision buys it anything. A question citing several evidence sources is counted under each of them, so the per-source rows overlap and CANNOT be summed. The pooled row closing the table is computed fresh over every paired question, each counted once._

| evidence_source | Δ vision (points) | CI low | CI high | best image | best text | n (paired) | excludes 0 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| (none) | +10.5 | +0.0 | +27.8 | TLV | TL | 19 | no |
| Chart | +26.4 | +18.5 | +34.9 | TLV | TL | 178 | yes |
| Figure | +21.7 | +16.8 | +27.6 | TV | TL | 290 | yes |
| Generalized-text (Layout) | +13.6 | +6.8 | +22.4 | TLV | TL | 118 | yes |
| Pure-text (Plain-text) | +7.6 | +4.0 | +11.3 | TLV | TL | 291 | yes |
| Table | +0.0 | -5.0 | +6.0 | TLV | TL | 217 | no |
| All sources | +13.7 | +10.5 | +17.6 | TLV | TL | 847 | yes |

### Parser comparison: TL/TLV accuracy by doc_type

> **swept**: parser (paddleocrvl / mineru / unlimited) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| doc_type | paddleocrvl TL | paddleocrvl TLV | mineru TL | mineru TLV | unlimited TL | unlimited TLV | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 35.1 [26.2-44.2] | 39.6 [31.3-48.0] | 19.5 [11.9-27.8] | 35.1 [25.7-44.7] | 39.0 [28.9-49.1] | 40.9 [32.2-50.3] | 154 |
| Administration/Industry file | 56.2 [47.7-66.0] | 70.3 [62.5-80.8] | 40.6 [30.0-54.7] | 62.5 [56.2-71.4] | 64.1 [55.1-74.5] | 68.8 [58.5-78.9] | 64 |
| Brochure | 32.5 [22.1-45.3] | 41.6 [27.8-56.0] | 16.9 [10.3-25.0] | 40.3 [29.1-53.2] | 36.4 [25.6-47.9] | 49.4 [35.4-62.5] | 77 |
| Financial report | 51.9 [38.8-62.6] | 54.6 [46.1-62.6] | 41.7 [27.0-53.8] | 47.2 [36.8-55.5] | 54.6 [45.0-62.5] | 53.7 [46.7-61.7] | 108 |
| Guidebook | 37.5 [25.2-50.4] | 51.7 [38.7-63.8] | 25.0 [15.8-34.5] | 50.0 [37.8-60.8] | 37.5 [24.6-51.1] | 50.8 [37.9-63.8] | 120 |
| Research report / Introduction | 26.9 [19.8-34.0] | 48.1 [39.3-56.0] | 19.8 [14.1-25.5] | 45.3 [37.0-52.9] | 26.9 [19.6-34.3] | 50.5 [40.7-58.3] | 212 |
| Tutorial/Workshop | 46.4 [38.7-53.8] | 74.1 [67.6-81.2] | 36.6 [27.9-46.5] | 68.8 [60.7-76.8] | 46.4 [37.9-55.4] | 72.3 [65.1-80.0] | 112 |
| n (per col) | 847 | 847 | 847 | 847 | 847 | 847 | - |

### Parser comparison (overall): TL/TLV accuracy per parser

> **view**: summary — pooled across all doc_types · **swept**: parser (paddleocrvl / mineru / unlimited) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| parser | TL | TLV | n |
| --- | --- | --- | --- |
| paddleocrvl | 38.4 [34.4-42.5] | 52.4 [48.3-56.4] | 847 |
| mineru | 26.8 [22.8-30.6] | 48.3 [44.1-52.2] | 847 |
| unlimited | 40.4 [36.1-44.6] | 53.4 [49.2-57.6] | 847 |
| n (per col) | 2541 | 2541 | - |

### Parser fidelity by scan status: text-only vs text+vision, digital vs scanned

> **swept**: text source × scan status × (text-only / text+vision) · **dataset**: mmlongbench · **scan**: SPLIT digital vs scanned (the pooled parser table is scan: any) · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV for the layout parsers, T/TV for PyMuPDF · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **delta column**: paired bootstrap on vision − text, not two marginals · **scanned pool**: 201 questions over 31 documents; the bootstrap resamples documents, so these intervals are wide

_A regroup of already-generated cells, not new inference: `scan_label` is a per-row covariate on every judged row (backfilled from annotations/auto_scan.csv), so this is the pooled parser comparison re-aggregated by scan class. Text-only is the parser's markdown alone (TL) for the three layout parsers and raw PyMuPDF embedded text (T) for the parser-free source; text+vision adds that page's images (TLV, TV). Accuracy cells carry a marginal CI and their own n. The Δ column is a PAIRED bootstrap on the difference (same questions both sides, documents resampled, 1000 resamples, seed 0), which is the right interval for a recovery claim; do not read it off the two marginal CIs. The scanned pool is 201 questions over just 31 documents, and the bootstrap resamples documents, so scanned intervals are wide by construction: quote the interval, not the point. Every cell here is measured, none imputed: the scanned text-only cells DO have scored rows, so nothing is blank. What collapses on scanned input is the text itself, not the cell — PyMuPDF (raw embedded text) on scanned pages (median 40 tokens) sits at the token floor, which is the block wrapper rather than document content (digital pages floor around 30 tokens and run to a median of ~840). Read those cells as 'the reasoner was handed no usable text', not as a text-only reading. The three layout parsers all OCR scanned pages and do produce real text there._

| text source (rungs) | digital: text-only | digital: text+vision | digital: Δ (vision − text) | scanned: text-only | scanned: text+vision | scanned: Δ (vision − text) |
| --- | --- | --- | --- | --- | --- | --- |
| PaddleOCR-VL (TL→TLV) | 40.1 [35.1-44.9] (n=646) | 49.7 [44.6-54.2] (n=646) | +9.6 [+5.7, +13.4] | 32.8 [26.2-40.0] (n=201) | 61.2 [53.1-68.8] (n=201) | +28.4 [+21.7, +34.8] |
| MinerU (TL→TLV) | 26.6 [22.0-31.4] (n=646) | 46.0 [41.2-50.3] (n=646) | +19.3 [+14.4, +23.5] | 27.4 [20.7-34.6] (n=201) | 55.7 [47.7-63.6] (n=201) | +28.4 [+19.8, +38.0] |
| Unlimited-OCR (TL→TLV) | 42.3 [37.2-47.2] (n=646) | 50.2 [45.1-54.7] (n=646) | +7.9 [+4.2, +11.7] | 34.3 [26.8-41.6] (n=201) | 63.7 [55.4-70.6] (n=201) | +29.4 [+21.7, +36.2] |
| PyMuPDF (raw embedded text) (T→TV) | 40.6 [35.8-45.4] (n=646) | 49.7 [45.0-54.3] (n=646) | +9.1 [+5.1, +13.1] | 4.0 [1.0-7.4] (n=201) | 57.7 [50.0-64.4] (n=201) | +53.7 [+46.7, +60.5] |
| **spread (max − min)** | 15.6 | 4.2 | 11.5 | 30.3 | 8.0 | 25.4 |

### Parser fidelity by evidence source and scan status: text-only vs text+vision

> **swept**: text source × evidence source × scan status × (text-only / text+vision) · **dataset**: mmlongbench · **scan**: SPLIT digital vs scanned (the pooled parser table is scan: any) · **sampling**: full · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV for the layout parsers, T/TV for PyMuPDF · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **delta column**: paired bootstrap on vision − text, not two marginals · **transition columns**: paired within-question R→W / W→R across the vision step, on the same pairs as the delta · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **scanned pool**: 201 questions over 31 documents split five ways; most scanned per-source cells are thin and daggered

_The `parser_scan` table cut by evidence source. Same regroup of already-generated cells, same rung pairs per text source (TL→TLV for the three layout parsers, T→TV for PyMuPDF), same scan_label covariate; see that table for the mechanism and the scanned-pool caveat. A question citing several evidence sources is counted under EACH of them, so the per-source rows overlap and CANNOT be summed; the bolded All sources row closing each parser pools every question once and reproduces the `parser_scan` row. R→W and W→R are the PAIRED within-question verdict changes across the vision step, as percentages of that cell's paired n with the raw question count in parentheses; they do not sum to 100 because the two unchanged verdicts are not shown. The Δ column is a paired bootstrap on the difference (documents resampled, 1000 resamples, seed 0), not a comparison of two marginal CIs. † marks a paired cell under 30 questions, which is most of the scanned per-source cells: the scanned pool is 201 questions over 31 documents before it is split five ways, so read those as direction only. PyMuPDF on scanned pages has no usable embedded text at all, so its scanned text-only cells are the token floor rather than a text reading._

| text source (rungs) | evidence_source | digital: text-only | digital: text+vision | digital: Δ (vision − text) | digital: R→W (%) | digital: W→R (%) | digital: paired n | scanned: text-only | scanned: text+vision | scanned: Δ (vision − text) | scanned: R→W (%) | scanned: W→R (%) | scanned: paired n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PaddleOCR-VL (TL→TLV) | Chart | 23.8 [16.3-32.0] (n=130) | 40.8 [30.0-50.7] (n=130) | +16.9 [+5.2, +28.4] | 3.8 (5) | 20.8 (27) | 130 | 4.2 [0.0-10.9] (n=48) | 54.2 [35.1-72.9] (n=48) | +50.0 [+30.2, +68.8] | 0.0 (0) | 50.0 (24) | 48 |
| PaddleOCR-VL (TL→TLV) | Figure | 17.4 [12.1-23.5] (n=184) | 37.0 [29.6-45.1] (n=184) | +19.6 [+12.3, +26.2] | 1.6 (3) | 21.2 (39) | 184 | 31.1 [20.9-41.7] (n=106) | 57.5 [46.9-68.2] (n=106) | +26.4 [+19.4, +33.6] | 0.9 (1) | 27.4 (29) | 106 |
| PaddleOCR-VL (TL→TLV) | Generalized-text (Layout) | 43.8 [33.8-53.7] (n=80) | 47.5 [37.0-57.6] (n=80) | +3.7 [-3.5, +11.0] | 3.8 (3) | 7.5 (6) | 80 | 26.3 [11.9-45.5] (n=38) | 57.9 [42.9-73.5] (n=38) | +31.6 [+17.2, +42.5] | 0.0 (0) | 31.6 (12) | 38 |
| PaddleOCR-VL (TL→TLV) | Pure-text (Plain-text) | 50.9 [42.9-59.1] (n=226) | 54.9 [46.5-63.3] (n=226) | +4.0 [+0.0, +8.1] | 3.5 (8) | 7.5 (17) | 226 | 35.4 [24.1-48.3] (n=65) | 55.4 [40.0-69.6] (n=65) | +20.0 [+9.4, +30.5] | 0.0 (0) | 20.0 (13) | 65 |
| PaddleOCR-VL (TL→TLV) | Table | 47.6 [38.6-55.5] (n=185) | 46.5 [38.5-53.7] (n=185) | -1.1 [-5.1, +3.4] | 5.9 (11) | 4.9 (9) | 185 | 59.4 [43.3-73.3] (n=32) | 71.9 [60.0-82.9] (n=32) | +12.5 [+0.0, +29.2] | 3.1 (1) | 15.6 (5) | 32 |
| PaddleOCR-VL (TL→TLV) | **All sources** | 40.1 [35.1-44.9] (n=646) | 49.7 [44.6-54.2] (n=646) | +9.6 [+5.7, +13.4] | 3.7 (24) | 13.3 (86) | 646 | 32.8 [26.2-40.0] (n=201) | 61.2 [53.1-68.8] (n=201) | +28.4 [+21.7, +34.8] | 1.0 (2) | 29.4 (59) | 201 |
| MinerU (TL→TLV) | Chart | 17.7 [10.6-24.2] (n=130) | 38.5 [29.3-46.9] (n=130) | +20.8 [+13.6, +29.5] | 3.1 (4) | 23.8 (31) | 130 | 14.6 [3.7-29.0] (n=48) | 47.9 [31.7-65.1] (n=48) | +33.3 [+14.8, +53.5] | 2.1 (1) | 35.4 (17) | 48 |
| MinerU (TL→TLV) | Figure | 12.5 [7.4-18.4] (n=184) | 38.6 [30.5-47.5] (n=184) | +26.1 [+18.6, +34.2] | 1.6 (3) | 27.7 (51) | 184 | 25.5 [16.1-33.9] (n=106) | 50.9 [40.7-60.7] (n=106) | +25.5 [+16.7, +33.6] | 1.9 (2) | 27.4 (29) | 106 |
| MinerU (TL→TLV) | Generalized-text (Layout) | 20.0 [12.3-28.2] (n=80) | 43.8 [34.1-54.3] (n=80) | +23.8 [+14.3, +34.6] | 2.5 (2) | 26.2 (21) | 80 | 18.4 [4.8-36.1] (n=38) | 50.0 [33.3-66.7] (n=38) | +31.6 [+14.7, +50.0] | 2.6 (1) | 34.2 (13) | 38 |
| MinerU (TL→TLV) | Pure-text (Plain-text) | 30.1 [22.7-37.8] (n=226) | 49.1 [41.0-57.3] (n=226) | +19.0 [+11.3, +26.6] | 3.1 (7) | 22.1 (50) | 226 | 30.8 [18.3-43.6] (n=65) | 53.8 [39.1-69.8] (n=65) | +23.1 [+13.5, +33.9] | 0.0 (0) | 23.1 (15) | 65 |
| MinerU (TL→TLV) | Table | 36.8 [27.5-45.3] (n=185) | 42.7 [35.0-50.3] (n=185) | +5.9 [-0.6, +13.0] | 5.9 (11) | 11.9 (22) | 185 | 56.2 [37.8-73.9] (n=32) | 65.6 [50.0-80.0] (n=32) | +9.4 [-9.1, +25.8] | 6.2 (2) | 15.6 (5) | 32 |
| MinerU (TL→TLV) | **All sources** | 26.6 [22.0-31.4] (n=646) | 46.0 [41.2-50.3] (n=646) | +19.3 [+14.4, +23.5] | 3.4 (22) | 22.8 (147) | 646 | 27.4 [20.7-34.6] (n=201) | 55.7 [47.7-63.6] (n=201) | +28.4 [+19.8, +38.0] | 2.0 (4) | 30.3 (61) | 201 |
| Unlimited-OCR (TL→TLV) | Chart | 23.8 [17.1-31.1] (n=130) | 42.3 [33.0-52.6] (n=130) | +18.5 [+9.2, +27.8] | 3.8 (5) | 22.3 (29) | 130 | 2.1 [0.0-6.7] (n=48) | 58.3 [39.7-76.2] (n=48) | +56.2 [+36.0, +74.4] | 0.0 (0) | 56.2 (27) | 48 |
| Unlimited-OCR (TL→TLV) | Figure | 20.7 [15.0-26.8] (n=184) | 38.0 [30.6-46.6] (n=184) | +17.4 [+11.2, +24.7] | 2.7 (5) | 20.1 (37) | 184 | 34.0 [25.6-41.4] (n=106) | 58.5 [50.0-66.0] (n=106) | +24.5 [+18.1, +31.4] | 0.9 (1) | 25.5 (27) | 106 |
| Unlimited-OCR (TL→TLV) | Generalized-text (Layout) | 43.8 [34.6-52.9] (n=80) | 52.5 [41.6-62.5] (n=80) | +8.8 [+1.3, +16.3] | 2.5 (2) | 11.2 (9) | 80 | 36.8 [21.6-52.5] (n=38) | 60.5 [44.7-76.5] (n=38) | +23.7 [+12.5, +34.2] | 0.0 (0) | 23.7 (9) | 38 |
| Unlimited-OCR (TL→TLV) | Pure-text (Plain-text) | 50.4 [41.7-59.8] (n=226) | 53.1 [44.5-61.7] (n=226) | +2.7 [-2.0, +7.2] | 4.4 (10) | 7.1 (16) | 226 | 36.9 [24.7-53.3] (n=65) | 56.9 [41.3-72.5] (n=65) | +20.0 [+8.8, +30.9] | 0.0 (0) | 20.0 (13) | 65 |
| Unlimited-OCR (TL→TLV) | Table | 49.7 [41.8-56.8] (n=185) | 48.1 [41.1-55.4] (n=185) | -1.6 [-5.6, +3.0] | 6.5 (12) | 4.9 (9) | 185 | 59.4 [42.3-73.9] (n=32) | 71.9 [57.7-83.9] (n=32) | +12.5 [-5.7, +33.3] | 6.2 (2) | 18.8 (6) | 32 |
| Unlimited-OCR (TL→TLV) | **All sources** | 42.3 [37.2-47.2] (n=646) | 50.2 [45.1-54.7] (n=646) | +7.9 [+4.2, +11.7] | 4.6 (30) | 12.5 (81) | 646 | 34.3 [26.8-41.6] (n=201) | 63.7 [55.4-70.6] (n=201) | +29.4 [+21.7, +36.2] | 1.5 (3) | 30.8 (62) | 201 |
| PyMuPDF (raw embedded text) (T→TV) | Chart | 24.6 [17.6-31.6] (n=130) | 37.7 [27.1-48.1] (n=130) | +13.1 [+4.2, +22.3] | 3.8 (5) | 16.9 (22) | 130 | 0.0 [0.0-0.0] (n=48) | 54.2 [34.2-71.1] (n=48) | +54.2 [+34.2, +71.1] | 0.0 (0) | 54.2 (26) | 48 |
| PyMuPDF (raw embedded text) (T→TV) | Figure | 19.6 [13.1-26.1] (n=184) | 41.3 [33.7-48.9] (n=184) | +21.7 [+13.6, +31.0] | 3.3 (6) | 25.0 (46) | 184 | 7.5 [2.4-14.3] (n=106) | 52.8 [44.0-61.0] (n=106) | +45.3 [+37.2, +52.8] | 0.9 (1) | 46.2 (49) | 106 |
| PyMuPDF (raw embedded text) (T→TV) | Generalized-text (Layout) | 40.0 [28.1-51.2] (n=80) | 47.5 [37.3-57.1] (n=80) | +7.5 [-1.2, +16.2] | 3.8 (3) | 11.2 (9) | 80 | 2.6 [0.0-7.5] (n=38) | 52.6 [37.9-67.4] (n=38) | +50.0 [+35.3, +66.7] | 2.6 (1) | 52.6 (20) | 38 |
| PyMuPDF (raw embedded text) (T→TV) | Pure-text (Plain-text) | 50.0 [40.9-59.0] (n=226) | 54.4 [45.7-63.1] (n=226) | +4.4 [-1.0, +10.0] | 4.4 (10) | 8.8 (20) | 226 | 3.1 [0.0-7.9] (n=65) | 50.8 [35.7-66.1] (n=65) | +47.7 [+33.3, +63.0] | 0.0 (0) | 47.7 (31) | 65 |
| PyMuPDF (raw embedded text) (T→TV) | Table | 48.1 [40.5-54.8] (n=185) | 44.9 [38.4-51.5] (n=185) | -3.2 [-9.8, +3.6] | 10.3 (19) | 7.0 (13) | 185 | 0.0 [0.0-0.0] (n=32) | 59.4 [44.4-73.3] (n=32) | +59.4 [+44.4, +73.3] | 0.0 (0) | 59.4 (19) | 32 |
| PyMuPDF (raw embedded text) (T→TV) | **All sources** | 40.6 [35.8-45.4] (n=646) | 49.7 [45.0-54.3] (n=646) | +9.1 [+5.1, +13.1] | 4.8 (31) | 13.9 (90) | 646 | 4.0 [1.0-7.4] (n=201) | 57.7 [50.0-64.4] (n=201) | +53.7 [+46.7, +60.5] | 0.5 (1) | 54.2 (109) | 201 |

### Resolution sweep: TLV/V accuracy by doc_type and preset

> **swept**: visual_resolution (low / med / high) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **representation**: TLV/V only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

| doc_type | rung | low | med | high | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | TLV | 37.0 [27.8-45.6] | 40.3 [31.8-48.7] | 46.8 [38.1-55.5] | 462 |
| Academic paper | V | 19.5 [12.7-26.7] | 30.5 [22.6-38.0] | 38.3 [29.5-47.0] | 462 |
| Administration/Industry file | TLV | 64.1 [53.2-75.4] | 68.8 [61.6-77.2] | 70.3 [60.0-83.0] | 192 |
| Administration/Industry file | V | 42.2 [29.8-53.1] | 51.6 [43.6-61.7] | 64.1 [54.1-75.0] | 192 |
| Brochure | TLV | 40.3 [28.4-52.1] | 42.9 [28.4-57.5] | 48.1 [35.0-61.8] | 231 |
| Brochure | V | 39.0 [28.0-51.3] | 45.5 [32.5-58.4] | 49.4 [37.0-63.2] | 231 |
| Financial report | TLV | 54.6 [45.2-61.9] | 52.8 [44.2-61.7] | 53.7 [46.7-61.7] | 324 |
| Financial report | V | 21.3 [11.9-28.6] | 36.1 [29.5-43.4] | 46.3 [38.9-53.2] | 324 |
| Guidebook | TLV | 48.3 [35.8-60.9] | 50.8 [37.7-63.2] | 51.7 [38.8-65.6] | 360 |
| Guidebook | V | 38.3 [28.6-47.6] | 47.5 [35.5-59.5] | 47.5 [36.4-59.6] | 360 |
| Research report / Introduction | TLV | 42.9 [33.9-50.9] | 49.5 [40.5-57.7] | 50.0 [40.5-58.4] | 636 |
| Research report / Introduction | V | 38.2 [29.2-46.4] | 47.2 [37.5-55.3] | 47.6 [39.2-55.0] | 636 |
| Tutorial/Workshop | TLV | 71.4 [62.6-80.3] | 74.1 [67.6-81.2] | 74.1 [66.7-80.9] | 336 |
| Tutorial/Workshop | V | 74.1 [67.7-81.2] | 67.9 [61.6-74.4] | 70.5 [62.2-78.3] | 336 |
| **all doc_types** | **TLV** | **49.2 [45.0-53.3]** | **52.5 [48.3-56.6]** | **54.7 [50.4-58.5]** | **2541** |
| **all doc_types** | **V** | **37.8 [33.2-42.3]** | **45.7 [41.8-50.1]** | **50.2 [46.4-54.1]** | **2541** |
| n (per col) | - | 1694 | 1694 | 1694 | - |

### Resolution sweep: TLV/V accuracy by evidence source and preset

> **swept**: visual_resolution (low / med / high) × evidence source · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **representation**: TLV/V only · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: does high resolution recover the pixel-limited sources (Chart, Figure) specifically, or lift every source alike

_Same sweep as the doc_type table, cut by the evidence modality a question draws on instead of by document class. The point is WHERE pixels buy accuracy: Chart and Figure are the pixel-limited sources (their content only exists in the image), so a resolution effect that is real should be larger there than on Pure-text, and a uniform lift across every source is a decoding-length or prompt effect rather than a legibility one. A question can cite SEVERAL sources and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus; the bolded All sources rows pool every question exactly once and are NOT a column sum. Per-cell n rides inline: the resolution run carries 6-10% OOM, attrition differs by preset (high loses the most), so a thin cell reads as survivorship rather than as a weaker effect._

| evidence_source | rung | low | med | high | n |
| --- | --- | --- | --- | --- | --- |
| (none) | TLV | 63.2 [38.9-83.3] (n=19) | 68.4 [44.4-90.9] (n=19) | 73.7 [52.6-91.3] (n=19) | 57 |
| (none) | V | 36.8 [17.6-60.0] (n=19) | 47.4 [27.7-66.7] (n=19) | 52.6 [31.2-71.4] (n=19) | 57 |
| Chart | TLV | 38.2 [30.1-46.5] (n=178) | 44.9 [35.5-54.5] (n=178) | 48.3 [39.2-57.4] (n=178) | 534 |
| Chart | V | 34.3 [26.2-43.4] (n=178) | 44.9 [35.8-54.0] (n=178) | 48.3 [40.3-56.8] (n=178) | 534 |
| Figure | TLV | 39.7 [32.8-46.6] (n=290) | 45.5 [38.3-52.4] (n=290) | 48.3 [41.5-54.9] (n=290) | 870 |
| Figure | V | 38.3 [31.2-44.9] (n=290) | 40.0 [33.7-46.1] (n=290) | 43.8 [37.3-49.8] (n=290) | 870 |
| Generalized-text (Layout) | TLV | 46.6 [37.6-55.3] (n=118) | 50.0 [41.0-58.3] (n=118) | 54.2 [45.5-62.6] (n=118) | 354 |
| Generalized-text (Layout) | V | 47.5 [38.3-57.0] (n=118) | 49.2 [40.8-57.7] (n=118) | 53.4 [45.0-61.7] (n=118) | 354 |
| Pure-text (Plain-text) | TLV | 52.9 [45.9-60.2] (n=291) | 55.0 [48.0-62.1] (n=291) | 55.0 [48.0-62.3] (n=291) | 873 |
| Pure-text (Plain-text) | V | 38.8 [31.9-45.5] (n=291) | 45.4 [38.8-52.3] (n=291) | 51.5 [43.5-58.8] (n=291) | 873 |
| Table | TLV | 48.8 [41.1-55.8] (n=217) | 49.8 [42.8-56.6] (n=217) | 48.8 [41.8-55.4] (n=217) | 651 |
| Table | V | 25.3 [18.7-32.5] (n=217) | 37.3 [31.0-44.1] (n=217) | 42.4 [35.5-48.9] (n=217) | 651 |
| **All sources** | **TLV** | **49.2 [45.0-53.3] (n=847)** | **52.5 [48.3-56.6] (n=847)** | **54.7 [50.4-58.5] (n=847)** | **2541** |
| **All sources** | **V** | **37.8 [33.2-42.3] (n=847)** | **45.7 [41.8-50.1] (n=847)** | **50.2 [46.4-54.1] (n=847)** | **2541** |
| n (per col) | - | 1694 | 1694 | 1694 | - |

### Mined: ladder accuracy, scanned vs digital, by doc_type and rung

> **swept**: scan (digital vs scanned), all rungs · **dataset**: mmlongbench · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **scan**: split: digital vs scanned

_oracle pages, primary reasoner. Empty T on scans is by design (no embedded text)._

| doc_type | rung | digital | scanned | n_digital | n_scanned |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 39.0 [28.8-48.2] | - | 154 | 0 |
| Academic paper | TL | 35.1 [26.2-44.2] | - | 154 | 0 |
| Academic paper | TLV | 39.6 [31.3-48.0] | - | 154 | 0 |
| Academic paper | V | 31.2 [24.2-38.3] | - | 154 | 0 |
| Administration/Industry file | T | 60.4 [49.2-75.0] | 0.0 [0.0-0.0] | 53 | 11 |
| Administration/Industry file | TL | 56.6 [46.5-67.3] | 54.5 [42.9-75.0] | 53 | 11 |
| Administration/Industry file | TLV | 69.8 [60.9-82.9] | 72.7 [71.4-75.0] | 53 | 11 |
| Administration/Industry file | V | 49.1 [41.5-60.0] | 54.5 [50.0-57.1] | 53 | 11 |
| Brochure | T | 31.3 [20.9-43.1] | 0.0 [0.0-0.0] | 67 | 10 |
| Brochure | TL | 32.8 [20.3-47.6] | 30.0 [20.0-40.0] | 67 | 10 |
| Brochure | TLV | 40.3 [26.6-55.1] | 50.0 [20.0-80.0] | 67 | 10 |
| Brochure | V | 44.8 [31.1-58.6] | 50.0 [20.0-80.0] | 67 | 10 |
| Financial report | T | 50.0 [40.0-59.8] | - | 108 | 0 |
| Financial report | TL | 51.9 [38.8-62.6] | - | 108 | 0 |
| Financial report | TLV | 54.6 [46.1-62.6] | - | 108 | 0 |
| Financial report | V | 36.1 [29.5-43.4] | - | 108 | 0 |
| Guidebook | T | 38.2 [24.7-52.5] | 0.0 [0.0-0.0] | 110 | 10 |
| Guidebook | TL | 39.1 [26.1-52.0] | 20.0 [20.0-20.0] | 110 | 10 |
| Guidebook | TLV | 53.6 [40.4-66.7] | 30.0 [20.0-40.0] | 110 | 10 |
| Guidebook | V | 49.1 [37.2-60.6] | 30.0 [20.0-40.0] | 110 | 10 |
| Research report / Introduction | T | 34.4 [25.0-43.9] | 1.2 [0.0-3.8] | 131 | 81 |
| Research report / Introduction | TL | 32.8 [23.5-42.4] | 17.3 [9.0-25.6] | 131 | 81 |
| Research report / Introduction | TLV | 47.3 [36.8-57.4] | 49.4 [34.8-61.3] | 131 | 81 |
| Research report / Introduction | V | 42.7 [31.4-53.1] | 50.6 [34.7-63.6] | 131 | 81 |
| Tutorial/Workshop | T | 34.8 [28.6-38.5] | 7.9 [2.3-14.4] | 23 | 89 |
| Tutorial/Workshop | TL | 47.8 [28.6-57.7] | 46.1 [37.0-55.4] | 23 | 89 |
| Tutorial/Workshop | TLV | 69.6 [57.1-76.9] | 75.3 [66.7-83.1] | 23 | 89 |
| Tutorial/Workshop | V | 65.2 [57.1-69.2] | 69.7 [62.7-76.7] | 23 | 89 |
| **all doc_types** | **T** | **40.6 [35.8-45.4]** | **4.0 [1.0-7.4]** | **646** | **201** |
| **all doc_types** | **TL** | **40.1 [35.1-44.9]** | **32.8 [26.2-40.0]** | **646** | **201** |
| **all doc_types** | **TLV** | **49.7 [44.6-54.2]** | **61.2 [53.1-68.8]** | **646** | **201** |
| **all doc_types** | **V** | **41.5 [37.1-45.6]** | **58.2 [50.0-65.4]** | **646** | **201** |
| n (per col) | - | 2584 | 804 | - | - |

### Mined: ladder accuracy, scanned vs digital, by evidence source and rung

> **swept**: scan (digital vs scanned) × evidence source × rung · **dataset**: mmlongbench · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **scan**: split: digital vs scanned · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **n**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_Same digital/scanned split as the doc_type table, cut by the evidence modality a question draws on. The reason to cut it this way: on scans the V rung stops losing to TL, and there are two different explanations for that. Either the OCR text layer is degraded for EVERY source (so the split looks flat), or it is specifically Table and Chart that lose their text layer while Pure-text survives. T is omitted: a scan has no embedded text by construction, so a T row measures guessing, not the source. A question can cite SEVERAL sources and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus; the bolded All sources rows pool every question exactly once and are NOT a column sum. ⚠ SURVIVORSHIP: the scanned n are thin (a few hundred cells spread over sources and rungs, further thinned by rung-dependent OOM), so per-cell n rides inline on both accuracy columns and a small scanned cell reads as which questions survived, not as robustness. This is a trend table, not a precision table._

| evidence_source | rung | digital | scanned | n |
| --- | --- | --- | --- | --- |
| (none) | TL | 66.7 [41.2-87.0] (n=18) | 0.0 [0.0-0.0] (n=1) | 19 |
| (none) | TLV | 66.7 [37.5-90.5] (n=18) | 100.0 [100.0-100.0] (n=1) | 19 |
| (none) | V | 44.4 [23.5-62.5] (n=18) | 100.0 [100.0-100.0] (n=1) | 19 |
| Chart | TL | 23.8 [16.3-32.0] (n=130) | 4.2 [0.0-10.9] (n=48) | 178 |
| Chart | TLV | 40.8 [30.0-50.7] (n=130) | 54.2 [35.1-72.9] (n=48) | 178 |
| Chart | V | 41.5 [32.2-51.0] (n=130) | 52.1 [32.6-70.0] (n=48) | 178 |
| Figure | TL | 17.4 [12.1-23.5] (n=184) | 31.1 [20.9-41.7] (n=106) | 290 |
| Figure | TLV | 37.0 [29.6-45.1] (n=184) | 57.5 [46.9-68.2] (n=106) | 290 |
| Figure | V | 33.2 [26.6-40.4] (n=184) | 52.8 [42.4-62.0] (n=106) | 290 |
| Generalized-text (Layout) | TL | 43.8 [33.8-53.7] (n=80) | 26.3 [11.9-45.5] (n=38) | 118 |
| Generalized-text (Layout) | TLV | 47.5 [37.0-57.6] (n=80) | 57.9 [42.9-73.5] (n=38) | 118 |
| Generalized-text (Layout) | V | 47.5 [38.2-57.7] (n=80) | 50.0 [34.3-65.7] (n=38) | 118 |
| Pure-text (Plain-text) | TL | 50.9 [42.9-59.1] (n=226) | 35.4 [24.1-48.3] (n=65) | 291 |
| Pure-text (Plain-text) | TLV | 54.9 [46.5-63.3] (n=226) | 55.4 [40.0-69.6] (n=65) | 291 |
| Pure-text (Plain-text) | V | 42.5 [35.7-50.0] (n=226) | 50.8 [35.7-66.1] (n=65) | 291 |
| Table | TL | 47.6 [38.6-55.5] (n=185) | 59.4 [43.3-73.3] (n=32) | 217 |
| Table | TLV | 46.5 [38.5-53.7] (n=185) | 71.9 [60.0-82.9] (n=32) | 217 |
| Table | V | 32.4 [25.9-38.4] (n=185) | 65.6 [48.5-80.6] (n=32) | 217 |
| **All sources** | **TL** | **40.1 [35.1-44.9] (n=646)** | **32.8 [26.2-40.0] (n=201)** | **847** |
| **All sources** | **TLV** | **49.7 [44.6-54.2] (n=646)** | **61.2 [53.1-68.8] (n=201)** | **847** |
| **All sources** | **V** | **41.5 [37.1-45.6] (n=646)** | **58.2 [50.0-65.4] (n=201)** | **847** |
| n (per col) | - | 1938 | 603 | - |

## Selection

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page_set condition (sufficiency / robustness) × ranking source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **pivot**: all-gold row loaded from g1-representation-full (oracle, hop=multi) by the builder

_Rows group on the pageset condition grammar (ranking source, gold rule, distractor count); the robustness gold-count BLOCKS come from the corpus gold-page annotation (the +k design filters questions by exact gold count and feeds ALL their gold pages, so the block is a property of the question, not the rule). Each block's d=0 baseline is the bolded oracle row above it: all gold + no distractors IS the oracle condition, loaded from the G1 cache over the same questions, so the baseline is exact and was never re-generated. Read DOWN a block for the dilution slope at constant evidence; blocks are not comparable to each other (evidence and length both differ). Sufficiency rows withhold or isolate ONE gold page by the named ranker's ordering, on the hop=multi pool, and read against the bolded multi-pool oracle row. Per-cell n is load-bearing: OOM attrition is rung-dependent._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 25.4 [19.7-31.4] (n=358) | 30.7 [25.1-36.0] (n=358) | 38.0 [32.4-43.9] (n=358) | 33.5 [28.2-39.1] (n=358) | 1432 |
| drop bottom 1 | bm25 | 10.2 [7.1-14.3] (n=352) | 11.4 [7.9-14.9] (n=352) | 15.9 [12.2-20.8] (n=352) | 13.4 [9.7-17.7] (n=352) | 1408 |
| drop bottom 1 | colqwen3 | 11.4 [8.0-15.1] (n=352) | 13.4 [9.7-17.5] (n=352) | 18.5 [13.7-24.0] (n=352) | 15.1 [10.9-19.8] (n=352) | 1408 |
| drop top 1 | bm25 | 11.9 [8.3-16.0] (n=352) | 13.6 [10.3-17.5] (n=352) | 15.9 [12.1-19.8] (n=352) | 14.2 [10.5-17.8] (n=352) | 1408 |
| drop top 1 | colqwen3 | 10.8 [7.5-15.0] (n=352) | 11.1 [7.9-14.8] (n=352) | 15.9 [12.2-19.9] (n=352) | 13.9 [10.4-17.6] (n=352) | 1408 |
| keep bottom 1 | bm25 | 9.1 [5.9-12.8] (n=352) | 9.9 [7.0-13.4] (n=352) | 11.1 [7.9-14.2] (n=352) | 10.5 [7.8-13.6] (n=352) | 1408 |
| keep bottom 1 | colqwen3 | 9.4 [6.4-13.1] (n=352) | 9.7 [6.7-13.2] (n=352) | 10.5 [7.5-14.0] (n=352) | 9.9 [7.2-13.2] (n=352) | 1408 |
| keep top 1 | bm25 | 9.1 [6.2-12.8] (n=352) | 8.5 [5.8-11.7] (n=352) | 12.2 [9.0-16.6] (n=352) | 9.4 [6.2-13.4] (n=352) | 1408 |
| keep top 1 | colqwen3 | 9.1 [6.1-12.4] (n=352) | 10.2 [6.9-14.1] (n=352) | 12.8 [8.9-17.6] (n=352) | 11.1 [7.5-15.4] (n=352) | 1408 |
| **oracle (gold 1, d=0)** | - | 37.1 [31.1-43.1] (n=480) | 44.6 [38.9-50.1] (n=480) | 63.7 [58.2-69.3] (n=480) | 55.0 [49.7-60.2] (n=480) | 1920 |
| gold 1 + 1 distractors | bm25 | 39.7 [33.5-45.7] (n=474) | 46.8 [41.3-52.4] (n=474) | 64.6 [59.2-69.5] (n=474) | 57.4 [52.1-62.4] (n=474) | 1896 |
| gold 1 + 1 distractors | colqwen3 | 39.5 [33.7-45.2] (n=474) | 48.9 [43.3-54.1] (n=474) | 63.7 [58.7-68.6] (n=474) | 55.7 [50.5-60.4] (n=474) | 1896 |
| gold 1 + 2 distractors | bm25 | 40.9 [34.8-47.2] (n=474) | 46.2 [40.8-51.7] (n=474) | 64.8 [59.6-69.9] (n=474) | 53.6 [48.4-58.7] (n=474) | 1896 |
| gold 1 + 2 distractors | colqwen3 | 38.8 [32.3-45.0] (n=474) | 47.9 [42.0-53.4] (n=474) | 64.3 [59.5-68.7] (n=474) | 56.1 [51.2-61.4] (n=474) | 1896 |
| gold 1 + 3 distractors | bm25 | 40.9 [34.8-47.0] (n=474) | 47.0 [41.6-52.1] (n=474) | 65.0 [59.9-69.6] (n=474) | 54.4 [49.7-59.2] (n=474) | 1896 |
| gold 1 + 3 distractors | colqwen3 | 40.9 [35.0-46.9] (n=474) | 47.0 [41.4-52.9] (n=474) | 63.1 [58.3-67.6] (n=474) | 55.1 [50.3-59.9] (n=474) | 1896 |
| **oracle (gold 2, d=0)** | - | 28.9 [22.5-35.2] (n=246) | 33.3 [27.4-39.7] (n=246) | 37.8 [30.7-44.5] (n=246) | 34.6 [27.9-41.2] (n=246) | 984 |
| gold 2 + 1 distractors | bm25 | 29.0 [22.2-35.8] (n=241) | 34.9 [29.0-40.6] (n=241) | 39.0 [31.7-46.5] (n=241) | 34.0 [27.2-41.0] (n=241) | 964 |
| gold 2 + 1 distractors | colqwen3 | 25.7 [19.6-32.0] (n=241) | 34.0 [27.8-40.7] (n=241) | 38.6 [31.2-46.3] (n=241) | 34.4 [27.7-41.7] (n=241) | 964 |
| gold 2 + 2 distractors | bm25 | 27.0 [20.7-33.5] (n=241) | 32.8 [26.2-39.2] (n=241) | 39.8 [32.7-46.8] (n=241) | 34.4 [28.2-40.9] (n=241) | 964 |
| gold 2 + 2 distractors | colqwen3 | 25.3 [18.9-32.2] (n=241) | 33.6 [27.3-40.3] (n=241) | 35.7 [28.3-43.0] (n=241) | 32.4 [25.9-39.6] (n=241) | 964 |
| gold 2 + 3 distractors | bm25 | 28.2 [21.5-35.1] (n=241) | 34.9 [27.8-41.7] (n=241) | 40.2 [32.5-47.4] (n=241) | 34.0 [27.3-40.5] (n=241) | 964 |
| gold 2 + 3 distractors | colqwen3 | 21.6 [16.1-27.5] (n=241) | 28.2 [22.2-34.6] (n=241) | 33.6 [26.4-41.0] (n=241) | 33.2 [26.4-40.0] (n=241) | 964 |
| **oracle (gold 3, d=0)** | - | 25.0 [10.2-41.5] (n=40) | 30.0 [15.4-46.2] (n=40) | 47.5 [30.8-63.4] (n=40) | 42.5 [24.3-57.8] (n=40) | 160 |
| gold 3 + 1 distractors | bm25 | 22.5 [9.8-38.5] (n=40) | 35.0 [20.5-50.0] (n=40) | 50.0 [34.1-65.9] (n=40) | 37.5 [21.4-54.1] (n=40) | 160 |
| gold 3 + 1 distractors | colqwen3 | 22.5 [7.9-39.0] (n=40) | 40.0 [23.7-56.8] (n=40) | 45.0 [28.2-61.0] (n=40) | 40.0 [25.0-54.1] (n=40) | 160 |
| gold 3 + 2 distractors | bm25 | 17.5 [5.1-32.5] (n=40) | 37.5 [21.1-53.8] (n=40) | 52.5 [35.1-67.4] (n=40) | 40.0 [25.6-55.0] (n=40) | 160 |
| gold 3 + 2 distractors | colqwen3 | 27.5 [12.8-43.9] (n=40) | 37.5 [22.5-53.7] (n=40) | 40.0 [23.7-55.8] (n=40) | 30.0 [16.2-44.2] (n=40) | 160 |
| gold 3 + 3 distractors | bm25 | 17.5 [5.1-31.0] (n=40) | 30.0 [15.8-44.5] (n=40) | 40.0 [23.1-55.3] (n=40) | 37.5 [21.1-52.5] (n=40) | 160 |
| gold 3 + 3 distractors | colqwen3 | 25.0 [10.0-41.5] (n=40) | 35.0 [19.5-51.2] (n=40) | 40.0 [25.0-56.1] (n=40) | 32.5 [17.5-46.5] (n=40) | 160 |
| n (per col) | - | 7346 | 7346 | 7346 | 7346 | - |

### Selection: paired within-question verdict transitions from the oracle page set

> **swept**: page_set transition (oracle → each sufficiency rule / +k distractors) × ranking source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **pivot**: oracle cells loaded from g1-representation-full by the builder and paired per (question, rung) · **pairing**: within-question, oracle and perturbed page set both status==ok at that rung

_Paired on (question_id, rung) against the SAME question's oracle cell, loaded from the G1 cache: a question counts at a rung only when both the oracle and the perturbed page set produced a status==ok row there. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw question count behind the percentage. Sufficiency pairs against the hop=multi oracle (the pool its rules are defined on); each robustness block pairs against the oracle over the questions with exactly that gold-page count, so every block reads against its own d=0 condition and blocks are not comparable to each other. The bolded All rungs row closing each transition pools the four rungs, so its paired n is the sum of the rung rows above it and one question can appear in it up to four times._

| block | transition | ranker | rung | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | T | 1.7 (6) | 17.3 (61) | 8.5 (30) | 72.4 (255) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | TL | 2.6 (9) | 22.4 (79) | 8.8 (31) | 66.2 (233) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | TLV | 4.3 (15) | 27.0 (95) | 11.6 (41) | 57.1 (201) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | V | 2.3 (8) | 23.0 (81) | 11.1 (39) | 63.6 (224) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | **All rungs** | 2.7 (38) | 22.4 (316) | 10.0 (141) | 64.8 (913) | 1408 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | T | 2.8 (10) | 17.3 (61) | 8.5 (30) | 71.3 (251) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | TL | 2.8 (10) | 20.7 (73) | 10.5 (37) | 65.9 (232) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | TLV | 4.5 (16) | 24.7 (87) | 13.9 (49) | 56.8 (200) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | V | 2.6 (9) | 21.6 (76) | 12.5 (44) | 63.4 (223) | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | **All rungs** | 3.2 (45) | 21.1 (297) | 11.4 (160) | 64.3 (906) | 1408 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | T | 2.3 (8) | 16.2 (57) | 9.7 (34) | 71.9 (253) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | TL | 2.8 (10) | 20.5 (72) | 10.8 (38) | 65.9 (232) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | TLV | 3.1 (11) | 25.9 (91) | 12.8 (45) | 58.2 (205) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | V | 3.4 (12) | 23.3 (82) | 10.8 (38) | 62.5 (220) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | **All rungs** | 2.9 (41) | 21.4 (302) | 11.0 (155) | 64.6 (910) | 1408 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | T | 1.4 (5) | 16.5 (58) | 9.4 (33) | 72.7 (256) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | TL | 1.7 (6) | 21.9 (77) | 9.4 (33) | 67.0 (236) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | TLV | 4.3 (15) | 27.0 (95) | 11.6 (41) | 57.1 (201) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | V | 3.7 (13) | 23.9 (84) | 10.2 (36) | 62.2 (219) | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | **All rungs** | 2.8 (39) | 22.3 (314) | 10.2 (143) | 64.8 (912) | 1408 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | T | 2.3 (8) | 19.0 (67) | 6.8 (24) | 71.9 (253) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | TL | 1.7 (6) | 23.0 (81) | 8.2 (29) | 67.0 (236) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | TLV | 1.7 (6) | 29.3 (103) | 9.4 (33) | 59.7 (210) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | V | 2.8 (10) | 26.4 (93) | 7.7 (27) | 63.1 (222) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | **All rungs** | 2.1 (30) | 24.4 (344) | 8.0 (113) | 65.4 (921) | 1408 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | T | 1.1 (4) | 17.6 (62) | 8.2 (29) | 73.0 (257) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | TL | 2.0 (7) | 23.6 (83) | 7.7 (27) | 66.8 (235) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | TLV | 2.3 (8) | 30.4 (107) | 8.2 (29) | 59.1 (208) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | V | 3.7 (13) | 27.8 (98) | 6.2 (22) | 62.2 (219) | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | **All rungs** | 2.3 (32) | 24.9 (350) | 7.6 (107) | 65.3 (919) | 1408 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | T | 1.4 (5) | 18.2 (64) | 7.7 (27) | 72.7 (256) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | TL | 1.7 (6) | 24.4 (86) | 6.8 (24) | 67.0 (236) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | TLV | 3.4 (12) | 29.8 (105) | 8.8 (31) | 58.0 (204) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | V | 1.4 (5) | 26.1 (92) | 8.0 (28) | 64.5 (227) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | **All rungs** | 2.0 (28) | 24.6 (347) | 7.8 (110) | 65.6 (923) | 1408 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | T | 2.3 (8) | 19.0 (67) | 6.8 (24) | 71.9 (253) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | TL | 2.3 (8) | 23.3 (82) | 8.0 (28) | 66.5 (234) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | TLV | 2.6 (9) | 28.4 (100) | 10.2 (36) | 58.8 (207) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | V | 2.0 (7) | 25.0 (88) | 9.1 (32) | 63.9 (225) | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | **All rungs** | 2.3 (32) | 23.9 (337) | 8.5 (120) | 65.3 (919) | 1408 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | T | 5.3 (25) | 3.2 (15) | 34.4 (163) | 57.2 (271) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | TL | 5.1 (24) | 3.4 (16) | 41.8 (198) | 49.8 (236) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | TLV | 5.9 (28) | 5.9 (28) | 58.6 (278) | 29.5 (140) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | V | 8.9 (42) | 7.2 (34) | 48.5 (230) | 35.4 (168) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | **All rungs** | 6.3 (119) | 4.9 (93) | 45.8 (869) | 43.0 (815) | 1896 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | T | 6.1 (29) | 4.2 (20) | 33.3 (158) | 56.3 (267) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | TL | 8.4 (40) | 4.6 (22) | 40.5 (192) | 46.4 (220) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | TLV | 7.0 (33) | 7.8 (37) | 56.8 (269) | 28.5 (135) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | V | 9.5 (45) | 9.5 (45) | 46.2 (219) | 34.8 (165) | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | **All rungs** | 7.8 (147) | 6.5 (124) | 44.2 (838) | 41.5 (787) | 1896 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | T | 7.2 (34) | 3.8 (18) | 33.8 (160) | 55.3 (262) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | TL | 6.3 (30) | 5.3 (25) | 39.9 (189) | 48.5 (230) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | TLV | 6.8 (32) | 6.5 (31) | 58.0 (275) | 28.7 (136) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | V | 7.2 (34) | 9.3 (44) | 46.4 (220) | 37.1 (176) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | **All rungs** | 6.9 (130) | 6.2 (118) | 44.5 (844) | 42.4 (804) | 1896 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | T | 5.5 (26) | 4.2 (20) | 33.3 (158) | 57.0 (270) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | TL | 7.8 (37) | 5.1 (24) | 40.1 (190) | 47.0 (223) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | TLV | 8.0 (38) | 8.2 (39) | 56.3 (267) | 27.4 (130) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | V | 11.2 (53) | 10.8 (51) | 44.9 (213) | 33.1 (157) | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | **All rungs** | 8.1 (154) | 7.1 (134) | 43.7 (828) | 41.1 (780) | 1896 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | T | 7.2 (34) | 3.8 (18) | 33.8 (160) | 55.3 (262) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | TL | 6.8 (32) | 4.9 (23) | 40.3 (191) | 48.1 (228) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | TLV | 7.8 (37) | 7.4 (35) | 57.2 (271) | 27.6 (131) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | V | 9.3 (44) | 10.5 (50) | 45.1 (214) | 35.0 (166) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | **All rungs** | 7.8 (147) | 6.6 (126) | 44.1 (836) | 41.5 (787) | 1896 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | T | 8.2 (39) | 4.9 (23) | 32.7 (155) | 54.2 (257) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | TL | 8.2 (39) | 6.3 (30) | 38.8 (184) | 46.6 (221) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | TLV | 8.2 (39) | 9.7 (46) | 54.9 (260) | 27.2 (129) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | V | 10.5 (50) | 11.2 (53) | 44.5 (211) | 33.8 (160) | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | **All rungs** | 8.8 (167) | 8.0 (152) | 42.7 (810) | 40.5 (767) | 1896 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | T | 7.1 (17) | 7.5 (18) | 22.0 (53) | 63.5 (153) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | TL | 7.1 (17) | 6.2 (15) | 27.8 (67) | 58.9 (142) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | TLV | 6.6 (16) | 6.2 (15) | 32.4 (78) | 54.8 (132) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | V | 6.6 (16) | 7.9 (19) | 27.4 (66) | 58.1 (140) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | **All rungs** | 6.8 (66) | 7.0 (67) | 27.4 (264) | 58.8 (567) | 964 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | T | 4.1 (10) | 7.9 (19) | 21.6 (52) | 66.4 (160) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | TL | 7.1 (17) | 7.1 (17) | 27.0 (65) | 58.9 (142) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | TLV | 7.5 (18) | 7.5 (18) | 31.1 (75) | 53.9 (130) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | V | 7.9 (19) | 8.7 (21) | 26.6 (64) | 56.8 (137) | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | **All rungs** | 6.6 (64) | 7.8 (75) | 26.6 (256) | 59.0 (569) | 964 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | T | 6.6 (16) | 9.1 (22) | 20.3 (49) | 63.9 (154) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | TL | 5.4 (13) | 6.6 (16) | 27.4 (66) | 60.6 (146) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | TLV | 7.9 (19) | 6.6 (16) | 32.0 (77) | 53.5 (129) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | V | 6.6 (16) | 7.5 (18) | 27.8 (67) | 58.1 (140) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | **All rungs** | 6.6 (64) | 7.5 (72) | 26.9 (259) | 59.0 (569) | 964 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | T | 6.6 (16) | 10.8 (26) | 18.7 (45) | 63.9 (154) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | TL | 7.9 (19) | 8.3 (20) | 25.7 (62) | 58.1 (140) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | TLV | 6.2 (15) | 9.1 (22) | 29.5 (71) | 55.2 (133) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | V | 7.1 (17) | 10.0 (24) | 25.3 (61) | 57.7 (139) | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | **All rungs** | 7.0 (67) | 9.5 (92) | 24.8 (239) | 58.7 (566) | 964 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | T | 6.2 (15) | 7.5 (18) | 22.0 (53) | 64.3 (155) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | TL | 7.5 (18) | 6.6 (16) | 27.4 (66) | 58.5 (141) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | TLV | 9.5 (23) | 7.9 (19) | 30.7 (74) | 51.9 (125) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | V | 7.9 (19) | 9.1 (22) | 26.1 (63) | 56.8 (137) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | **All rungs** | 7.8 (75) | 7.8 (75) | 26.6 (256) | 57.9 (558) | 964 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | T | 3.3 (8) | 11.2 (27) | 18.3 (44) | 67.2 (162) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | TL | 5.8 (14) | 11.6 (28) | 22.4 (54) | 60.2 (145) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | TLV | 6.2 (15) | 11.2 (27) | 27.4 (66) | 55.2 (133) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | V | 7.5 (18) | 9.5 (23) | 25.7 (62) | 57.3 (138) | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | **All rungs** | 5.7 (55) | 10.9 (105) | 23.4 (226) | 60.0 (578) | 964 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | T | 2.5 (1) | 5.0 (2) | 20.0 (8) | 72.5 (29) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | TL | 10.0 (4) | 5.0 (2) | 25.0 (10) | 60.0 (24) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | TLV | 5.0 (2) | 2.5 (1) | 45.0 (18) | 47.5 (19) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | V | 7.5 (3) | 12.5 (5) | 30.0 (12) | 50.0 (20) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | **All rungs** | 6.2 (10) | 6.2 (10) | 30.0 (48) | 57.5 (92) | 160 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | T | 2.5 (1) | 5.0 (2) | 20.0 (8) | 72.5 (29) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | TL | 12.5 (5) | 2.5 (1) | 27.5 (11) | 57.5 (23) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | TLV | 7.5 (3) | 10.0 (4) | 37.5 (15) | 45.0 (18) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | V | 10.0 (4) | 12.5 (5) | 30.0 (12) | 47.5 (19) | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | **All rungs** | 8.1 (13) | 7.5 (12) | 28.7 (46) | 55.6 (89) | 160 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | T | 2.5 (1) | 10.0 (4) | 15.0 (6) | 72.5 (29) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | TL | 12.5 (5) | 5.0 (2) | 25.0 (10) | 57.5 (23) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | TLV | 12.5 (5) | 7.5 (3) | 40.0 (16) | 40.0 (16) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | V | 12.5 (5) | 15.0 (6) | 27.5 (11) | 45.0 (18) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | **All rungs** | 10.0 (16) | 9.4 (15) | 26.9 (43) | 53.8 (86) | 160 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | T | 5.0 (2) | 2.5 (1) | 22.5 (9) | 70.0 (28) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | TL | 7.5 (3) | 0.0 (0) | 30.0 (12) | 62.5 (25) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | TLV | 5.0 (2) | 12.5 (5) | 35.0 (14) | 47.5 (19) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | V | 2.5 (1) | 15.0 (6) | 27.5 (11) | 55.0 (22) | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | **All rungs** | 5.0 (8) | 7.5 (12) | 28.7 (46) | 58.8 (94) | 160 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | T | 2.5 (1) | 10.0 (4) | 15.0 (6) | 72.5 (29) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | TL | 7.5 (3) | 7.5 (3) | 22.5 (9) | 62.5 (25) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | TLV | 10.0 (4) | 17.5 (7) | 30.0 (12) | 42.5 (17) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | V | 7.5 (3) | 12.5 (5) | 30.0 (12) | 50.0 (20) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | **All rungs** | 6.9 (11) | 11.9 (19) | 24.4 (39) | 56.9 (91) | 160 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | T | 5.0 (2) | 5.0 (2) | 20.0 (8) | 70.0 (28) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | TL | 5.0 (2) | 0.0 (0) | 30.0 (12) | 65.0 (26) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | TLV | 5.0 (2) | 12.5 (5) | 35.0 (14) | 47.5 (19) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | V | 7.5 (3) | 17.5 (7) | 25.0 (10) | 50.0 (20) | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | **All rungs** | 5.6 (9) | 8.8 (14) | 27.5 (44) | 58.1 (93) | 160 |
| n (per col) | - | - | - | - | - | - | - | - |

### Selection: paired verdict transitions from the oracle page set, by evidence source

> **swept**: page_set transition (oracle → each sufficiency rule / +k distractors) × ranking source × evidence source · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **pivot**: oracle cells loaded from g1-representation-full by the builder and paired per (question, rung) · **pairing**: within-question, oracle and perturbed page set both status==ok; pooled over the four rungs · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: does a dropped gold page or an added distractor cost text-carried and graphical evidence alike, or land on one of them

_Same pairing as the by-rung table (see it for the definition), POOLED over the four rungs: paired n counts (question, rung) cells and `questions` counts the distinct questions behind them, so paired n is about four times `questions`. The four transition columns are PERCENTAGES of that row's paired n and sum to 100 per row; the figure in parentheses is the raw cell count behind the percentage. A question citing several evidence sources is counted under each of them, so the per-source rows overlap and CANNOT be summed. The bolded All sources row closing each transition is computed fresh over every paired cell, each counted once, and is a pooled total rather than a column sum. † marks a row computed on fewer than 30 distinct questions, where one question moves the percentages by more than three points: read the direction, not the value._

| block | transition | ranker | evidence_source | wrong→right (%) | right→wrong (%) | right→right (%) | wrong→wrong (%) | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | (none)† | 5.0 (1) | 5.0 (1) | 15.0 (3) | 75.0 (15) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | Chart | 1.6 (5) | 15.4 (48) | 8.0 (25) | 75.0 (234) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | Figure | 3.5 (16) | 20.0 (91) | 7.0 (32) | 69.5 (317) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | Generalized-text (Layout) | 4.2 (10) | 22.9 (55) | 9.6 (23) | 63.3 (152) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | Pure-text (Plain-text) | 2.3 (12) | 23.7 (124) | 13.7 (72) | 60.3 (316) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | Table | 2.3 (10) | 22.2 (96) | 10.0 (43) | 65.5 (283) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | **All sources** | 2.7 (38) | 22.4 (316) | 10.0 (141) | 64.8 (913) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | (none)† | 0.0 (0) | 0.0 (0) | 20.0 (4) | 80.0 (16) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | Chart | 2.6 (8) | 14.7 (46) | 8.7 (27) | 74.0 (231) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | Figure | 3.5 (16) | 16.9 (77) | 10.1 (46) | 69.5 (317) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | Generalized-text (Layout) | 2.9 (7) | 21.2 (51) | 11.2 (27) | 64.6 (155) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | Pure-text (Plain-text) | 3.2 (17) | 23.7 (124) | 13.7 (72) | 59.4 (311) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | Table | 4.2 (18) | 23.1 (100) | 9.0 (39) | 63.7 (275) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | **All sources** | 3.2 (45) | 21.1 (297) | 11.4 (160) | 64.3 (906) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | (none)† | 0.0 (0) | 0.0 (0) | 20.0 (4) | 80.0 (16) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | Chart | 2.9 (9) | 14.7 (46) | 8.7 (27) | 73.7 (230) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | Figure | 3.1 (14) | 17.3 (79) | 9.6 (44) | 70.0 (319) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | Generalized-text (Layout) | 4.2 (10) | 22.9 (55) | 9.6 (23) | 63.3 (152) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | Pure-text (Plain-text) | 3.2 (17) | 22.1 (116) | 15.3 (80) | 59.4 (311) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | Table | 3.7 (16) | 24.8 (107) | 7.4 (32) | 64.1 (277) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | **All sources** | 2.9 (41) | 21.4 (302) | 11.0 (155) | 64.6 (910) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | (none)† | 5.0 (1) | 0.0 (0) | 20.0 (4) | 75.0 (15) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | Chart | 1.9 (6) | 15.4 (48) | 8.0 (25) | 74.7 (233) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | Figure | 3.5 (16) | 20.6 (94) | 6.4 (29) | 69.5 (317) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | Generalized-text (Layout) | 5.8 (14) | 24.2 (58) | 8.3 (20) | 61.7 (148) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | Pure-text (Plain-text) | 2.3 (12) | 21.9 (115) | 15.5 (81) | 60.3 (316) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | Table | 2.5 (11) | 23.6 (102) | 8.6 (37) | 65.3 (282) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | **All sources** | 2.8 (39) | 22.3 (314) | 10.2 (143) | 64.8 (912) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | (none)† | 0.0 (0) | 20.0 (4) | 0.0 (0) | 80.0 (16) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | Chart | 1.9 (6) | 16.0 (50) | 7.4 (23) | 74.7 (233) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | Figure | 1.8 (8) | 20.2 (92) | 6.8 (31) | 71.3 (325) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | Generalized-text (Layout) | 2.9 (7) | 25.8 (62) | 6.7 (16) | 64.6 (155) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | Pure-text (Plain-text) | 1.7 (9) | 26.7 (140) | 10.7 (56) | 60.9 (319) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | Table | 3.9 (17) | 25.7 (111) | 6.5 (28) | 63.9 (276) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | **All sources** | 2.1 (30) | 24.4 (344) | 8.0 (113) | 65.4 (921) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | (none)† | 5.0 (1) | 20.0 (4) | 0.0 (0) | 75.0 (15) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | Chart | 1.3 (4) | 17.3 (54) | 6.1 (19) | 75.3 (235) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | Figure | 3.3 (15) | 23.0 (105) | 3.9 (18) | 69.7 (318) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | Generalized-text (Layout) | 4.2 (10) | 26.7 (64) | 5.8 (14) | 63.3 (152) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | Pure-text (Plain-text) | 1.3 (7) | 25.6 (134) | 11.8 (62) | 61.3 (321) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | Table | 2.3 (10) | 24.1 (104) | 8.1 (35) | 65.5 (283) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | **All sources** | 2.3 (32) | 24.9 (350) | 7.6 (107) | 65.3 (919) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | (none)† | 0.0 (0) | 20.0 (4) | 0.0 (0) | 80.0 (16) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | Chart | 0.6 (2) | 17.0 (53) | 6.4 (20) | 76.0 (237) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | Figure | 2.9 (13) | 22.4 (102) | 4.6 (21) | 70.2 (320) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | Generalized-text (Layout) | 2.9 (7) | 23.8 (57) | 8.8 (21) | 64.6 (155) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | Pure-text (Plain-text) | 1.1 (6) | 27.3 (143) | 10.1 (53) | 61.5 (322) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | Table | 2.3 (10) | 22.7 (98) | 9.5 (41) | 65.5 (283) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | **All sources** | 2.0 (28) | 24.6 (347) | 7.8 (110) | 65.6 (923) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | (none)† | 0.0 (0) | 20.0 (4) | 0.0 (0) | 80.0 (16) | 20 | 5 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | Chart | 1.6 (5) | 16.3 (51) | 7.1 (22) | 75.0 (234) | 312 | 78 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | Figure | 1.8 (8) | 19.5 (89) | 7.5 (34) | 71.3 (325) | 456 | 114 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | Generalized-text (Layout) | 2.5 (6) | 23.8 (57) | 8.8 (21) | 65.0 (156) | 240 | 60 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | Pure-text (Plain-text) | 1.7 (9) | 27.1 (142) | 10.3 (54) | 60.9 (319) | 524 | 131 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | Table | 3.7 (16) | 24.5 (106) | 7.6 (33) | 64.1 (277) | 432 | 108 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | **All sources** | 2.3 (32) | 23.9 (337) | 8.5 (120) | 65.3 (919) | 1408 | 352 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | (none)† | 8.9 (5) | 3.6 (2) | 67.9 (38) | 19.6 (11) | 56 | 14 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | Chart | 5.2 (20) | 6.2 (24) | 32.5 (126) | 56.2 (218) | 388 | 97 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | Figure | 6.5 (42) | 4.6 (30) | 30.6 (198) | 58.3 (378) | 648 | 162 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | Generalized-text (Layout) | 2.7 (6) | 9.4 (21) | 42.9 (96) | 45.1 (101) | 224 | 56 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | Pure-text (Plain-text) | 7.2 (44) | 3.1 (19) | 53.4 (327) | 36.3 (222) | 612 | 153 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | Table | 5.0 (21) | 7.2 (30) | 51.9 (216) | 35.8 (149) | 416 | 104 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | **All sources** | 6.3 (119) | 4.9 (93) | 45.8 (869) | 43.0 (815) | 1896 | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | (none)† | 8.9 (5) | 3.6 (2) | 67.9 (38) | 19.6 (11) | 56 | 14 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | Chart | 7.5 (29) | 7.5 (29) | 31.2 (121) | 53.9 (209) | 388 | 97 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | Figure | 8.0 (52) | 5.2 (34) | 29.9 (194) | 56.8 (368) | 648 | 162 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | Generalized-text (Layout) | 4.0 (9) | 8.9 (20) | 43.3 (97) | 43.8 (98) | 224 | 56 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | Pure-text (Plain-text) | 8.2 (50) | 6.5 (40) | 50.0 (306) | 35.3 (216) | 612 | 153 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | Table | 6.2 (26) | 7.0 (29) | 52.2 (217) | 34.6 (144) | 416 | 104 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | **All sources** | 7.8 (147) | 6.5 (124) | 44.2 (838) | 41.5 (787) | 1896 | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | (none)† | 5.4 (3) | 1.8 (1) | 69.6 (39) | 23.2 (13) | 56 | 14 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | Chart | 5.7 (22) | 7.0 (27) | 31.7 (123) | 55.7 (216) | 388 | 97 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | Figure | 8.0 (52) | 5.6 (36) | 29.6 (192) | 56.8 (368) | 648 | 162 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | Generalized-text (Layout) | 2.2 (5) | 9.4 (21) | 42.9 (96) | 45.5 (102) | 224 | 56 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | Pure-text (Plain-text) | 6.7 (41) | 4.7 (29) | 51.8 (317) | 36.8 (225) | 612 | 153 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | Table | 6.5 (27) | 7.2 (30) | 51.9 (216) | 34.4 (143) | 416 | 104 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | **All sources** | 6.9 (130) | 6.2 (118) | 44.5 (844) | 42.4 (804) | 1896 | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | (none)† | 7.1 (4) | 5.4 (3) | 66.1 (37) | 21.4 (12) | 56 | 14 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | Chart | 7.0 (27) | 7.7 (30) | 30.9 (120) | 54.4 (211) | 388 | 97 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | Figure | 9.6 (62) | 7.4 (48) | 27.8 (180) | 55.2 (358) | 648 | 162 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | Generalized-text (Layout) | 3.6 (8) | 9.4 (21) | 42.9 (96) | 44.2 (99) | 224 | 56 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | Pure-text (Plain-text) | 7.8 (48) | 5.9 (36) | 50.7 (310) | 35.6 (218) | 612 | 153 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | Table | 6.5 (27) | 5.8 (24) | 53.4 (222) | 34.4 (143) | 416 | 104 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | **All sources** | 8.1 (154) | 7.1 (134) | 43.7 (828) | 41.1 (780) | 1896 | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | (none)† | 5.4 (3) | 3.6 (2) | 67.9 (38) | 23.2 (13) | 56 | 14 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | Chart | 8.2 (32) | 8.8 (34) | 29.9 (116) | 53.1 (206) | 388 | 97 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | Figure | 8.8 (57) | 6.2 (40) | 29.0 (188) | 56.0 (363) | 648 | 162 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | Generalized-text (Layout) | 4.0 (9) | 10.7 (24) | 41.5 (93) | 43.8 (98) | 224 | 56 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | Pure-text (Plain-text) | 7.8 (48) | 4.9 (30) | 51.6 (316) | 35.6 (218) | 612 | 153 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | Table | 6.5 (27) | 6.2 (26) | 52.9 (220) | 34.4 (143) | 416 | 104 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | **All sources** | 7.8 (147) | 6.6 (126) | 44.1 (836) | 41.5 (787) | 1896 | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | (none)† | 5.4 (3) | 0.0 (0) | 71.4 (40) | 23.2 (13) | 56 | 14 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | Chart | 8.5 (33) | 11.1 (43) | 27.6 (107) | 52.8 (205) | 388 | 97 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | Figure | 10.5 (68) | 7.3 (47) | 27.9 (181) | 54.3 (352) | 648 | 162 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | Generalized-text (Layout) | 4.0 (9) | 9.4 (21) | 42.9 (96) | 43.8 (98) | 224 | 56 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | Pure-text (Plain-text) | 8.3 (51) | 6.2 (38) | 50.3 (308) | 35.1 (215) | 612 | 153 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | Table | 7.5 (31) | 7.5 (31) | 51.7 (215) | 33.4 (139) | 416 | 104 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | **All sources** | 8.8 (167) | 8.0 (152) | 42.7 (810) | 40.5 (767) | 1896 | 474 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | (none)† | 25.0 (4) | 0.0 (0) | 0.0 (0) | 75.0 (12) | 16 | 4 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | Chart | 7.8 (18) | 5.6 (13) | 21.6 (50) | 65.1 (151) | 232 | 58 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | Figure | 4.5 (12) | 5.3 (14) | 22.3 (59) | 67.8 (179) | 264 | 66 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | Generalized-text (Layout) | 5.1 (7) | 5.9 (8) | 32.4 (44) | 56.6 (77) | 136 | 34 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | Pure-text (Plain-text) | 6.2 (23) | 7.1 (26) | 31.8 (117) | 54.9 (202) | 368 | 92 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | Table | 8.6 (33) | 6.8 (26) | 25.0 (96) | 59.6 (229) | 384 | 96 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | **All sources** | 6.8 (66) | 7.0 (67) | 27.4 (264) | 58.8 (567) | 964 | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | (none)† | 25.0 (4) | 0.0 (0) | 0.0 (0) | 75.0 (12) | 16 | 4 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | Chart | 6.9 (16) | 6.9 (16) | 20.3 (47) | 65.9 (153) | 232 | 58 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | Figure | 7.2 (19) | 5.7 (15) | 22.0 (58) | 65.2 (172) | 264 | 66 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | Generalized-text (Layout) | 5.1 (7) | 6.6 (9) | 31.6 (43) | 56.6 (77) | 136 | 34 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | Pure-text (Plain-text) | 4.1 (15) | 7.3 (27) | 31.5 (116) | 57.1 (210) | 368 | 92 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | Table | 6.5 (25) | 7.6 (29) | 24.2 (93) | 61.7 (237) | 384 | 96 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | **All sources** | 6.6 (64) | 7.8 (75) | 26.6 (256) | 59.0 (569) | 964 | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | (none)† | 25.0 (4) | 0.0 (0) | 0.0 (0) | 75.0 (12) | 16 | 4 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | Chart | 7.8 (18) | 5.2 (12) | 22.0 (51) | 65.1 (151) | 232 | 58 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | Figure | 3.4 (9) | 4.9 (13) | 22.7 (60) | 68.9 (182) | 264 | 66 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | Generalized-text (Layout) | 4.4 (6) | 8.8 (12) | 29.4 (40) | 57.4 (78) | 136 | 34 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | Pure-text (Plain-text) | 5.4 (20) | 8.4 (31) | 30.4 (112) | 55.7 (205) | 368 | 92 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | Table | 8.3 (32) | 7.3 (28) | 24.5 (94) | 59.9 (230) | 384 | 96 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | **All sources** | 6.6 (64) | 7.5 (72) | 26.9 (259) | 59.0 (569) | 964 | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | (none)† | 25.0 (4) | 0.0 (0) | 0.0 (0) | 75.0 (12) | 16 | 4 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | Chart | 6.9 (16) | 6.5 (15) | 20.7 (48) | 65.9 (153) | 232 | 58 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | Figure | 8.0 (21) | 7.6 (20) | 20.1 (53) | 64.4 (170) | 264 | 66 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | Generalized-text (Layout) | 3.7 (5) | 14.0 (19) | 24.3 (33) | 58.1 (79) | 136 | 34 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | Pure-text (Plain-text) | 4.9 (18) | 8.4 (31) | 30.4 (112) | 56.2 (207) | 368 | 92 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | Table | 4.9 (19) | 8.9 (34) | 22.9 (88) | 63.3 (243) | 384 | 96 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | **All sources** | 7.0 (67) | 9.5 (92) | 24.8 (239) | 58.7 (566) | 964 | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | (none)† | 31.2 (5) | 0.0 (0) | 0.0 (0) | 68.8 (11) | 16 | 4 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | Chart | 7.3 (17) | 6.9 (16) | 20.3 (47) | 65.5 (152) | 232 | 58 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | Figure | 5.7 (15) | 5.7 (15) | 22.0 (58) | 66.7 (176) | 264 | 66 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | Generalized-text (Layout) | 5.9 (8) | 7.4 (10) | 30.9 (42) | 55.9 (76) | 136 | 34 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | Pure-text (Plain-text) | 6.8 (25) | 6.0 (22) | 32.9 (121) | 54.3 (200) | 368 | 92 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | Table | 6.0 (23) | 7.8 (30) | 24.0 (92) | 62.2 (239) | 384 | 96 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | **All sources** | 7.8 (75) | 7.8 (75) | 26.6 (256) | 57.9 (558) | 964 | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | (none)† | 25.0 (4) | 0.0 (0) | 0.0 (0) | 75.0 (12) | 16 | 4 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | Chart | 5.2 (12) | 9.5 (22) | 17.7 (41) | 67.7 (157) | 232 | 58 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | Figure | 4.2 (11) | 8.3 (22) | 19.3 (51) | 68.2 (180) | 264 | 66 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | Generalized-text (Layout) | 2.9 (4) | 14.0 (19) | 24.3 (33) | 58.8 (80) | 136 | 34 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | Pure-text (Plain-text) | 4.6 (17) | 9.8 (36) | 29.1 (107) | 56.5 (208) | 368 | 92 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | Table | 4.4 (17) | 11.2 (43) | 20.6 (79) | 63.8 (245) | 384 | 96 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | **All sources** | 5.7 (55) | 10.9 (105) | 23.4 (226) | 60.0 (578) | 964 | 241 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | Figure† | 7.9 (6) | 2.6 (2) | 28.9 (22) | 60.5 (46) | 76 | 19 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | Generalized-text (Layout)† | 5.0 (1) | 5.0 (1) | 50.0 (10) | 40.0 (8) | 20 | 5 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | Pure-text (Plain-text)† | 5.9 (4) | 10.3 (7) | 26.5 (18) | 57.4 (39) | 68 | 17 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | Table† | 3.6 (1) | 14.3 (4) | 32.1 (9) | 50.0 (14) | 28 | 7 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | **All sources** | 6.2 (10) | 6.2 (10) | 30.0 (48) | 57.5 (92) | 160 | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | Figure† | 9.2 (7) | 7.9 (6) | 23.7 (18) | 59.2 (45) | 76 | 19 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | Generalized-text (Layout)† | 10.0 (2) | 5.0 (1) | 50.0 (10) | 35.0 (7) | 20 | 5 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | Pure-text (Plain-text)† | 8.8 (6) | 7.4 (5) | 29.4 (20) | 54.4 (37) | 68 | 17 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | Table† | 7.1 (2) | 14.3 (4) | 32.1 (9) | 46.4 (13) | 28 | 7 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | **All sources** | 8.1 (13) | 7.5 (12) | 28.7 (46) | 55.6 (89) | 160 | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | Figure† | 13.2 (10) | 3.9 (3) | 27.6 (21) | 55.3 (42) | 76 | 19 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | Generalized-text (Layout)† | 10.0 (2) | 5.0 (1) | 50.0 (10) | 35.0 (7) | 20 | 5 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | Pure-text (Plain-text)† | 10.3 (7) | 10.3 (7) | 26.5 (18) | 52.9 (36) | 68 | 17 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | Table† | 3.6 (1) | 25.0 (7) | 21.4 (6) | 50.0 (14) | 28 | 7 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | **All sources** | 10.0 (16) | 9.4 (15) | 26.9 (43) | 53.8 (86) | 160 | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | Figure† | 6.6 (5) | 10.5 (8) | 21.1 (16) | 61.8 (47) | 76 | 19 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | Generalized-text (Layout)† | 5.0 (1) | 10.0 (2) | 45.0 (9) | 40.0 (8) | 20 | 5 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | Pure-text (Plain-text)† | 2.9 (2) | 2.9 (2) | 33.8 (23) | 60.3 (41) | 68 | 17 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | Table† | 7.1 (2) | 7.1 (2) | 39.3 (11) | 46.4 (13) | 28 | 7 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | **All sources** | 5.0 (8) | 7.5 (12) | 28.7 (46) | 58.8 (94) | 160 | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | Figure† | 9.2 (7) | 7.9 (6) | 23.7 (18) | 59.2 (45) | 76 | 19 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | Generalized-text (Layout)† | 10.0 (2) | 5.0 (1) | 50.0 (10) | 35.0 (7) | 20 | 5 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | Pure-text (Plain-text)† | 4.4 (3) | 11.8 (8) | 25.0 (17) | 58.8 (40) | 68 | 17 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | Table† | 3.6 (1) | 32.1 (9) | 14.3 (4) | 50.0 (14) | 28 | 7 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | **All sources** | 6.9 (11) | 11.9 (19) | 24.4 (39) | 56.9 (91) | 160 | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | Chart† | 0.0 (0) | 0.0 (0) | 33.3 (4) | 66.7 (8) | 12 | 3 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | Figure† | 3.9 (3) | 11.8 (9) | 19.7 (15) | 64.5 (49) | 76 | 19 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | Generalized-text (Layout)† | 10.0 (2) | 20.0 (4) | 35.0 (7) | 35.0 (7) | 20 | 5 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | Pure-text (Plain-text)† | 7.4 (5) | 4.4 (3) | 32.4 (22) | 55.9 (38) | 68 | 17 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | Table† | 7.1 (2) | 7.1 (2) | 39.3 (11) | 46.4 (13) | 28 | 7 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | **All sources** | 5.6 (9) | 8.8 (14) | 27.5 (44) | 58.1 (93) | 160 | 40 |
| n (per col) | - | - | - | - | - | - | - | - | - |

### Withholding gold pages: verdict flips from the oracle page set, by evidence source

> **swept**: withheld/isolated gold page × evidence source (both flip directions) · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **ranker**: colqwen3 only, matching the main text and figure · **pairing**: within-question against the oracle, pooled over the four rungs · **reading**: R→W is what the change breaks, W→R what it repairs; the pair is the whole effect

_Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. Rung and ranker match the main text and the selection figure, so the All sources rows reproduce that figure's two flip columns exactly and these tables are its per-source breakdown. R→W is the share of oracle-correct cells the change breaks and W→R the share of oracle-wrong cells it repairs, both as percentages of that row's paired n, so the two columns are the loss and the gain of the same change and their difference is its net effect. A question citing several evidence sources appears under each, so the per-source rows OVERLAP and cannot be summed; the bolded All sources row is computed fresh over every paired cell counted once. † marks a row over fewer than 30 distinct questions._

| evidence_source | drop lowest gold R→W | drop lowest gold W→R | drop highest gold R→W | drop highest gold W→R | keep highest only R→W | keep highest only W→R | keep lowest only R→W | keep lowest only W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| (none)† | 0.0 | 0.0 | 0.0 | 20.0 | 20.0 | 0.0 | 20.0 | 20.0 | 5 | 5 |
| Chart | 19.2 | 3.8 | 20.5 | 2.6 | 19.2 | 1.3 | 21.8 | 0.0 | 78 | 78 |
| Figure | 26.3 | 4.4 | 31.6 | 5.3 | 29.8 | 2.6 | 36.0 | 4.4 | 114 | 114 |
| Generalized-text (Layout) | 25.0 | 5.0 | 31.7 | 10.0 | 28.3 | 1.7 | 35.0 | 5.0 | 60 | 60 |
| Pure-text (Plain-text) | 26.7 | 3.1 | 26.7 | 3.1 | 31.3 | 0.8 | 30.5 | 0.8 | 131 | 131 |
| Table | 22.2 | 5.6 | 22.2 | 1.9 | 25.0 | 3.7 | 24.1 | 0.9 | 108 | 108 |
| **All sources** | 24.7 | 4.5 | 27.0 | 4.3 | 28.4 | 2.6 | 30.4 | 2.3 | 352 | 352 |
| n (per col) | - | - | - | - | - | - | - | - | - | - |

### Adding distractor pages: verdict flips from the oracle page set, by evidence source

> **swept**: added distractor count × gold count × evidence source (both flip directions) · **dataset**: mmlongbench · **scan**: any · **sampling**: full (hop: multi) · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: page_set rule (colqwen3 / bm25 ranking) · **prompt_mode**: none · **ranker**: colqwen3 only, matching the main text and figure · **pairing**: within-question against the oracle, pooled over the four rungs · **blocks**: one block per gold-page count; each reads against its own d=0 oracle and blocks are not comparable

_Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. Rung and ranker match the main text and the selection figure, so the All sources rows reproduce that figure's two flip columns exactly and these tables are its per-source breakdown. R→W is the share of oracle-correct cells the change breaks and W→R the share of oracle-wrong cells it repairs, both as percentages of that row's paired n, so the two columns are the loss and the gain of the same change and their difference is its net effect. A question citing several evidence sources appears under each, so the per-source rows OVERLAP and cannot be summed; the bolded All sources row is computed fresh over every paired cell counted once. † marks a row over fewer than 30 distinct questions._

| gold pages | evidence_source | +1 distractor R→W | +1 distractor W→R | +2 distractors R→W | +2 distractors W→R | +3 distractors R→W | +3 distractors W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 gold page | (none)† | 0.0 | 14.3 | 0.0 | 14.3 | 0.0 | 14.3 | 14 | 14 |
| 1 gold page | Chart | 9.3 | 7.2 | 10.3 | 9.3 | 17.5 | 8.2 | 97 | 97 |
| 1 gold page | Figure | 7.4 | 6.8 | 11.1 | 10.5 | 9.3 | 9.9 | 162 | 162 |
| 1 gold page | Generalized-text (Layout) | 10.7 | 5.4 | 8.9 | 7.1 | 7.1 | 3.6 | 56 | 56 |
| 1 gold page | Pure-text (Plain-text) | 7.2 | 6.5 | 5.9 | 5.9 | 7.2 | 5.9 | 153 | 153 |
| 1 gold page | Table | 8.7 | 4.8 | 5.8 | 3.8 | 6.7 | 6.7 | 104 | 104 |
| 1 gold page | **All sources** | 7.8 | 7.0 | 8.2 | 8.0 | 9.7 | 8.2 | 474 | 474 |
| 2-3 gold pages | (none)† | 0.0 | 25.0 | 0.0 | 25.0 | 0.0 | 25.0 | 4 | 4 |
| 2-3 gold pages | Chart | 4.9 | 8.2 | 6.6 | 4.9 | 9.8 | 8.2 | 61 | 61 |
| 2-3 gold pages | Figure | 7.1 | 9.4 | 8.2 | 5.9 | 10.6 | 2.4 | 85 | 85 |
| 2-3 gold pages | Generalized-text (Layout) | 5.1 | 7.7 | 15.4 | 2.6 | 20.5 | 7.7 | 39 | 39 |
| 2-3 gold pages | Pure-text (Plain-text) | 8.3 | 4.6 | 10.1 | 4.6 | 11.0 | 4.6 | 109 | 109 |
| 2-3 gold pages | Table | 7.8 | 7.8 | 6.8 | 4.9 | 8.7 | 4.9 | 103 | 103 |
| 2-3 gold pages | **All sources** | 7.8 | 7.5 | 9.6 | 6.0 | 11.4 | 6.0 | 281 | 281 |
| n (per col) | - | - | - | - | - | - | - | - | - |

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
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 at every depth, from the full rankings

> **swept**: retriever × k ∈ {1,3,5,7,10} (complete depth sweep, P/R/F1 as %) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **page_selection**: retrieved (bm25 text / colqwen2.5 vision / joint) · **prompt_mode**: none · **units**: PERCENTAGES, unlike the other retrieval tables · **provenance column**: measured = read off the side artifact; derived (union) = a joint arm rebuilt from its two constituents at the same depth, after the union rule is verified against every stored joint row

_P/R/F1 as PERCENTAGES (the other retrieval tables emit fractions), macro-averaged over the 847 answerable questions, one row per (retriever, k). Every cell is computed from the retrieval MEMO (`results/cache/<run_tag>/retrieval/<name>__dpi<dpi>.jsonl`), which stores each retriever's complete ranking of a document's pages independent of depth. `retrieval.jsonl` stores only the depths a sweep was configured to score, and the G2 run scored fewer for the joint arms and for qwen3-embedding, which was re-run separately after an OOM by `ops/scripts/complete_retrieval.py` — that tool writes the memo and leaves `retrieval.jsonl` alone by design, and the merge back was never done. The `provenance` column says which: `scored` means a row for that depth also exists in `retrieval.jsonl`, `from ranking` means the depth is read off the same stored ranking without re-running anything. The memo is checked before any of it is used: 26257 scored rows reproduced exactly from the memo, across every retriever and depth `retrieval.jsonl` does carry, so the two agree wherever they overlap. Recovered here: bge-m3|colqwen2.5 k=7, bge-m3|colqwen2.5 k=10, bm25|colmodernvbert k=7, bm25|colmodernvbert k=10. No cell is missing. Note a joint arm at depth k returns up to 2k pages, so its precision is measured over a larger page set than a single arm at the same k._

| retriever | modality | k | P | R | F1 | n | provenance |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 33.8 | 25.5 | 27.9 | 847 | scored |
| bge-m3 | text | 3 | 18.7 | 38.8 | 23.9 | 847 | scored |
| bge-m3 | text | 5 | 14.7 | 48.2 | 21.2 | 847 | scored |
| bge-m3 | text | 7 | 12.0 | 53.2 | 18.4 | 847 | scored |
| bge-m3 | text | 10 | 10.0 | 61.1 | 16.3 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 1 | 48.5 | 55.2 | 48.6 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 3 | 23.4 | 72.8 | 33.2 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 5 | 16.7 | 79.8 | 25.9 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 7 | 13.4 | 83.7 | 21.6 | 847 | from ranking |
| bge-m3\|colqwen2.5 | joint | 10 | 10.7 | 87.5 | 17.9 | 847 | from ranking |
| bm25 | text | 1 | 29.5 | 22.2 | 24.2 | 847 | scored |
| bm25 | text | 3 | 18.5 | 37.8 | 23.4 | 847 | scored |
| bm25 | text | 5 | 14.0 | 46.0 | 20.1 | 847 | scored |
| bm25 | text | 7 | 11.4 | 50.8 | 17.5 | 847 | scored |
| bm25 | text | 10 | 9.5 | 58.5 | 15.4 | 847 | scored |
| bm25\|colmodernvbert | joint | 1 | 44.2 | 51.2 | 44.5 | 847 | scored |
| bm25\|colmodernvbert | joint | 3 | 22.3 | 69.8 | 31.6 | 847 | scored |
| bm25\|colmodernvbert | joint | 5 | 15.9 | 77.6 | 24.8 | 847 | scored |
| bm25\|colmodernvbert | joint | 7 | 12.6 | 81.2 | 20.5 | 847 | from ranking |
| bm25\|colmodernvbert | joint | 10 | 10.2 | 85.3 | 17.2 | 847 | from ranking |
| colmodernvbert | vision | 1 | 58.8 | 46.0 | 49.6 | 847 | scored |
| colmodernvbert | vision | 3 | 31.5 | 64.6 | 39.6 | 847 | scored |
| colmodernvbert | vision | 5 | 22.7 | 72.5 | 32.2 | 847 | scored |
| colmodernvbert | vision | 7 | 17.9 | 77.2 | 27.1 | 847 | scored |
| colmodernvbert | vision | 10 | 14.0 | 81.7 | 22.2 | 847 | scored |
| colqwen2.5 | vision | 1 | 63.3 | 48.8 | 52.8 | 847 | scored |
| colqwen2.5 | vision | 3 | 33.8 | 68.3 | 42.5 | 847 | scored |
| colqwen2.5 | vision | 5 | 23.6 | 74.9 | 33.5 | 847 | scored |
| colqwen2.5 | vision | 7 | 18.5 | 79.2 | 27.9 | 847 | scored |
| colqwen2.5 | vision | 10 | 14.4 | 83.8 | 22.9 | 847 | scored |
| colqwen3 | vision | 1 | 70.2 | 54.1 | 58.6 | 847 | scored |
| colqwen3 | vision | 3 | 36.8 | 73.9 | 46.0 | 847 | scored |
| colqwen3 | vision | 5 | 25.5 | 80.6 | 36.1 | 847 | scored |
| colqwen3 | vision | 7 | 19.9 | 83.9 | 29.9 | 847 | scored |
| colqwen3 | vision | 10 | 15.2 | 87.4 | 24.1 | 847 | scored |
| n (per col) | - | - | - | - | - | - | - |

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
| n (per col) | - | - | - | - | - | - | - |

### Top-k sweep: accuracy vs retrieval depth by modality

> **swept**: retrieval depth k · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV/V · **pool**: answerable · **prompt_mode**: none · **inference arms**: spec ran bge-m3 text / colqwen2.5 vision / joint; BASELINE captions the text arm as bm25 (the config default the spec overrode) — cite the spec · **status**: PROVISIONAL (partial G2 pool)

| k | text | vision | joint | n |
| --- | --- | --- | --- | --- |
| 1 | 18.0 [13.1-23.3] | 32.7 [26.7-38.5] | 36.4 [31.5-41.2] | 1779 |
| 3 | 24.3 [18.7-30.5] | 37.6 [32.2-43.3] | 37.6 [31.6-43.7] | 1490 |
| 5 | 22.3 [16.7-29.0] | 38.1 [31.8-44.4] | 36.8 [29.7-44.2] | 1024 |
| 7 | 42.9 [42.9-42.9] | 28.6 [28.6-28.6] | 50.0 [50.0-50.0] | 18 |
| n (per col) | 1523 | 1538 | 1250 | - |

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

## Integration

### Integration: accuracy by evidence hop, per doc_type and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse._

| doc_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 34.5 [20.7-48.2] | 39.7 [26.5-53.6] | +5.2 | 152 |
| Academic paper | TL | 29.8 [17.9-41.6] | 38.2 [25.0-52.7] | +8.5 | 152 |
| Academic paper | TV | 46.4 [32.2-59.5] | 44.1 [31.1-56.8] | -2.3 | 152 |
| Academic paper | TLV | 39.3 [26.8-51.8] | 47.1 [33.3-60.0] | +7.8 | 152 |
| Academic paper | V | 31.0 [20.3-40.6] | 38.2 [26.9-50.8] | +7.3 | 152 |
| Administration/Industry file | T | 58.5 [38.3-80.6] | 40.0 [11.8-61.9] | -18.5 | 61 |
| Administration/Industry file | TL | 68.3 [57.4-81.1] | 40.0 [7.1-63.6] | -28.3 | 61 |
| Administration/Industry file | TV | 80.5 [66.0-100.0] | 50.0 [23.5-69.6] | -30.5 | 61 |
| Administration/Industry file | TLV | 87.8 [78.0-100.0] | 35.0 [17.6-46.4] | -52.8 | 61 |
| Administration/Industry file | V | 68.3 [57.4-81.2] | 35.0 [17.6-46.4] | -33.3 | 61 |
| Brochure | T | 24.5 [14.6-35.2] | 35.7 [13.0-59.3] | +11.2 | 77 |
| Brochure | TL | 30.6 [18.6-44.7] | 35.7 [16.1-54.8] | +5.1 | 77 |
| Brochure | TV | 42.9 [29.5-55.6] | 50.0 [27.6-73.1] | +7.1 | 77 |
| Brochure | TLV | 51.0 [34.6-68.2] | 35.7 [16.0-53.8] | -15.3 | 77 |
| Brochure | V | 44.9 [26.7-63.8] | 32.1 [12.0-55.6] | -12.8 | 77 |
| Financial report | T | 60.3 [46.3-72.9] | 34.1 [26.2-44.1] | -26.2 | 107 |
| Financial report | TL | 68.3 [56.1-77.6] | 31.8 [18.5-48.6] | -36.4 | 107 |
| Financial report | TV | 71.4 [60.0-84.3] | 20.5 [10.0-36.4] | -51.0 | 107 |
| Financial report | TLV | 74.6 [68.1-83.1] | 20.5 [10.4-32.4] | -54.1 | 107 |
| Financial report | V | 52.4 [38.7-70.4] | 20.5 [10.9-33.3] | -31.9 | 107 |
| Guidebook | T | 42.5 [27.1-59.2] | 25.5 [10.4-41.3] | -16.9 | 120 |
| Guidebook | TL | 46.6 [32.8-60.8] | 29.8 [14.3-46.0] | -16.8 | 120 |
| Guidebook | TV | 56.2 [42.1-69.3] | 38.3 [21.7-56.4] | -17.9 | 120 |
| Guidebook | TLV | 60.3 [45.5-74.4] | 38.3 [22.7-54.4] | -22.0 | 120 |
| Guidebook | V | 53.4 [40.0-66.7] | 31.9 [19.6-44.4] | -21.5 | 120 |
| Research report / Introduction | T | 28.0 [16.8-39.8] | 17.1 [9.4-26.2] | -10.9 | 212 |
| Research report / Introduction | TL | 34.6 [23.2-46.2] | 20.0 [12.6-27.6] | -14.6 | 212 |
| Research report / Introduction | TV | 61.7 [49.5-72.2] | 31.4 [20.0-41.6] | -30.3 | 212 |
| Research report / Introduction | TLV | 64.5 [53.5-75.0] | 30.5 [20.8-39.1] | -34.0 | 212 |
| Research report / Introduction | V | 61.7 [49.1-73.9] | 28.6 [19.0-36.7] | -33.1 | 212 |
| Tutorial/Workshop | T | 23.8 [9.4-37.7] | 0.0 [0.0-0.0] | -23.8 | 109 |
| Tutorial/Workshop | TL | 54.0 [40.0-68.3] | 41.3 [28.6-52.0] | -12.7 | 109 |
| Tutorial/Workshop | TV | 84.1 [75.8-91.7] | 52.2 [40.6-61.5] | -32.0 | 109 |
| Tutorial/Workshop | TLV | 81.0 [71.2-89.8] | 65.2 [50.0-80.0] | -15.7 | 109 |
| Tutorial/Workshop | V | 81.0 [71.6-89.8] | 52.2 [40.6-61.5] | -28.8 | 109 |
| **all doc_types** | **T** | **37.3 [31.1-43.3]** | **25.1 [19.8-30.8]** | **-12.2** | **838** |
| **all doc_types** | **TL** | **45.0 [39.0-50.6]** | **31.3 [25.6-36.7]** | **-13.7** | **838** |
| **all doc_types** | **TV** | **62.1 [56.6-67.6]** | **38.5 [32.6-45.2]** | **-23.5** | **838** |
| **all doc_types** | **TLV** | **63.5 [58.1-68.8]** | **38.5 [32.6-44.7]** | **-25.0** | **838** |
| **all doc_types** | **V** | **55.2 [49.8-60.8]** | **33.5 [28.7-38.6]** | **-21.7** | **838** |
| n (per col) | - | 2400 | 1790 | - | - |

### Integration: accuracy by evidence hop, per evidence source and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × evidence source × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. T/TL/TLV/V come from g4-faithfulness-full prompt_mode=none and TV from g1-tv-full; those are two run_tags but one pool, because the TV spec pins every axis to g4 prompt_mode=none (same reasoner, resolution, oracle pages, prompt, and the same 847 questions), so the rungs pair question-for-question. TV is the parser-free image rung (PyMuPDF embedded text plus page images), sitting between TL and TLV in cost, so TV->TLV is what the parser buys once the model can already see the page. The V100 version of this table ran on ~130 fewer questions, and that loss was not random: OOM tracks page count and length, so it dropped the long, high-page, multi-hop ones. Structure, columns, groupings and per-cell n match that earlier table; the size of the shift is in the reconciliation tables under Reconciliation & coverage. hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse. Blocks are the evidence modality a question draws on, replacing the document class of the doc_type integration table; the hop split, pins, and gap column are identical. A question can cite SEVERAL sources (e.g. Chart + Table) and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus. The bolded All sources rows pool every question exactly once and are therefore NOT a column sum of the blocks above them. Per-cell n rides inline on the single and multi columns: OOM attrition is rung-dependent and the multi cells at TLV are thin, where a small n reads as survivorship, not signal._

| evidence_source | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 [42.9-85.7] (n=14) | 20.0 [0.0-60.0] (n=5) | -44.3 | 19 |
| (none) | TL | 78.6 [53.8-100.0] (n=14) | 20.0 [0.0-60.0] (n=5) | -58.6 | 19 |
| (none) | TV | 85.7 [66.7-100.0] (n=14) | 20.0 [0.0-60.0] (n=5) | -65.7 | 19 |
| (none) | TLV | 92.9 [76.9-100.0] (n=14) | 20.0 [0.0-60.0] (n=5) | -72.9 | 19 |
| (none) | V | 64.3 [40.0-85.7] (n=14) | 20.0 [0.0-60.0] (n=5) | -44.3 | 19 |
| Chart | T | 20.4 [12.5-29.6] (n=98) | 16.5 [8.5-25.6] (n=79) | -4.0 | 177 |
| Chart | TL | 19.4 [11.6-27.7] (n=98) | 19.0 [11.0-28.8] (n=79) | -0.4 | 177 |
| Chart | TV | 53.1 [40.6-64.4] (n=98) | 29.1 [18.3-41.4] (n=79) | -23.9 | 177 |
| Chart | TLV | 56.1 [44.7-66.7] (n=98) | 32.9 [21.8-44.2] (n=79) | -23.2 | 177 |
| Chart | V | 54.1 [41.6-65.6] (n=98) | 30.4 [21.6-41.4] (n=79) | -23.7 | 177 |
| Figure | T | 19.3 [13.4-25.9] (n=166) | 10.1 [4.4-16.7] (n=119) | -9.2 | 285 |
| Figure | TL | 25.3 [18.1-33.0] (n=166) | 21.8 [13.5-30.1] (n=119) | -3.5 | 285 |
| Figure | TV | 50.6 [42.8-58.1] (n=166) | 39.5 [30.6-47.7] (n=119) | -11.1 | 285 |
| Figure | TLV | 49.4 [40.9-57.8] (n=166) | 39.5 [28.4-49.1] (n=119) | -9.9 | 285 |
| Figure | V | 45.8 [37.2-52.9] (n=166) | 33.6 [24.3-41.7] (n=119) | -12.2 | 285 |
| Generalized-text (Layout) | T | 30.4 [15.8-43.9] (n=56) | 26.7 [14.8-41.1] (n=60) | -3.7 | 116 |
| Generalized-text (Layout) | TL | 44.6 [32.3-57.7] (n=56) | 31.7 [18.6-45.0] (n=60) | -13.0 | 116 |
| Generalized-text (Layout) | TV | 60.7 [48.3-73.3] (n=56) | 40.0 [26.8-52.4] (n=60) | -20.7 | 116 |
| Generalized-text (Layout) | TLV | 66.1 [54.4-78.2] (n=56) | 38.3 [25.0-51.4] (n=60) | -27.7 | 116 |
| Generalized-text (Layout) | V | 55.4 [41.7-70.0] (n=56) | 35.0 [23.3-46.8] (n=60) | -20.4 | 116 |
| Pure-text (Plain-text) | T | 46.8 [36.6-58.1] (n=154) | 31.3 [21.5-42.0] (n=134) | -15.4 | 288 |
| Pure-text (Plain-text) | TL | 56.5 [45.5-67.3] (n=154) | 38.8 [29.9-48.5] (n=134) | -17.7 | 288 |
| Pure-text (Plain-text) | TV | 64.3 [53.5-75.2] (n=154) | 42.5 [32.6-52.9] (n=134) | -21.7 | 288 |
| Pure-text (Plain-text) | TLV | 67.5 [56.7-78.4] (n=154) | 42.5 [33.9-52.1] (n=134) | -25.0 | 288 |
| Pure-text (Plain-text) | V | 53.9 [44.3-64.3] (n=154) | 34.3 [26.4-42.5] (n=134) | -19.6 | 288 |
| Table | T | 47.1 [36.8-56.3] (n=104) | 35.5 [27.8-43.4] (n=110) | -11.7 | 214 |
| Table | TL | 66.3 [57.4-75.0] (n=104) | 32.7 [23.1-42.7] (n=110) | -33.6 | 214 |
| Table | TV | 66.3 [58.0-75.5] (n=104) | 30.0 [21.2-40.5] (n=110) | -36.3 | 214 |
| Table | TLV | 66.3 [57.4-75.0] (n=104) | 31.8 [22.7-42.5] (n=110) | -34.5 | 214 |
| Table | V | 51.9 [42.4-61.0] (n=104) | 25.5 [18.1-34.1] (n=110) | -26.5 | 214 |
| **All sources** | **T** | **37.3 [31.1-43.3] (n=480)** | **25.1 [19.8-30.8] (n=358)** | **-12.2** | **838** |
| **All sources** | **TL** | **45.0 [39.0-50.6] (n=480)** | **31.3 [25.6-36.7] (n=358)** | **-13.7** | **838** |
| **All sources** | **TV** | **62.1 [56.6-67.6] (n=480)** | **38.5 [32.6-45.2] (n=358)** | **-23.5** | **838** |
| **All sources** | **TLV** | **63.5 [58.1-68.8] (n=480)** | **38.5 [32.6-44.7] (n=358)** | **-25.0** | **838** |
| **All sources** | **V** | **55.2 [49.8-60.8] (n=480)** | **33.5 [28.7-38.6] (n=358)** | **-21.7** | **838** |
| n (per col) | - | 2400 | 1790 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view._

| evidence pages | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| 1 | 37.1 [31.1-43.1] (n=480) | 44.6 [38.9-50.1] (n=480) | 63.7 [58.2-69.3] (n=480) | 55.0 [49.7-60.2] (n=480) | 1920 |
| 2 | 28.9 [22.5-35.2] (n=246) | 33.3 [27.4-39.7] (n=246) | 37.8 [30.7-44.5] (n=246) | 34.6 [27.9-41.2] (n=246) | 984 |
| 3 | 25.0 [10.2-41.5] (n=40) | 30.0 [15.4-46.2] (n=40) | 47.5 [30.8-63.4] (n=40) | 42.5 [24.3-57.8] (n=40) | 160 |
| 4-5 | 13.9 [2.7-27.8] (n=36) | 25.0 [11.8-38.5] (n=36) | 44.4 [26.5-60.5] (n=36) | 36.1 [20.0-51.4] (n=36) | 144 |
| 6+ | 13.9 [2.6-28.2] (n=36) | 19.4 [7.1-33.4] (n=36) | 22.2 [9.1-37.1] (n=36) | 13.9 [2.9-26.3] (n=36) | 144 |
| n (per col) | 838 | 838 | 838 | 838 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). Questions with zero evidence pages are excluded. The 4-5 and 6+ buckets are small (about 36 and 31 questions before OOM attrition, against 480 at one page), so read them for trend, not precision: check the per-cell n before quoting either. This is the finer-grained companion to the integration table, which keeps the collapsed single-versus-multi view. `1 → 6+` is the accuracy of the last bucket minus the first, in points; negative means the rung degrades as evidence spreads. Read it against the per-cell n: TLV OOMs hardest at high page counts, so its tail buckets are a handful of surviving questions and its slope is not comparable to the text rungs'._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 37.1 [31.1-43.1] (n=480) | 28.9 [22.5-35.2] (n=246) | 25.0 [10.2-41.5] (n=40) | 13.9 [2.7-27.8] (n=36) | 13.9 [2.6-28.2] (n=36) | -23.2 | 838 |
| TL | 44.6 [38.9-50.1] (n=480) | 33.3 [27.4-39.7] (n=246) | 30.0 [15.4-46.2] (n=40) | 25.0 [11.8-38.5] (n=36) | 19.4 [7.1-33.4] (n=36) | -25.1 | 838 |
| TLV | 63.7 [58.2-69.3] (n=480) | 37.8 [30.7-44.5] (n=246) | 47.5 [30.8-63.4] (n=40) | 44.4 [26.5-60.5] (n=36) | 22.2 [9.1-37.1] (n=36) | -41.5 | 838 |
| V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 42.5 [24.3-57.8] (n=40) | 36.1 [20.0-51.4] (n=36) | 13.9 [2.9-26.3] (n=36) | -41.1 | 838 |
| n (per col) | 1920 | 984 | 160 | 144 | 144 | - | - |

### Integration cross-tab: accuracy by doc_type, rung, and evidence-page bucket (oracle pages)

> **swept**: doc_type × rung × evidence-page bucket (1 / 2 / 3+) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail

_Buckets are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it); zero-evidence questions are dropped. 3+ merges the finer 3 / 4-5 / 6+ buckets of the integration-detail table. Every cell carries its own n: OOM attrition is rung-dependent at high page counts (worst on TLV), so a thin cell reads as survivorship, not robustness — check the n before quoting the cell. The bolded All rows pool every doc_type._

| doc_type | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 36.9 [22.5-50.6] (n=84) | 45.8 [29.5-61.7] (n=48) | 35.0 [11.8-58.8] (n=20) | 152 |
| Academic paper | TL | 32.1 [20.9-42.9] (n=84) | 43.8 [26.5-63.3] (n=48) | 30.0 [10.0-55.0] (n=20) | 152 |
| Academic paper | TLV | 38.1 [26.2-48.5] (n=84) | 37.5 [21.1-54.8] (n=48) | 50.0 [27.8-70.6] (n=20) | 152 |
| Academic paper | V | 29.8 [19.5-39.7] (n=84) | 33.3 [18.7-47.6] (n=48) | 35.0 [13.3-55.0] (n=20) | 152 |
| Administration/Industry file | T | 58.5 [38.3-80.6] (n=41) | 18.2 [0.0-45.5] (n=11) | 66.7 [25.0-100.0] (n=9) | 61 |
| Administration/Industry file | TL | 68.3 [57.4-81.1] (n=41) | 27.3 [0.0-60.0] (n=11) | 55.6 [20.0-88.9] (n=9) | 61 |
| Administration/Industry file | TLV | 85.4 [73.8-100.0] (n=41) | 45.5 [12.5-66.7] (n=11) | 55.6 [20.0-88.9] (n=9) | 61 |
| Administration/Industry file | V | 65.9 [56.5-77.1] (n=41) | 18.2 [0.0-28.6] (n=11) | 33.3 [9.1-66.7] (n=9) | 61 |
| Brochure | T | 22.4 [11.9-33.3] (n=49) | 47.1 [21.0-75.0] (n=17) | 18.2 [0.0-45.5] (n=11) | 77 |
| Brochure | TL | 30.6 [20.0-43.2] (n=49) | 35.3 [12.5-60.0] (n=17) | 36.4 [11.1-60.0] (n=11) | 77 |
| Brochure | TLV | 44.9 [30.2-60.8] (n=49) | 23.5 [0.0-47.1] (n=17) | 54.5 [22.2-81.8] (n=11) | 77 |
| Brochure | V | 44.9 [27.5-60.8] (n=49) | 47.1 [18.8-76.5] (n=17) | 45.5 [11.1-72.7] (n=11) | 77 |
| Financial report | T | 60.3 [46.3-72.9] (n=63) | 36.6 [25.6-46.7] (n=41) | 33.3 [0.0-100.0] (n=3) | 107 |
| Financial report | TL | 68.3 [54.9-76.5] (n=63) | 31.7 [19.6-48.6] (n=41) | 0.0 [0.0-0.0] (n=3) | 107 |
| Financial report | TLV | 76.2 [70.5-83.3] (n=63) | 26.8 [14.9-40.0] (n=41) | 0.0 [0.0-0.0] (n=3) | 107 |
| Financial report | V | 47.6 [33.9-62.3] (n=63) | 22.0 [13.1-33.3] (n=41) | 0.0 [0.0-0.0] (n=3) | 107 |
| Guidebook | T | 41.1 [26.0-58.3] (n=73) | 37.5 [17.8-57.9] (n=32) | 0.0 [0.0-0.0] (n=15) | 120 |
| Guidebook | TL | 45.2 [31.3-58.9] (n=73) | 34.4 [16.7-51.5] (n=32) | 6.7 [0.0-16.7] (n=15) | 120 |
| Guidebook | TLV | 58.9 [45.3-72.0] (n=73) | 43.8 [22.2-65.0] (n=32) | 33.3 [12.5-58.3] (n=15) | 120 |
| Guidebook | V | 54.8 [41.4-67.5] (n=73) | 37.5 [17.2-55.3] (n=32) | 33.3 [14.3-53.3] (n=15) | 120 |
| Research report / Introduction | T | 28.0 [17.3-39.8] (n=107) | 17.1 [9.1-26.7] (n=70) | 11.4 [0.0-25.0] (n=35) | 212 |
| Research report / Introduction | TL | 32.7 [21.9-43.1] (n=107) | 24.3 [14.3-35.3] (n=70) | 14.3 [3.1-27.3] (n=35) | 212 |
| Research report / Introduction | TLV | 67.3 [54.9-77.8] (n=107) | 34.3 [22.2-46.5] (n=70) | 17.1 [5.6-29.7] (n=35) | 212 |
| Research report / Introduction | V | 64.5 [53.2-73.8] (n=107) | 30.0 [17.2-42.5] (n=70) | 20.0 [5.4-36.1] (n=35) | 212 |
| Tutorial/Workshop | T | 22.2 [8.9-34.8] (n=63) | 0.0 [0.0-0.0] (n=27) | 0.0 [0.0-0.0] (n=19) | 109 |
| Tutorial/Workshop | TL | 52.4 [38.5-65.5] (n=63) | 40.7 [27.3-52.0] (n=27) | 36.8 [15.8-55.6] (n=19) | 109 |
| Tutorial/Workshop | TLV | 85.7 [76.9-93.9] (n=63) | 63.0 [43.5-79.2] (n=27) | 57.9 [33.3-78.9] (n=19) | 109 |
| Tutorial/Workshop | V | 81.0 [71.9-89.5] (n=63) | 63.0 [43.5-79.2] (n=27) | 42.1 [21.1-62.5] (n=19) | 109 |
| **All** | T | 37.1 [31.1-43.1] (n=480) | 28.9 [22.5-35.2] (n=246) | 17.9 [10.2-26.6] (n=112) | 838 |
| **All** | TL | 44.6 [38.9-50.1] (n=480) | 33.3 [27.4-39.7] (n=246) | 25.0 [17.0-33.3] (n=112) | 838 |
| **All** | TLV | 63.7 [58.2-69.3] (n=480) | 37.8 [30.7-44.5] (n=246) | 38.4 [28.4-46.9] (n=112) | 838 |
| **All** | V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 31.2 [22.2-40.0] (n=112) | 838 |
| n (per col) | - | 1920 | 984 | 448 | - |

### Integration cross-tab: accuracy by evidence source, rung, and evidence-page bucket (oracle pages)

> **swept**: evidence source × rung × evidence-page bucket (1 / 2 / 3+) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail · **multi-source questions**: counted once in every source they cite, so the blocks overlap; the All rows pool each question once and are not a column sum

_The evidence-source companion to the doc_type integration cross-tab: same buckets, same rungs, the modality a question draws on replacing the document class. Buckets are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it); zero-evidence questions are dropped. 3+ merges the finer 3 / 4-5 / 6+ buckets of the integration-detail table. A question can cite several sources (e.g. Chart + Table) and is counted in each one it cites, so the source blocks overlap and their n do not sum to the corpus. The bolded All rows pool every question exactly once and are therefore NOT a column sum of the blocks above them. Every cell carries its own n: OOM attrition is rung-dependent at high page counts (worst on TLV), so a thin cell reads as survivorship, not robustness — check the n before quoting the cell. Read the 3+ column for trend, not precision: crossed with five sources it falls to single digits in places._

| evidence_source | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 [42.9-85.7] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| (none) | TL | 78.6 [53.8-100.0] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| (none) | TLV | 85.7 [61.5-100.0] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| (none) | V | 57.1 [33.3-80.0] (n=14) | 0.0 [0.0-0.0] (n=4) | 100.0 [100.0-100.0] (n=1) | 19 |
| Chart | T | 20.4 [12.4-29.7] (n=98) | 18.6 [9.2-29.8] (n=59) | 5.0 [0.0-15.8] (n=20) | 177 |
| Chart | TL | 17.3 [10.0-25.3] (n=98) | 22.0 [11.3-35.2] (n=59) | 15.0 [0.0-31.6] (n=20) | 177 |
| Chart | TLV | 58.2 [44.8-69.2] (n=98) | 32.2 [20.3-45.2] (n=59) | 15.0 [0.0-31.6] (n=20) | 177 |
| Chart | V | 57.1 [44.9-68.1] (n=98) | 33.9 [21.0-48.3] (n=59) | 15.0 [0.0-31.6] (n=20) | 177 |
| Figure | T | 18.1 [12.0-25.1] (n=166) | 12.9 [5.6-22.1] (n=70) | 8.2 [0.0-18.4] (n=49) | 285 |
| Figure | TL | 24.7 [17.8-31.8] (n=166) | 20.0 [10.0-29.3] (n=70) | 18.4 [8.5-28.6] (n=49) | 285 |
| Figure | TLV | 49.4 [40.9-58.1] (n=166) | 34.3 [21.5-47.1] (n=70) | 44.9 [32.6-57.7] (n=49) | 285 |
| Figure | V | 45.2 [36.5-52.8] (n=166) | 37.1 [25.0-48.7] (n=70) | 30.6 [17.8-43.8] (n=49) | 285 |
| Generalized-text (Layout) | T | 33.9 [18.7-48.8] (n=56) | 32.4 [17.5-51.4] (n=34) | 11.5 [3.3-25.0] (n=26) | 116 |
| Generalized-text (Layout) | TL | 48.2 [35.4-62.1] (n=56) | 35.3 [20.5-51.4] (n=34) | 23.1 [8.0-40.0] (n=26) | 116 |
| Generalized-text (Layout) | TLV | 64.3 [51.9-76.9] (n=56) | 44.1 [26.5-60.5] (n=34) | 34.6 [16.0-53.6] (n=26) | 116 |
| Generalized-text (Layout) | V | 62.5 [48.9-75.5] (n=56) | 41.2 [27.3-55.3] (n=34) | 30.8 [12.5-51.6] (n=26) | 116 |
| Pure-text (Plain-text) | T | 46.8 [36.5-57.7] (n=154) | 35.1 [23.4-48.4] (n=94) | 25.0 [10.0-41.0] (n=40) | 288 |
| Pure-text (Plain-text) | TL | 55.8 [45.8-66.2] (n=154) | 41.5 [30.1-54.7] (n=94) | 32.5 [17.1-47.7] (n=40) | 288 |
| Pure-text (Plain-text) | TLV | 66.2 [56.0-76.7] (n=154) | 44.7 [32.7-57.8] (n=94) | 40.0 [25.6-53.9] (n=40) | 288 |
| Pure-text (Plain-text) | V | 55.8 [46.2-66.4] (n=154) | 30.9 [20.0-42.2] (n=94) | 35.0 [20.5-50.0] (n=40) | 288 |
| Table | T | 49.0 [38.6-58.5] (n=104) | 32.7 [24.4-41.5] (n=98) | 50.0 [25.0-75.0] (n=12) | 214 |
| Table | TL | 67.3 [57.9-75.8] (n=104) | 34.7 [25.8-45.8] (n=98) | 25.0 [8.3-50.0] (n=12) | 214 |
| Table | TLV | 69.2 [60.8-77.8] (n=104) | 31.6 [23.1-42.0] (n=98) | 41.7 [16.7-75.0] (n=12) | 214 |
| Table | V | 51.0 [41.7-59.6] (n=104) | 25.5 [17.2-36.3] (n=98) | 25.0 [8.3-50.0] (n=12) | 214 |
| **All** | T | 37.1 [31.1-43.1] (n=480) | 28.9 [22.5-35.2] (n=246) | 17.9 [10.2-26.6] (n=112) | 838 |
| **All** | TL | 44.6 [38.9-50.1] (n=480) | 33.3 [27.4-39.7] (n=246) | 25.0 [17.0-33.3] (n=112) | 838 |
| **All** | TLV | 63.7 [58.2-69.3] (n=480) | 37.8 [30.7-44.5] (n=246) | 38.4 [28.4-46.9] (n=112) | 838 |
| **All** | V | 55.0 [49.7-60.2] (n=480) | 34.6 [27.9-41.2] (n=246) | 31.2 [22.2-40.0] (n=112) | 838 |
| n (per col) | - | 1920 | 984 | 448 | - |

### Integration: accuracy by evidence hop for the TLV vs TLVi ordering pair

> **swept**: evidence hop (single vs multi) × page ordering (TLV vs TLVi) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse. Rows are the two orderings of the same run: TLV feeds all page text then all page images, TLVi interleaves each page's text with its own image. Same questions, same oracle pages, same reasoner, so the pair isolates ordering. The `M − S` column is the point of the table: interleaving is meant to help where evidence spans several pages, so the claim is about how the gap MOVES between the two rows, not about either row's pooled accuracy._

| ordering | single | multi | M − S | n |
| --- | --- | --- | --- | --- |
| TLV | 64.0 [58.7-69.3] | 38.5 [32.5-44.9] | -25.4 | 838 |
| TLVi | 65.4 [60.3-70.7] | 41.9 [36.3-47.8] | -23.5 | 838 |
| n (per col) | 960 | 716 | - | - |

## Faithfulness

### Faithfulness: answerable accuracy by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **anchor**: the none row reproduces the G1 headline ladder 31.9 / 39.4 / 56.8 / 45.9; drift is flagged in the note

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. The `none` row must reproduce the G1 headline ladder (31.9 / 39.4 / 56.8 / 45.9 for T / TL / TLV / V) within 1 point. FLAGGED ⚠: TLV 52.5 vs 56.8. This grid runs the full answerable pool while the ladder lost part of it to OOM on the 16 GB V100, and the recovered cells are the harder ones, so the gap is pool coverage rather than drift: on the cells both runs scored the two agree (see the oom_recovery table). Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 31.9 [27.3-36.5] (n=847) | 38.8 [34.5-43.0] (n=847) | 52.5 [48.5-56.5] (n=847) ⚠ | 45.6 [41.7-49.5] (n=847) |
| grounded | 26.8 [22.8-30.9] (n=847) | 34.4 [30.5-38.3] (n=847) | 45.7 [41.7-49.4] (n=847) | 39.9 [36.3-43.8] (n=847) |
| abstain | 23.3 [19.3-27.2] (n=847) | 29.3 [25.4-33.1] (n=847) | 41.4 [37.3-45.4] (n=847) | 33.5 [29.9-37.1] (n=847) |
| abstain_balanced | 23.8 [19.7-27.9] (n=847) | 30.0 [26.2-33.8] (n=847) | 42.6 [38.5-46.6] (n=847) | 35.2 [31.5-39.0] (n=847) |
| cot | 29.5 [25.2-33.7] (n=847) | 36.0 [32.5-39.6] (n=847) | 53.1 [49.4-56.9] (n=847) | 49.7 [45.5-53.8] (n=847) |
| extract_cot | 28.0 [23.6-32.3] (n=847) | 36.5 [32.9-40.2] (n=847) | 50.2 [46.4-54.1] (n=846) | 44.4 [40.4-48.5] (n=847) |
| n (per col) | 5082 | 5082 | 5081 | 5082 |

### Faithfulness: answerable false-abstention rate by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **direction**: abstaining is an ERROR here; lower is better

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. Every abstention counted here is an ERROR: the pages fed are the oracle evidence pages, so the answer was available. Lower is better, the opposite of the unanswerable table. Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 7.4 (n=847) | 3.3 (n=847) | 1.7 (n=847) | 1.1 (n=847) |
| grounded | 9.6 (n=847) | 1.3 (n=847) | 0.8 (n=847) | 0.6 (n=847) |
| abstain | 52.2 (n=847) | 47.1 (n=847) | 27.4 (n=847) | 32.5 (n=847) |
| abstain_balanced | 47.8 (n=847) | 42.9 (n=847) | 22.9 (n=847) | 27.7 (n=847) |
| cot | 2.8 (n=847) | 4.3 (n=847) | 1.1 (n=847) | 0.4 (n=847) |
| extract_cot | 2.5 (n=847) | 5.7 (n=847) | 2.1 (n=846) | 2.4 (n=847) |
| n (per col) | 5082 | 5082 | 5081 | 5082 |

### Faithfulness: unanswerable abstention rate by prompt mode and rung (bm25 k=3 pages)

> **swept**: prompt_mode × rung (unanswerable pool, bm25 k=3 pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **direction**: abstaining is CORRECT here; higher is better · **anchor**: grounded ≈ 10.7 and abstain ≈ 80.7 (legacy generic/targeted)

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. Pages are the bm25 k=3 similarity set, not oracle: an unanswerable question has no gold pages to select, so the two pools differ in page selection by design and the claim is about the instruction, not the retriever. Abstaining is CORRECT here, so higher is better. `grounded` and `abstain` are byte-identical instructions to the legacy generic/targeted and must reproduce their rates within 3 points, checked on the n-weighted pool across rungs the way reconcile.py reads them: grounded 10.6 vs 10.7 (ok); abstain 79.3 vs 80.7 (ok). Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 13.1 (n=244) | 13.1 (n=244) | 14.3 (n=244) | 13.5 (n=244) |
| grounded | 22.1 (n=244) | 6.6 (n=244) | 8.2 (n=244) | 5.3 (n=244) |
| abstain | 81.1 (n=244) | 79.9 (n=244) | 74.6 (n=244) | 81.6 (n=244) |
| abstain_balanced | 75.4 (n=244) | 77.0 (n=244) | 68.9 (n=244) | 76.6 (n=244) |
| cot | 8.6 (n=244) | 13.9 (n=244) | 11.9 (n=244) | 5.7 (n=244) |
| extract_cot | 8.6 (n=244) | 18.0 (n=244) | 18.4 (n=244) | 18.4 (n=244) |
| n (per col) | 1464 | 1464 | 1464 | 1464 |

### Faithfulness: answerable accuracy by prompt mode, evidence source and rung (oracle pages)

> **swept**: prompt_mode × evidence source × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. A regroup of the pooled grid, not new inference: `evidence_sources` is a per-row covariate on every judged row, so this is the same cells re-aggregated. A question citing several evidence sources is counted under EACH of them, so the per-source rows overlap and CANNOT be summed; the bolded All sources row closing each prompt mode is computed fresh over every row, each counted once, and reproduces the pooled table. † marks a cell computed on fewer than 30 rows, where a single question moves it by more than three points: read the direction, not the value. Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Chart | 18.5 [12.3-24.6] (n=178) | 19.1 [13.1-25.5] (n=178) | 45.5 [37.3-54.3] (n=178) | 43.3 [34.4-52.4] (n=178) |
| none | Figure | 15.5 [11.1-20.5] (n=290) | 23.8 [17.8-30.5] (n=290) | 44.8 [38.0-51.7] (n=290) | 40.3 [34.2-46.4] (n=290) |
| none | Generalized-text (Layout) | 28.0 [18.1-37.6] (n=118) | 37.3 [27.3-47.4] (n=118) | 50.8 [42.3-59.2] (n=118) | 44.1 [35.7-52.8] (n=118) |
| none | Pure-text (Plain-text) | 39.2 [31.5-47.6] (n=291) | 47.8 [41.1-55.3] (n=291) | 55.3 [48.8-62.8] (n=291) | 44.3 [37.7-51.3] (n=291) |
| none | Table | 40.6 [33.8-46.4] (n=217) | 48.4 [40.3-55.2] (n=217) | 48.4 [41.4-55.4] (n=217) | 37.8 [31.0-44.3] (n=217) |
| none | (none) | 52.6 [31.2-73.7] (n=19)† | 63.2 [38.9-83.3] (n=19)† | 73.7 [52.6-91.3] (n=19)† | 52.6 [29.4-70.8] (n=19)† |
| none | **All sources** | 31.9 [27.3-36.5] (n=847) | 38.8 [34.5-43.0] (n=847) | 52.5 [48.5-56.5] (n=847) | 45.6 [41.7-49.5] (n=847) |
| grounded | Chart | 16.3 [10.1-22.7] (n=178) | 16.3 [11.1-22.5] (n=178) | 33.7 [26.8-41.0] (n=178) | 31.5 [24.6-38.8] (n=178) |
| grounded | Figure | 12.1 [8.0-17.2] (n=290) | 22.4 [16.8-28.1] (n=290) | 42.4 [35.9-48.9] (n=290) | 39.3 [33.0-45.4] (n=290) |
| grounded | Generalized-text (Layout) | 18.6 [10.8-27.4] (n=118) | 29.7 [20.7-38.3] (n=118) | 42.4 [32.8-52.2] (n=118) | 44.9 [34.7-55.2] (n=118) |
| grounded | Pure-text (Plain-text) | 37.8 [30.7-45.7] (n=291) | 45.0 [38.4-52.0] (n=291) | 51.2 [43.8-58.5] (n=291) | 41.6 [35.6-48.7] (n=291) |
| grounded | Table | 29.5 [23.3-35.5] (n=217) | 39.2 [31.9-46.2] (n=217) | 40.1 [33.3-47.3] (n=217) | 30.9 [24.5-36.6] (n=217) |
| grounded | (none) | 42.1 [22.2-66.7] (n=19)† | 57.9 [33.3-81.8] (n=19)† | 52.6 [29.4-75.0] (n=19)† | 42.1 [19.0-62.5] (n=19)† |
| grounded | **All sources** | 26.8 [22.8-30.9] (n=847) | 34.4 [30.5-38.3] (n=847) | 45.7 [41.7-49.4] (n=847) | 39.9 [36.3-43.8] (n=847) |
| abstain | Chart | 13.5 [7.5-19.7] (n=178) | 12.4 [7.0-18.3] (n=178) | 28.7 [22.8-35.4] (n=178) | 26.4 [19.9-32.4] (n=178) |
| abstain | Figure | 7.2 [4.1-10.9] (n=290) | 14.1 [10.0-18.2] (n=290) | 34.5 [27.9-40.9] (n=290) | 31.0 [24.8-36.7] (n=290) |
| abstain | Generalized-text (Layout) | 19.5 [11.3-28.2] (n=118) | 25.4 [17.4-33.3] (n=118) | 41.5 [32.1-50.9] (n=118) | 37.3 [28.0-47.0] (n=118) |
| abstain | Pure-text (Plain-text) | 34.0 [27.4-41.7] (n=291) | 40.5 [34.8-47.2] (n=291) | 45.7 [39.1-53.1] (n=291) | 36.1 [29.6-43.7] (n=291) |
| abstain | Table | 26.3 [20.4-32.5] (n=217) | 38.2 [31.2-45.5] (n=217) | 39.2 [32.2-46.2] (n=217) | 26.7 [20.7-32.8] (n=217) |
| abstain | (none) | 36.8 [17.6-62.5] (n=19)† | 52.6 [25.0-77.3] (n=19)† | 57.9 [30.0-81.8] (n=19)† | 42.1 [19.0-62.5] (n=19)† |
| abstain | **All sources** | 23.3 [19.3-27.2] (n=847) | 29.3 [25.4-33.1] (n=847) | 41.4 [37.3-45.4] (n=847) | 33.5 [29.9-37.1] (n=847) |
| abstain_balanced | Chart | 14.0 [8.4-20.2] (n=178) | 12.9 [7.4-18.6] (n=178) | 30.9 [24.5-38.2] (n=178) | 25.8 [19.7-32.1] (n=178) |
| abstain_balanced | Figure | 7.9 [4.5-12.3] (n=290) | 14.5 [10.1-18.9] (n=290) | 36.2 [29.7-42.3] (n=290) | 33.4 [27.0-39.6] (n=290) |
| abstain_balanced | Generalized-text (Layout) | 19.5 [11.3-28.2] (n=118) | 28.8 [19.7-37.7] (n=118) | 41.5 [32.8-50.9] (n=118) | 39.0 [29.4-49.0] (n=118) |
| abstain_balanced | Pure-text (Plain-text) | 33.7 [27.0-41.5] (n=291) | 39.5 [33.6-46.5] (n=291) | 47.4 [40.6-54.7] (n=291) | 36.4 [30.3-43.8] (n=291) |
| abstain_balanced | Table | 26.3 [20.4-32.5] (n=217) | 37.8 [30.8-44.2] (n=217) | 37.3 [30.5-44.3] (n=217) | 30.0 [23.7-36.2] (n=217) |
| abstain_balanced | (none) | 42.1 [22.2-66.7] (n=19)† | 57.9 [33.3-81.8] (n=19)† | 63.2 [37.5-87.5] (n=19)† | 42.1 [19.0-62.5] (n=19)† |
| abstain_balanced | **All sources** | 23.8 [19.7-27.9] (n=847) | 30.0 [26.2-33.8] (n=847) | 42.6 [38.5-46.6] (n=847) | 35.2 [31.5-39.0] (n=847) |
| cot | Chart | 21.3 [14.8-27.6] (n=178) | 16.9 [11.4-22.9] (n=178) | 45.5 [37.7-53.9] (n=178) | 44.4 [35.9-52.7] (n=178) |
| cot | Figure | 11.7 [7.7-16.3] (n=290) | 18.3 [13.8-23.3] (n=290) | 45.2 [38.1-51.6] (n=290) | 44.8 [38.5-51.1] (n=290) |
| cot | Generalized-text (Layout) | 24.6 [16.0-33.8] (n=118) | 37.3 [27.2-47.1] (n=118) | 50.0 [39.7-60.4] (n=118) | 55.9 [46.2-65.1] (n=118) |
| cot | Pure-text (Plain-text) | 34.7 [28.3-42.0] (n=291) | 45.0 [38.5-52.7] (n=291) | 54.6 [48.1-61.8] (n=291) | 48.1 [41.4-54.7] (n=291) |
| cot | Table | 40.6 [33.5-47.2] (n=217) | 51.2 [44.6-57.7] (n=217) | 55.3 [48.6-61.8] (n=217) | 47.5 [40.1-55.1] (n=217) |
| cot | (none) | 42.1 [21.1-62.5] (n=19)† | 57.9 [35.3-81.2] (n=19)† | 63.2 [41.2-85.0] (n=19)† | 52.6 [30.0-75.0] (n=19)† |
| cot | **All sources** | 29.5 [25.2-33.7] (n=847) | 36.0 [32.5-39.6] (n=847) | 53.1 [49.4-56.9] (n=847) | 49.7 [45.5-53.8] (n=847) |
| extract_cot | Chart | 13.5 [8.3-19.1] (n=178) | 17.4 [11.4-23.9] (n=178) | 39.3 [31.2-48.7] (n=178) | 38.8 [30.1-48.3] (n=178) |
| extract_cot | Figure | 10.7 [7.0-15.3] (n=290) | 21.0 [16.2-26.0] (n=290) | 44.1 [37.4-49.8] (n=290) | 41.7 [35.3-47.5] (n=290) |
| extract_cot | Generalized-text (Layout) | 20.3 [12.6-29.3] (n=118) | 37.3 [27.8-47.4] (n=118) | 50.8 [41.7-59.7] (n=118) | 52.5 [44.1-61.1] (n=118) |
| extract_cot | Pure-text (Plain-text) | 37.5 [30.4-45.2] (n=291) | 45.0 [38.6-52.1] (n=291) | 51.7 [45.2-58.6] (n=290) | 44.3 [37.8-52.1] (n=291) |
| extract_cot | Table | 41.5 [34.0-48.5] (n=217) | 49.8 [43.6-55.6] (n=217) | 52.5 [46.9-58.8] (n=217) | 39.6 [33.0-47.3] (n=217) |
| extract_cot | (none) | 31.6 [12.5-50.0] (n=19)† | 52.6 [26.3-75.0] (n=19)† | 57.9 [31.6-83.3] (n=19)† | 42.1 [19.0-62.5] (n=19)† |
| extract_cot | **All sources** | 28.0 [23.6-32.3] (n=847) | 36.5 [32.9-40.2] (n=847) | 50.2 [46.4-54.1] (n=846) | 44.4 [40.4-48.5] (n=847) |
| n (per col) | - | - | - | - | - |

### Faithfulness: answerable false-abstention rate by prompt mode, evidence source and rung

> **swept**: prompt_mode × evidence source × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **direction**: abstaining is an ERROR here; lower is better · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. Every abstention counted here is an ERROR: the pages fed are the oracle evidence pages, so the answer was available. Lower is better. A regroup of the pooled grid, not new inference: `evidence_sources` is a per-row covariate on every judged row, so this is the same cells re-aggregated. A question citing several evidence sources is counted under EACH of them, so the per-source rows overlap and CANNOT be summed; the bolded All sources row closing each prompt mode is computed fresh over every row, each counted once, and reproduces the pooled table. † marks a cell computed on fewer than 30 rows, where a single question moves it by more than three points: read the direction, not the value. Per-cell n is inline because OOM attrition is rung-dependent and thins the TLV/V cells; a small n there reads as survivorship, not signal. Rows carrying no gold evidence pages are kept in the answerable pool exactly as the other tables treat hop=none, i.e. not split out, since these tables do not condition on hop._

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Chart | 12.9 (n=178) | 8.4 (n=178) | 2.8 (n=178) | 1.1 (n=178) |
| none | Figure | 10.7 (n=290) | 2.8 (n=290) | 2.8 (n=290) | 1.4 (n=290) |
| none | Generalized-text (Layout) | 2.5 (n=118) | 4.2 (n=118) | 0.0 (n=118) | 0.8 (n=118) |
| none | Pure-text (Plain-text) | 4.5 (n=291) | 1.7 (n=291) | 1.7 (n=291) | 0.3 (n=291) |
| none | Table | 6.0 (n=217) | 1.4 (n=217) | 2.3 (n=217) | 1.8 (n=217) |
| none | (none) | 5.3 (n=19)† | 5.3 (n=19)† | 0.0 (n=19)† | 5.3 (n=19)† |
| none | **All sources** | 7.4 (n=847) | 3.3 (n=847) | 1.7 (n=847) | 1.1 (n=847) |
| grounded | Chart | 16.9 (n=178) | 2.8 (n=178) | 1.1 (n=178) | 0.6 (n=178) |
| grounded | Figure | 10.3 (n=290) | 0.3 (n=290) | 0.7 (n=290) | 1.0 (n=290) |
| grounded | Generalized-text (Layout) | 7.6 (n=118) | 0.8 (n=118) | 0.0 (n=118) | 0.0 (n=118) |
| grounded | Pure-text (Plain-text) | 6.5 (n=291) | 0.7 (n=291) | 1.0 (n=291) | 0.7 (n=291) |
| grounded | Table | 10.1 (n=217) | 1.4 (n=217) | 0.9 (n=217) | 0.0 (n=217) |
| grounded | (none) | 0.0 (n=19)† | 0.0 (n=19)† | 0.0 (n=19)† | 0.0 (n=19)† |
| grounded | **All sources** | 9.6 (n=847) | 1.3 (n=847) | 0.8 (n=847) | 0.6 (n=847) |
| abstain | Chart | 52.2 (n=178) | 59.0 (n=178) | 25.3 (n=178) | 27.5 (n=178) |
| abstain | Figure | 76.2 (n=290) | 65.2 (n=290) | 35.2 (n=290) | 38.3 (n=290) |
| abstain | Generalized-text (Layout) | 55.9 (n=118) | 44.1 (n=118) | 19.5 (n=118) | 25.4 (n=118) |
| abstain | Pure-text (Plain-text) | 41.9 (n=291) | 35.4 (n=291) | 23.7 (n=291) | 30.9 (n=291) |
| abstain | Table | 42.4 (n=217) | 36.4 (n=217) | 30.0 (n=217) | 39.6 (n=217) |
| abstain | (none) | 36.8 (n=19)† | 31.6 (n=19)† | 26.3 (n=19)† | 36.8 (n=19)† |
| abstain | **All sources** | 52.2 (n=847) | 47.1 (n=847) | 27.4 (n=847) | 32.5 (n=847) |
| abstain_balanced | Chart | 44.9 (n=178) | 51.7 (n=178) | 18.5 (n=178) | 24.2 (n=178) |
| abstain_balanced | Figure | 71.7 (n=290) | 62.1 (n=290) | 31.0 (n=290) | 33.1 (n=290) |
| abstain_balanced | Generalized-text (Layout) | 52.5 (n=118) | 41.5 (n=118) | 18.6 (n=118) | 21.2 (n=118) |
| abstain_balanced | Pure-text (Plain-text) | 39.5 (n=291) | 32.6 (n=291) | 18.9 (n=291) | 25.4 (n=291) |
| abstain_balanced | Table | 37.8 (n=217) | 30.0 (n=217) | 25.3 (n=217) | 34.6 (n=217) |
| abstain_balanced | (none) | 26.3 (n=19)† | 31.6 (n=19)† | 21.1 (n=19)† | 31.6 (n=19)† |
| abstain_balanced | **All sources** | 47.8 (n=847) | 42.9 (n=847) | 22.9 (n=847) | 27.7 (n=847) |
| cot | Chart | 3.9 (n=178) | 13.5 (n=178) | 1.1 (n=178) | 1.1 (n=178) |
| cot | Figure | 1.7 (n=290) | 2.4 (n=290) | 0.3 (n=290) | 0.0 (n=290) |
| cot | Generalized-text (Layout) | 0.0 (n=118) | 3.4 (n=118) | 0.8 (n=118) | 0.0 (n=118) |
| cot | Pure-text (Plain-text) | 4.1 (n=291) | 3.1 (n=291) | 1.0 (n=291) | 0.7 (n=291) |
| cot | Table | 3.2 (n=217) | 2.8 (n=217) | 2.3 (n=217) | 0.0 (n=217) |
| cot | (none) | 10.5 (n=19)† | 5.3 (n=19)† | 5.3 (n=19)† | 0.0 (n=19)† |
| cot | **All sources** | 2.8 (n=847) | 4.3 (n=847) | 1.1 (n=847) | 0.4 (n=847) |
| extract_cot | Chart | 5.6 (n=178) | 14.0 (n=178) | 2.2 (n=178) | 2.2 (n=178) |
| extract_cot | Figure | 2.1 (n=290) | 4.1 (n=290) | 1.0 (n=290) | 1.4 (n=290) |
| extract_cot | Generalized-text (Layout) | 1.7 (n=118) | 3.4 (n=118) | 0.8 (n=118) | 1.7 (n=118) |
| extract_cot | Pure-text (Plain-text) | 1.4 (n=291) | 3.4 (n=291) | 2.4 (n=290) | 3.1 (n=291) |
| extract_cot | Table | 1.8 (n=217) | 4.1 (n=217) | 4.6 (n=217) | 5.1 (n=217) |
| extract_cot | (none) | 5.3 (n=19)† | 5.3 (n=19)† | 10.5 (n=19)† | 5.3 (n=19)† |
| extract_cot | **All sources** | 2.5 (n=847) | 5.7 (n=847) | 2.1 (n=846) | 2.4 (n=847) |
| n (per col) | - | - | - | - | - |

### Faithfulness: unanswerable abstention rate by prompt mode, evidence source and rung

> **swept**: prompt_mode × evidence source × rung (unanswerable pool, bm25 k=3 pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **⚠ not usable per source**: an unanswerable question has no gold evidence pages, so the pool is essentially unlabelled; see the note · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". Abstention is detected on the EXTRACTED final answer (the text after the last "Answer:"), not the whole generation: cot/extract_cot emit reasoning that would otherwise be read as an answer. An extraction that comes back empty is a non-answer, scored incorrect and not an abstention. ⚠ THIS CUT IS NOT USABLE PER SOURCE. An unanswerable question carries no gold evidence pages, so there is nothing to derive an evidence source from and the pool is essentially unlabelled: 235 of 244 questions fall in (none), and the labelled remainder is Figure: 3, Generalized-text (Layout): 1, Pure-text (Plain-text): 7, Table: 1. Chart is absent entirely. The rows are emitted so the gap is visible rather than silently missing; quote the pooled unanswerable table instead. A regroup of the pooled grid, not new inference: `evidence_sources` is a per-row covariate on every judged row, so this is the same cells re-aggregated. A question citing several evidence sources is counted under EACH of them, so the per-source rows overlap and CANNOT be summed; the bolded All sources row closing each prompt mode is computed fresh over every row, each counted once, and reproduces the pooled table. † marks a cell computed on fewer than 30 rows, where a single question moves it by more than three points: read the direction, not the value. _

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Figure | 0.0 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† |
| none | Generalized-text (Layout) | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| none | Pure-text (Plain-text) | 14.3 (n=7)† | 14.3 (n=7)† | 0.0 (n=7)† | 0.0 (n=7)† |
| none | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| none | (none) | 13.2 (n=235) | 13.2 (n=235) | 14.9 (n=235) | 14.0 (n=235) |
| none | **All sources** | 13.1 (n=244) | 13.1 (n=244) | 14.3 (n=244) | 13.5 (n=244) |
| grounded | Figure | 33.3 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† |
| grounded | Generalized-text (Layout) | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| grounded | Pure-text (Plain-text) | 0.0 (n=7)† | 0.0 (n=7)† | 14.3 (n=7)† | 0.0 (n=7)† |
| grounded | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| grounded | (none) | 22.6 (n=235) | 6.8 (n=235) | 8.1 (n=235) | 5.5 (n=235) |
| grounded | **All sources** | 22.1 (n=244) | 6.6 (n=244) | 8.2 (n=244) | 5.3 (n=244) |
| abstain | Figure | 100.0 (n=3)† | 100.0 (n=3)† | 100.0 (n=3)† | 100.0 (n=3)† |
| abstain | Generalized-text (Layout) | 100.0 (n=1)† | 100.0 (n=1)† | 100.0 (n=1)† | 100.0 (n=1)† |
| abstain | Pure-text (Plain-text) | 85.7 (n=7)† | 85.7 (n=7)† | 85.7 (n=7)† | 85.7 (n=7)† |
| abstain | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| abstain | (none) | 80.9 (n=235) | 79.6 (n=235) | 74.0 (n=235) | 81.3 (n=235) |
| abstain | **All sources** | 81.1 (n=244) | 79.9 (n=244) | 74.6 (n=244) | 81.6 (n=244) |
| abstain_balanced | Figure | 100.0 (n=3)† | 100.0 (n=3)† | 66.7 (n=3)† | 66.7 (n=3)† |
| abstain_balanced | Generalized-text (Layout) | 100.0 (n=1)† | 100.0 (n=1)† | 100.0 (n=1)† | 100.0 (n=1)† |
| abstain_balanced | Pure-text (Plain-text) | 85.7 (n=7)† | 85.7 (n=7)† | 85.7 (n=7)† | 85.7 (n=7)† |
| abstain_balanced | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| abstain_balanced | (none) | 74.9 (n=235) | 76.6 (n=235) | 68.5 (n=235) | 76.6 (n=235) |
| abstain_balanced | **All sources** | 75.4 (n=244) | 77.0 (n=244) | 68.9 (n=244) | 76.6 (n=244) |
| cot | Figure | 0.0 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† | 0.0 (n=3)† |
| cot | Generalized-text (Layout) | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| cot | Pure-text (Plain-text) | 0.0 (n=7)† | 0.0 (n=7)† | 14.3 (n=7)† | 0.0 (n=7)† |
| cot | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| cot | (none) | 8.9 (n=235) | 14.5 (n=235) | 11.9 (n=235) | 6.0 (n=235) |
| cot | **All sources** | 8.6 (n=244) | 13.9 (n=244) | 11.9 (n=244) | 5.7 (n=244) |
| extract_cot | Figure | 0.0 (n=3)† | 0.0 (n=3)† | 66.7 (n=3)† | 0.0 (n=3)† |
| extract_cot | Generalized-text (Layout) | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| extract_cot | Pure-text (Plain-text) | 0.0 (n=7)† | 14.3 (n=7)† | 28.6 (n=7)† | 0.0 (n=7)† |
| extract_cot | Table | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† | 0.0 (n=1)† |
| extract_cot | (none) | 8.9 (n=235) | 18.3 (n=235) | 17.9 (n=235) | 19.1 (n=235) |
| extract_cot | **All sources** | 8.6 (n=244) | 18.0 (n=244) | 18.4 (n=244) | 18.4 (n=244) |
| n (per col) | - | - | - | - | - |

### Faithfulness: paired verdict transitions from the uninstructed prompt to the abstention prompts

> **swept**: prompt_mode transition (none→abstain, none→abstain_balanced) × rung (answerable pool, oracle pages) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **pairing**: within-question at one rung, both modes status==ok; only the instruction changes, pages are the oracle set on both sides · **R→W split**: `as refusal` vs `as wrong answer` sum to R→W, so the table separates what the instruction refuses from what it merely gets wrong · **net column**: W→R − R→W in points, i.e. the mode's accuracy change against the uninstructed prompt

_Paired on question_id at one rung: a question counts only when BOTH prompt modes produced a status==ok row there, so every rate is a within-question flip and not two marginal accuracies read against each other. Pages are the oracle evidence pages under both modes and only the instruction changes. R→W is the share of paired questions the instruction breaks and W→R the share it repairs, both as PERCENTAGES of the row's paired n, so their difference is the mode's accuracy change in points (the `net` column) and reproduces the two modes' rows in the faithfulness accuracy grid. R→W splits by what replaced the correct answer: `as refusal` is a flip whose new row is an abstention, `as wrong answer` a flip that still answered and answered wrongly. The two sum to R→W. `abstentions` is every abstention under the target mode, as a percentage of the paired n, and reproduces that mode's row in the false-abstention grid. `of which previously correct` is the share OF THOSE ABSTENTIONS (not of the paired n) that refused a question the uninstructed prompt answered correctly, so it says how well the refusal is aimed: the rest of them refused questions that were already wrong and cost no accuracy._

| transition | rung | right→wrong (%) | …as refusal (%) | …as wrong answer (%) | wrong→right (%) | net (pts) | abstentions (%) | of which previously correct (% of abstentions) | paired n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| none->abstain | T | 9.9 (84) | 4.5 (38) | 5.4 (46) | 1.3 (11) | -8.6 | 52.2 (442) | 8.6 (38) | 847 |
| none->abstain | TL | 11.1 (94) | 6.3 (53) | 4.8 (41) | 1.5 (13) | -9.6 | 47.1 (399) | 13.3 (53) | 847 |
| none->abstain | TLV | 12.9 (109) | 4.8 (41) | 8.0 (68) | 1.8 (15) | -11.1 | 27.4 (232) | 17.7 (41) | 847 |
| none->abstain | V | 14.6 (124) | 6.3 (53) | 8.4 (71) | 2.6 (22) | -12.0 | 32.5 (275) | 19.3 (53) | 847 |
| none->abstain_balanced | T | 9.4 (80) | 3.9 (33) | 5.5 (47) | 1.4 (12) | -8.0 | 47.8 (405) | 8.1 (33) | 847 |
| none->abstain_balanced | TL | 10.6 (90) | 4.8 (41) | 5.8 (49) | 1.8 (15) | -8.9 | 42.9 (363) | 11.3 (41) | 847 |
| none->abstain_balanced | TLV | 11.8 (100) | 3.5 (30) | 8.3 (70) | 1.9 (16) | -9.9 | 22.9 (194) | 15.5 (30) | 847 |
| none->abstain_balanced | V | 13.8 (117) | 4.5 (38) | 9.3 (79) | 3.4 (29) | -10.4 | 27.7 (235) | 16.2 (38) | 847 |
| n (per col) | - | - | - | - | - | - | - | - | - |

### Hallucination: abstention rate on unanswerable questions by prompt

> **swept**: prompt_mode (none / generic / targeted; legacy names of the six-mode set) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

| prompt_condition | abstention_rate | answered | n |
| --- | --- | --- | --- |
| none | 17.1 | 809 | 976 |
| generic | 10.3 | 875 | 976 |
| targeted | 79.4 | 201 | 976 |
| n (per col) | - | - | - |

### Mined: abstention rate on unanswerable questions by prompt mode and doc_type

> **swept**: prompt_mode × doc_type · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV · **pool**: unanswerable · **page_selection**: similarity (bm25, k=3) · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

| doc_type | none | generic | targeted | n_none | n_generic | n_targeted |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 10.0 | 5.0 | 70.0 | 200 | 200 | 200 |
| Administration/Industry file | 16.2 | 14.7 | 72.1 | 68 | 68 | 68 |
| Brochure | 13.5 | 9.4 | 65.6 | 96 | 96 | 96 |
| Financial report | 13.9 | 8.3 | 69.4 | 36 | 36 | 36 |
| Guidebook | 17.4 | 6.9 | 88.2 | 144 | 144 | 144 |
| Research report / Introduction | 21.9 | 11.1 | 82.4 | 324 | 324 | 324 |
| Tutorial/Workshop | 20.4 | 21.3 | 96.3 | 108 | 108 | 108 |
| n (per col) | 976 | 976 | 976 | - | - | - |

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

## Deployment

### Reasoner: precision / scale / matched budget / family / reasoning variant

> **swept**: reasoner block (precision / scale / matched budget / family / reasoning variant) · **dataset**: mmlongbench · **scan**: mixed pools by run; compare within a block · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **memory**: weight footprint, not peak VRAM · **note**: thinking/llama rows appear when their runs land

_Weight footprint (MB, `~` = derived for quantized variants) replaces peak VRAM: the measured figure is device-0 only. Every accuracy cell carries its own n because OOM attrition is not random with respect to the question pool: it tracks document length and page count, which track the multi-page questions, so a thin cell compares an easier surviving subset. The reasoning-variant block reports M−S per rung (multi minus single accuracy, negative = multi worse), NOT pooled accuracy: the Thinking variant's value is entirely its hop-split behaviour. Blocks share the 8B bf16 baseline row wherever it is the comparison point; pool composition differs by run (scan filters), so compare within a block._

| block | model_spec | weights_mb | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| precision | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.7] (n=847) | 38.4 [34.4-42.5] (n=847) | 52.4 [48.3-56.4] (n=847) | 45.5 [41.6-49.6] (n=847) | 3388 |
| precision | qwen3vl-8b-local-8bit | 10285~ | 32.5 [27.6-37.2] (n=847) | 37.9 [33.7-42.1] (n=847) | 53.6 [49.4-57.7] (n=847) | 45.7 [41.5-50.1] (n=847) | 3388 |
| precision | qwen3vl-8b-local-4bit | 6775~ | 31.8 [27.1-36.4] (n=847) | 39.4 [35.4-43.2] (n=847) | 51.8 [47.7-55.9] (n=847) | 45.5 [41.1-49.8] (n=847) | 3388 |
| scale | qwen3vl-2b-local | 4255 | 24.7 [20.9-28.4] (n=847) | 31.9 [28.5-35.2] (n=847) | 38.3 [34.7-41.7] (n=847) | 31.9 [28.3-35.6] (n=847) | 3388 |
| scale | qwen3vl-4b-local | 8876 | 32.3 [27.5-37.1] (n=847) | 38.6 [34.4-42.7] (n=847) | 50.4 [46.6-54.1] (n=847) | 42.4 [38.2-46.9] (n=847) | 3388 |
| scale | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.7] (n=847) | 38.4 [34.4-42.5] (n=847) | 52.4 [48.3-56.4] (n=847) | 45.5 [41.6-49.6] (n=847) | 3388 |
| scale | qwen3vl-32b-local | 66715 | 35.5 [30.4-40.6] (n=847) | 43.9 [39.9-48.1] (n=847) | 59.6 [55.2-63.9] (n=846) | 56.7 [52.5-60.9] (n=847) | 3387 |
| matched budget (~17 GB) | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.7] (n=847) | 38.4 [34.4-42.5] (n=847) | 52.4 [48.3-56.4] (n=847) | 45.5 [41.6-49.6] (n=847) | 3388 |
| matched budget (~17 GB) | qwen3vl-32b-local-4bit | 19951~ | 37.0 [32.0-41.4] (n=847) | 42.1 [37.9-46.2] (n=847) | 59.1 [54.7-63.2] (n=847) | 52.3 [47.9-57.0] (n=847) | 3388 |
| family | qwen3vl-8b-local | 17534 | 31.9 [27.1-36.7] (n=847) | 38.4 [34.4-42.5] (n=847) | 52.4 [48.3-56.4] (n=847) | 45.5 [41.6-49.6] (n=847) | 3388 |
| family | internvl3-8b-local | 15889 | 19.3 [15.9-22.8] (n=845) | 25.3 [22.0-28.7] (n=842) | 32.6 [28.6-36.9] (n=807) | 24.1 [20.2-28.4] (n=845) | 3339 |
| reasoning variant (M−S) | qwen3vl-8b-local | 17534 | -11.7 (nS=480, nM=358) | -13.9 (nS=480, nM=358) | -25.8 (nS=480, nM=358) | -21.5 (nS=480, nM=358) | 3388 |
| reasoning variant (M−S) | qwen3vl-8b-thinking-local | - | -2.1 (nS=377, nM=302) | -3.3 (nS=377, nM=302) | -8.0 (nS=377, nM=301) | -10.8 (nS=377, nM=299) | 2740 |
| n (per col) | - | - | 7460 | 7457 | 7420 | 7457 | - |

### Reasoner scale vs evidence hop: accuracy by gold evidence-page bucket, per rung

> **swept**: reasoner size × gold evidence-page bucket × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: as the integration table (unresolved-evidence questions excluded); the 8B row reproduces it · **page_selection**: oracle · **prompt_mode**: none · **multi**: cumulative: two or more gold pages, pooling the 2 and 3+ columns · **reading**: does scale close the M−S deficit, or lift both hop buckets together · **note**: each size loads its own run_tags in the builder

_Accuracy on oracle pages, bucketed by the number of gold evidence pages the question cites (from the corpus annotation, not from `page_indices`). The 1/2/3/4+ columns are disjoint; `3+` pools 3 and 4+, and `multi` is CUMULATIVE over 2, 3 and 4+. Both are derived from the fine buckets, so a row here can be lifted straight into the integration table, which splits 3 from 4+. `M − S` is multi minus the single-page column, in points, so a negative value means multi-page evidence is worse and a value that does not move with size means scale lifted both hops together rather than closing the gap. Pool: the answerable questions carrying gold pages, less the twelve whose gold pages never reach the model, matching the integration table exactly — the 8B row reproduces it cell for cell. Each size reads its own run (2B/4B from the size sweep, 8B from the representation baseline, 32B from the matched-budget run) over the same 847-question corpus, so the sizes are comparable; the 32B is missing one TLV cell, which is why its TLV n can sit one below the others._

| model | rung | 1 | 2 | 3 | 4+ | 3+ | multi | M − S | multi Δ vs 8B | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2B | T | 31.4 | 20.7 | 10.0 | 7.0 | 8.1 | 16.8 | -14.7 | -9.1 | 826 |
| 2B | TL | 38.2 | 25.7 | 27.5 | 21.1 | 23.4 | 25.0 | -13.2 | -6.2 | 826 |
| 2B | TLV | 48.1 | 27.4 | 37.5 | 18.3 | 25.2 | 26.7 | -21.4 | -11.9 | 826 |
| 2B | V | 40.7 | 20.7 | 30.0 | 18.3 | 22.5 | 21.3 | -19.4 | -12.8 | 826 |
| 4B | T | 40.1 | 26.1 | 27.5 | 12.7 | 18.0 | 23.6 | -16.5 | -2.3 | 826 |
| 4B | TL | 43.9 | 36.1 | 35.0 | 22.5 | 27.0 | 33.2 | -10.6 | +2.0 | 826 |
| 4B | TLV | 60.5 | 42.3 | 42.5 | 26.8 | 32.4 | 39.2 | -21.3 | +0.6 | 826 |
| 4B | V | 50.4 | 34.9 | 47.5 | 22.5 | 31.5 | 33.8 | -16.6 | -0.3 | 826 |
| 8B | T | 37.6 | 29.5 | 25.0 | 14.1 | 18.0 | 25.9 | -11.7 | +0.0 | 826 |
| 8B | TL | 45.1 | 34.0 | 30.0 | 22.5 | 25.2 | 31.2 | -13.9 | +0.0 | 826 |
| 8B | TLV | 64.6 | 38.6 | 47.5 | 33.8 | 38.7 | 38.6 | -25.9 | +0.0 | 826 |
| 8B | V | 55.7 | 35.3 | 42.5 | 25.4 | 31.5 | 34.1 | -21.6 | +0.0 | 826 |
| 32B | T | 42.2 | 34.0 | 22.5 | 12.7 | 16.2 | 28.4 | -13.8 | +2.6 | 826 |
| 32B | TL | 50.6 | 39.4 | 42.5 | 26.8 | 32.4 | 37.2 | -13.4 | +6.0 | 826 |
| 32B | TLV | 71.5 | 49.0 | 52.5 | 34.3 | 40.9 | 46.4 | -25.1 | +7.8 | 825 |
| 32B | V | 66.0 | 48.5 | 52.5 | 36.6 | 42.3 | 46.6 | -19.4 | +12.5 | 826 |
| n (per col) | - | - | - | - | - | - | - | - | - | - |

### Scale: accuracy vs VRAM/latency across reasoner specs

> **swept**: reasoner_spec (size + family) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 8b bf16 baseline from the representation run

_latency_ms is end-to-end and decode-inflated (~20x by the verbose-answer change); prefill_ms is the clean cost signal, and reads `-` for a backend that cannot measure a prefill/decode split. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| model_spec | T | TL | TLV | V | weights_mb | peak_vram_mb | prefill_ms | latency_ms | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| internvl3-8b-local | 19.3 [15.9-22.8] | 25.3 [22.0-28.7] | 32.6 [28.6-36.9] | 24.1 [20.2-28.4] | 15889 | 64151 | - | 5196 | 3339 |
| qwen3vl-2b-local | 24.7 [20.9-28.4] | 31.9 [28.5-35.2] | 38.3 [34.7-41.7] | 31.9 [28.3-35.6] | 4255 | 14264 | 17992 | 23760 | 3388 |
| qwen3vl-4b-local | 32.3 [27.5-37.1] | 38.6 [34.4-42.7] | 50.4 [46.6-54.1] | 42.4 [38.2-46.9] | 8876 | 17266 | 17365 | 24123 | 3388 |
| qwen3vl-8b-local | 31.9 [27.1-36.7] | 38.4 [34.4-42.5] | 52.4 [48.3-56.4] | 45.5 [41.6-49.6] | 17534 | 26995 | 13488 | 19844 | 3388 |
| n (per col) | 3386 | 3383 | 3348 | 3386 | - | - | - | - | - |

### Reasoner: accuracy by evidence source, rung, and reasoner spec

> **swept**: reasoner_spec (size + family) × evidence source × rung · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 8b bf16 baseline from the representation run · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: whether the InternVL3 deficit sits on the image step (Chart, Figure) or spreads evenly over the sources

_The reasoner sweep cut by the evidence modality a question draws on, one rung per row. It exists to locate the family gap rather than restate it: InternVL3-8B and Qwen3-VL-8B carry the same parameter count, so if the pooled deficit is about visual reasoning it should sit on Chart and Figure (the sources whose content only exists in the image) and largely vanish on Pure-text. A deficit that is flat across every source is a prompt-following or answer-format effect instead. The `Δ family` column is InternVL3-8B minus Qwen3-VL-8B in points for that cell, so a NEGATIVE value means InternVL3 is worse there. ⚠ The 8B bf16 column comes from the representation run and the other specs from the reasoner run, so the two sides survived different OOM attrition and the comparison is between pools that overlap rather than match. A question can cite SEVERAL sources and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus; the bolded All sources rows pool every question exactly once and are NOT a column sum. Per-cell n rides inline, and a thin cell reads as survivorship, not as a family effect. † marks a cell computed on fewer than 30 questions, where a single question moves accuracy by more than three points: read the direction, not the value. ⚠ INCOMPLETE GRID: internvl3-8b-local is 49 cells short of 3388. Those cells are still `oom` and were never recovered, so that spec's column rests on a slightly smaller and non-random pool._

| evidence_source | rung | internvl3-8b-local | qwen3vl-2b-local | qwen3vl-4b-local | qwen3vl-8b-local | Δ family (InternVL3 − Qwen 8B) | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| (none) | T | 36.8 [12.5-56.0] (n=19)† | 42.1 [22.2-62.5] (n=19)† | 57.9 [33.3-79.2] (n=19)† | 52.6 [31.2-73.7] (n=19)† | -15.8 | 76 |
| (none) | TL | 42.1 [22.2-62.5] (n=19)† | 57.9 [31.2-80.0] (n=19)† | 57.9 [31.6-80.0] (n=19)† | 63.2 [38.9-83.3] (n=19)† | -21.1 | 76 |
| (none) | TLV | 38.9 [18.8-58.8] (n=18)† | 52.6 [31.2-71.4] (n=19)† | 68.4 [44.4-88.9] (n=19)† | 68.4 [44.4-90.9] (n=19)† | -29.5 | 75 |
| (none) | V | 26.3 [9.1-50.0] (n=19)† | 42.1 [20.0-68.8] (n=19)† | 42.1 [22.2-62.5] (n=19)† | 47.4 [27.7-66.7] (n=19)† | -21.1 | 76 |
| Chart | T | 12.9 [7.5-19.0] (n=178) | 13.5 [8.3-18.6] (n=178) | 16.9 [10.9-23.2] (n=178) | 18.0 [12.0-23.9] (n=178) | -5.1 | 712 |
| Chart | TL | 12.4 [6.5-18.6] (n=178) | 14.0 [9.0-19.5] (n=178) | 19.7 [12.6-27.3] (n=178) | 18.5 [12.4-25.3] (n=178) | -6.2 | 712 |
| Chart | TLV | 20.5 [13.8-28.6] (n=171) | 21.3 [15.2-28.7] (n=178) | 41.0 [33.3-49.2] (n=178) | 44.4 [35.3-53.4] (n=178) | -23.9 | 705 |
| Chart | V | 14.7 [10.3-20.4] (n=177) | 24.2 [17.6-31.4] (n=178) | 34.3 [26.1-43.2] (n=178) | 44.4 [35.4-52.8] (n=178) | -29.7 | 711 |
| Figure | T | 11.7 [8.1-16.1] (n=290) | 12.8 [8.7-17.4] (n=290) | 17.2 [12.0-23.0] (n=290) | 15.2 [10.2-20.2] (n=290) | -3.4 | 1160 |
| Figure | TL | 19.4 [15.0-24.1] (n=289) | 21.7 [17.0-26.5] (n=290) | 23.8 [18.1-29.7] (n=290) | 22.4 [17.0-28.3] (n=290) | -3.0 | 1159 |
| Figure | TLV | 30.1 [24.2-35.9] (n=279) | 35.2 [29.9-40.7] (n=290) | 43.1 [35.9-49.4] (n=290) | 44.5 [37.7-51.4] (n=290) | -14.4 | 1149 |
| Figure | V | 29.3 [23.7-35.2] (n=290) | 34.1 [28.1-40.0] (n=290) | 43.8 [36.2-51.0] (n=290) | 40.3 [33.9-46.5] (n=290) | -11.0 | 1160 |
| Generalized-text (Layout) | T | 18.6 [10.6-27.3] (n=118) | 22.9 [14.8-31.2] (n=118) | 27.1 [18.0-36.1] (n=118) | 28.0 [17.9-38.2] (n=118) | -9.3 | 472 |
| Generalized-text (Layout) | TL | 29.3 [20.2-39.1] (n=116) | 29.7 [21.1-38.5] (n=118) | 34.7 [25.6-43.9] (n=118) | 38.1 [28.9-48.0] (n=118) | -8.8 | 470 |
| Generalized-text (Layout) | TLV | 45.8 [34.7-56.6] (n=107) | 36.4 [26.7-46.2] (n=118) | 46.6 [37.7-55.9] (n=118) | 50.8 [41.8-59.0] (n=118) | -5.1 | 461 |
| Generalized-text (Layout) | V | 33.1 [23.8-43.5] (n=118) | 36.4 [29.1-44.4] (n=118) | 50.0 [38.9-60.3] (n=118) | 48.3 [39.8-57.0] (n=118) | -15.3 | 472 |
| Pure-text (Plain-text) | T | 27.0 [21.1-34.0] (n=289) | 32.6 [26.0-40.1] (n=291) | 38.8 [31.3-46.7] (n=291) | 39.5 [31.6-48.1] (n=291) | -12.5 | 1162 |
| Pure-text (Plain-text) | TL | 34.0 [27.7-40.4] (n=288) | 41.6 [35.3-48.1] (n=291) | 48.1 [41.4-55.8] (n=291) | 47.4 [40.9-54.9] (n=291) | -13.4 | 1161 |
| Pure-text (Plain-text) | TLV | 37.6 [30.8-45.1] (n=279) | 40.9 [34.5-47.6] (n=291) | 51.9 [45.3-59.6] (n=291) | 55.0 [47.9-62.5] (n=291) | -17.3 | 1152 |
| Pure-text (Plain-text) | V | 25.2 [19.7-31.1] (n=290) | 29.2 [23.4-35.4] (n=291) | 39.5 [32.9-46.2] (n=291) | 44.3 [37.9-51.2] (n=291) | -19.2 | 1163 |
| Table | T | 14.7 [9.3-20.5] (n=217) | 25.3 [19.7-31.0] (n=217) | 39.6 [30.5-47.7] (n=217) | 41.0 [33.5-48.0] (n=217) | -26.3 | 868 |
| Table | TL | 23.1 [16.9-30.0] (n=216) | 34.6 [27.7-41.2] (n=217) | 51.2 [43.8-57.9] (n=217) | 49.3 [41.1-56.7] (n=217) | -26.2 | 867 |
| Table | TLV | 23.7 [17.3-31.0] (n=207) | 37.8 [31.8-43.8] (n=217) | 48.8 [41.2-56.2] (n=217) | 50.2 [42.8-56.8] (n=217) | -26.6 | 858 |
| Table | V | 11.5 [6.9-16.9] (n=217) | 26.7 [20.4-33.3] (n=217) | 35.9 [29.7-43.1] (n=217) | 37.3 [31.0-44.3] (n=217) | -25.8 | 868 |
| **All sources** | **T** | **19.3 [15.9-22.8] (n=845)** | **24.7 [20.9-28.4] (n=847)** | **32.3 [27.5-37.1] (n=847)** | **31.9 [27.1-36.7] (n=847)** | **-12.6** | **3386** |
| **All sources** | **TL** | **25.3 [22.0-28.7] (n=842)** | **31.9 [28.5-35.2] (n=847)** | **38.6 [34.4-42.7] (n=847)** | **38.4 [34.4-42.5] (n=847)** | **-13.1** | **3383** |
| **All sources** | **TLV** | **32.6 [28.6-36.9] (n=807)** | **38.3 [34.7-41.7] (n=847)** | **50.4 [46.6-54.1] (n=847)** | **52.4 [48.3-56.4] (n=847)** | **-19.8** | **3348** |
| **All sources** | **V** | **24.1 [20.2-28.4] (n=845)** | **31.9 [28.3-35.6] (n=847)** | **42.4 [38.2-46.9] (n=847)** | **45.5 [41.6-49.6] (n=847)** | **-21.3** | **3386** |
| n (per col) | - | 3339 | 3388 | 3388 | 3388 | - | - |

### Weight footprint per model_spec and quantization level

> **swept**: model_spec × quantization (weight-only memory) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **source**: annotations/model_weights.csv, a static checkpoint property; no run, no device-0 truncation · **memory axis**: weight footprint, NOT peak VRAM

_Weight footprint is a STATIC property of the checkpoint: the summed safetensors tensor bytes, so unlike the measured peak VRAM it is complete rather than device-0 only, needs no re-run, and is the figure a memory claim should cite. `method=exact` is measured from the real tensor shapes; `derived` applies bitsandbytes' layout to those shapes (int8, or packed NF4 plus double-quant constants, for the 2D Linear weights; compute dtype for embeddings, lm_head, norms and biases) rather than measuring a loaded model. `in study` marks the specs that actually produced judged cells; the rest are annotated for comparison and were never run. Weights are not the whole deployment budget: activations and the KV cache ride on top, and both scale with the input, so an image rung needs materially more than the number here. Regenerate with ops/scripts/model_weight_sizes.py. ⚠ NOT ANNOTATED, so no footprint can be quoted for: qwen3vl-8b-thinking-local. These specs have judged cells but no row in the annotation file; the figure is missing, not zero._

| model_spec | quant | weights_mb | method | quantizable_params | in study |
| --- | --- | --- | --- | --- | --- |
| internvl3-8b-local | 16bit | 15889 | exact | 6.75B | yes |
| qwen3vl-2b-local | 16bit | 4255 | exact | 1.64B | yes |
| qwen3vl-2b-local-8bit | 8bit | 2619 | derived | 1.64B | - |
| qwen3vl-2b-local-4bit | 4bit | 1827 | derived | 1.64B | - |
| qwen3vl-32b-local | 16bit | 66715 | exact | 31.51B | yes |
| qwen3vl-32b-local-8bit | 8bit | 35206 | derived | 31.51B | - |
| qwen3vl-32b-local-4bit | 4bit | 19951 | derived | 31.51B | yes |
| qwen3vl-4b-local | 16bit | 8876 | exact | 3.86B | yes |
| qwen3vl-4b-local-8bit | 8bit | 5016 | derived | 3.86B | - |
| qwen3vl-4b-local-4bit | 4bit | 3147 | derived | 3.86B | - |
| qwen3vl-8b-local | 16bit | 17534 | exact | 7.25B | yes |
| qwen3vl-8b-local-8bit | 8bit | 10285 | derived | 7.25B | yes |
| qwen3vl-8b-local-4bit | 4bit | 6775 | derived | 7.25B | yes |
| n (per col) | - | - | - | - | - |

### Mined: quantization sensitivity (accuracy + VRAM delta) by doc_type

> **swept**: quantization (bf16 / 8bit / 4bit) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 16-bit baseline from the representation run

_delta is vs the 16-bit baseline of the same model; blank when no baseline is in the cache._

| doc_type | quant | accuracy | vram_mb | acc_delta_vs_16bit | vram_delta_mb | n |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 4bit | 36.4 | 12930 | +0.2 | -11165 | 616 |
| Academic paper | 8bit | 36.5 | 17906 | +0.3 | -6189 | 616 |
| Academic paper | 16bit | 36.2 | 24095 | +0.0 | +0 | 616 |
| Administration/Industry file | 4bit | 58.2 | 15830 | +1.6 | -11165 | 256 |
| Administration/Industry file | 8bit | 58.2 | 21395 | +1.6 | -5600 | 256 |
| Administration/Industry file | 16bit | 56.6 | 26995 | +0.0 | +0 | 256 |
| Brochure | 4bit | 37.3 | 11254 | +0.6 | -9119 | 308 |
| Brochure | 8bit | 37.0 | 13433 | +0.3 | -6940 | 308 |
| Brochure | 16bit | 36.7 | 20373 | +0.0 | +0 | 308 |
| Financial report | 4bit | 47.9 | 12488 | -0.2 | -8412 | 432 |
| Financial report | 8bit | 47.5 | 14065 | -0.7 | -6835 | 432 |
| Financial report | 16bit | 48.1 | 20900 | +0.0 | +0 | 432 |
| Guidebook | 4bit | 43.8 | 14428 | +0.8 | -11163 | 480 |
| Guidebook | 8bit | 43.5 | 19656 | +0.6 | -5936 | 480 |
| Guidebook | 16bit | 42.9 | 25592 | +0.0 | +0 | 480 |
| Research report / Introduction | 4bit | 34.4 | 13555 | -1.2 | -9748 | 848 |
| Research report / Introduction | 8bit | 35.3 | 16870 | -0.4 | -6433 | 848 |
| Research report / Introduction | 16bit | 35.6 | 23303 | +0.0 | +0 | 848 |
| Tutorial/Workshop | 4bit | 51.3 | 11490 | +0.7 | -9385 | 448 |
| Tutorial/Workshop | 8bit | 52.7 | 14007 | +2.0 | -6868 | 448 |
| Tutorial/Workshop | 16bit | 50.7 | 20875 | +0.0 | +0 | 448 |
| n (per col) | - | - | - | - | - | - |

### Quantization sensitivity (overall): accuracy per rung + VRAM per quant

> **view**: summary — pooled across all doc_types · **swept**: quantization (bf16 / 8bit / 4bit) · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 16-bit baseline from the representation run

_One row per quantization level, so accuracy is directly comparable across the rungs within a level. Each rung cell is that cell's accuracy with, in parentheses, its delta against the 16-bit baseline AT THE SAME RUNG, which is what isolates the quantization effect from the rung mix. The trailing columns are that level's aggregates over all its rows, not sums or means of the rung columns. `overall acc` is its pooled correctness rate and `acc_delta_vs_16bit` compares pooled to pooled; OOM attrition differs by rung and by level (16-bit TLV survives 717 cells against 4-bit's 762), so the pooled figures mix slightly different rung compositions and the per-rung cells are the cleaner comparison. `weights_mb` is WEIGHTS ONLY, with no activations and no device-0 truncation: it is a static property of the checkpoint (summed safetensors tensor bytes), so it needs no re-run and is complete. The 16-bit figure is exact; a trailing `~` marks a derived figure, computed by applying bitsandbytes' layout to the real tensor shapes (int8 or packed NF4 plus double-quant constants for the 2D Linear weights, compute dtype for embeddings, lm_head, norms and biases) rather than measured on a loaded model. Regenerate with ops/scripts/model_weight_sizes.py. `vram_mb` is the MAXIMUM peak over the level's rows, not an average, because it is a headroom figure and the binding cell is what matters. Compare it against `weights_mb` only with the caveat below in mind. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. Cells were generated on 2x V100, and the reasoner loads with device_map="auto", which shards the model across both GPUs for every spec (the shard is triggered by GPU count, not model size). But peak memory is recorded with `torch.cuda.max_memory_allocated()` and no device argument, so only device 0 is measured: reported minima land at about half each model's bf16 weight size (8B: 7.82 GB against ~16 GB of weights). Device 1's peak was never written to any row and is not recoverable from the cache. Treat these as a device-0 lower bound, not a deployment budget. See docs/CODEBASE_GUIDE.md Part B section 9._

| quant | T | TL | TLV | V | overall acc | weights_mb | vram_mb (max) | acc_delta_vs_16bit | vram_delta_mb | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 4bit | 31.8 (-0.1) | 39.4 (+1.1) | 51.8 (-0.6) | 45.5 (+0.0) | 42.1 | 6775~ | 15830 | +0.1 | -11165 | 3388 |
| 8bit | 32.5 (+0.6) | 37.9 (-0.5) | 53.6 (+1.2) | 45.7 (+0.2) | 42.4 | 10285~ | 21395 | +0.4 | -5600 | 3388 |
| 16bit | 31.9 (+0.0) | 38.4 (+0.0) | 52.4 (+0.0) | 45.5 (+0.0) | 42.0 | 17534 | 26995 | +0.0 | +0 | 3388 |
| n (per col) | 2541 | 2541 | 2541 | 2541 | - | - | - | - | - | - |

### Mined: quantization sensitivity by evidence source and rung

> **swept**: quantization (bf16 / 8bit / 4bit) × evidence source × rung · **dataset**: mmlongbench · **scan**: any (digital+scanned) · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: 16-bit baseline from the representation run · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: whether the small pooled 4-bit cost concentrates on the numeric, dense-table sources or is flat across them

_The same quantization sweep, cut by the evidence modality a question draws on and held at one rung per row, so the delta is a quantization effect and not a rung mix. Each cell is that cell's accuracy with, in parentheses, its delta against the 16-bit baseline for the SAME source and SAME rung, then its n. The reason to cut it this way: a pooled quantization delta near zero can be a genuinely flat cost or it can be a numeric, dense-table loss cancelling against a gain elsewhere, and only the per-source column tells those apart. VRAM is not repeated here (it is a property of the checkpoint and the rung, not of the evidence source) — read it off the doc_type and overall quantization tables. A question can cite SEVERAL sources and is counted in every block it cites, so the blocks OVERLAP and their n do not sum to the corpus; the bolded All sources rows pool every question exactly once and are NOT a column sum. Per-cell n rides inline: OOM attrition differs by rung and by quant level, so a thin cell reads as survivorship rather than as a quantization effect. † marks a cell computed on fewer than 30 questions, where a single question moves accuracy by more than three points: read the direction, not the value._

| evidence_source | rung | 4bit | 8bit | 16bit | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 52.6 (+0.0) (n=19)† | 52.6 (+0.0) (n=19)† | 52.6 (n=19)† | 57 |
| (none) | TL | 57.9 (-5.3) (n=19)† | 57.9 (-5.3) (n=19)† | 63.2 (n=19)† | 57 |
| (none) | TLV | 68.4 (+0.0) (n=19)† | 73.7 (+5.3) (n=19)† | 68.4 (n=19)† | 57 |
| (none) | V | 47.4 (+0.0) (n=19)† | 52.6 (+5.3) (n=19)† | 47.4 (n=19)† | 57 |
| Chart | T | 17.4 (-0.6) (n=178) | 18.5 (+0.6) (n=178) | 18.0 (n=178) | 534 |
| Chart | TL | 23.0 (+4.5) (n=178) | 19.1 (+0.6) (n=178) | 18.5 (n=178) | 534 |
| Chart | TLV | 39.3 (-5.1) (n=178) | 46.6 (+2.2) (n=178) | 44.4 (n=178) | 534 |
| Chart | V | 42.1 (-2.2) (n=178) | 41.6 (-2.8) (n=178) | 44.4 (n=178) | 534 |
| Figure | T | 18.6 (+3.4) (n=290) | 17.6 (+2.4) (n=290) | 15.2 (n=290) | 870 |
| Figure | TL | 24.5 (+2.1) (n=290) | 22.4 (+0.0) (n=290) | 22.4 (n=290) | 870 |
| Figure | TLV | 45.9 (+1.4) (n=290) | 47.2 (+2.8) (n=290) | 44.5 (n=290) | 870 |
| Figure | V | 42.1 (+1.7) (n=290) | 42.4 (+2.1) (n=290) | 40.3 (n=290) | 870 |
| Generalized-text (Layout) | T | 27.1 (-0.8) (n=118) | 28.8 (+0.8) (n=118) | 28.0 (n=118) | 354 |
| Generalized-text (Layout) | TL | 39.0 (+0.8) (n=118) | 37.3 (-0.8) (n=118) | 38.1 (n=118) | 354 |
| Generalized-text (Layout) | TLV | 49.2 (-1.7) (n=118) | 51.7 (+0.8) (n=118) | 50.8 (n=118) | 354 |
| Generalized-text (Layout) | V | 50.0 (+1.7) (n=118) | 47.5 (-0.8) (n=118) | 48.3 (n=118) | 354 |
| Pure-text (Plain-text) | T | 37.5 (-2.1) (n=291) | 40.2 (+0.7) (n=291) | 39.5 (n=291) | 873 |
| Pure-text (Plain-text) | TL | 46.7 (-0.7) (n=291) | 45.7 (-1.7) (n=291) | 47.4 (n=291) | 873 |
| Pure-text (Plain-text) | TLV | 56.0 (+1.0) (n=291) | 54.3 (-0.7) (n=291) | 55.0 (n=291) | 873 |
| Pure-text (Plain-text) | V | 45.4 (+1.0) (n=291) | 45.7 (+1.4) (n=291) | 44.3 (n=291) | 873 |
| Table | T | 37.3 (-3.7) (n=217) | 36.4 (-4.6) (n=217) | 41.0 (n=217) | 651 |
| Table | TL | 49.8 (+0.5) (n=217) | 48.4 (-0.9) (n=217) | 49.3 (n=217) | 651 |
| Table | TLV | 49.3 (-0.9) (n=217) | 48.4 (-1.8) (n=217) | 50.2 (n=217) | 651 |
| Table | V | 37.8 (+0.5) (n=217) | 37.8 (+0.5) (n=217) | 37.3 (n=217) | 651 |
| **All sources** | **T** | **31.8 (-0.1) (n=847)** | **32.5 (+0.6) (n=847)** | **31.9 (n=847)** | **2541** |
| **All sources** | **TL** | **39.4 (+1.1) (n=847)** | **37.9 (-0.5) (n=847)** | **38.4 (n=847)** | **2541** |
| **All sources** | **TLV** | **51.8 (-0.6) (n=847)** | **53.6 (+1.2) (n=847)** | **52.4 (n=847)** | **2541** |
| **All sources** | **V** | **45.5 (+0.0) (n=847)** | **45.7 (+0.2) (n=847)** | **45.5 (n=847)** | **2541** |
| n (per col) | - | 3388 | 3388 | 3388 | - |

### Mined: peak-VRAM headroom vs the 16 GB V100 ceiling

> **swept**: spec / rung / resolution (peak VRAM) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

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

> **view**: summary — pooled across all doc_types · **swept**: spec / rung / resolution (peak VRAM) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

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

> **swept**: rung / resolution / pages-fed (OOM rate) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: OOM from status rows, pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

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

> **view**: summary — pooled across all doc_types · **swept**: rung / resolution / pages-fed (OOM rate) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **note**: OOM from status rows, pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

_rate = oom cells / all cells; pooled over page buckets and G1 runs._

| rung | high | low | med | n_total |
| --- | --- | --- | --- | --- |
| T | - | - | 1.2 | 5082 |
| TL | - | - | 6.7 | 5082 |
| TLV | 19.6 | 13.6 | 11.2 | 7623 |
| V | 4.4 | 0.4 | 0.8 | 7623 |
| n (per col) | 1694 | 1694 | 22022 | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: representation (prefill / input tokens) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling · **TV**: absent: TV only ever ran on the H100, and a latency column cannot mix the two machines. TV's cost sits in the token counts, which are machine-independent: 929 text + 3,404 visual against TLV's 1,644 + 3,404, i.e. 44% less text and 14% less total input on the same questions

_`prefill_ms` and `input_tokens` are the INPUT-bound cost, set by the representation. `decode_ms` and `output_tokens` are the OUTPUT-bound cost, set by the prompt and the decode budget, not by the rung: a rung appears to decode more only because a longer input tends to draw a longer answer. Read the two halves separately; their sum is not the end-to-end latency, which also carries scheduling and detokenisation. ⚠ These rows come from the prompt_mode=none run, which carries NO instruction at all (`config.PROMPT_MODES['none']` is the empty string), so the model rambles and `decode_ms` here is an upper bound, not a deployment figure. The per-prompt-mode decode table gives the instructed cost, on different hardware._

| doc_type | rung | prefill_ms | input_tokens | decode_ms | output_tokens | n |
| --- | --- | --- | --- | --- | --- | --- |
| Academic paper | T | 2781 | 1616 | 7894 | 157 | 148 |
| Academic paper | TL | 2940 | 1697 | 8006 | 158 | 130 |
| Academic paper | TLV | 24666 | 4026 | 7897 | 156 | 119 |
| Academic paper | V | 27539 | 3201 | 8207 | 164 | 153 |
| Administration/Industry file | T | 1539 | 867 | 4109 | 82 | 60 |
| Administration/Industry file | TL | 1510 | 860 | 3722 | 75 | 57 |
| Administration/Industry file | TLV | 20710 | 3013 | 3705 | 75 | 55 |
| Administration/Industry file | V | 24313 | 2827 | 4485 | 90 | 61 |
| Brochure | T | 1022 | 565 | 5216 | 104 | 75 |
| Brochure | TL | 1423 | 808 | 6259 | 121 | 76 |
| Brochure | TLV | 27298 | 3523 | 6464 | 126 | 72 |
| Brochure | V | 28097 | 3114 | 6234 | 123 | 77 |
| Financial report | T | 1920 | 1140 | 7774 | 157 | 107 |
| Financial report | TL | 3280 | 1878 | 6132 | 122 | 70 |
| Financial report | TLV | 20855 | 3844 | 6071 | 119 | 68 |
| Financial report | V | 23207 | 2709 | 8698 | 176 | 108 |
| Guidebook | T | 1004 | 557 | 4627 | 92 | 120 |
| Guidebook | TL | 1451 | 828 | 5623 | 111 | 115 |
| Guidebook | TLV | 22818 | 3118 | 5585 | 110 | 110 |
| Guidebook | V | 24237 | 2735 | 5344 | 106 | 118 |
| Research report / Introduction | T | 1197 | 639 | 5818 | 113 | 209 |
| Research report / Introduction | TL | 1520 | 866 | 7720 | 144 | 202 |
| Research report / Introduction | TLV | 29156 | 3503 | 8053 | 149 | 186 |
| Research report / Introduction | V | 34775 | 3530 | 8090 | 151 | 207 |
| Tutorial/Workshop | T | 272 | 53 | 3169 | 57 | 112 |
| Tutorial/Workshop | TL | 719 | 371 | 6140 | 110 | 111 |
| Tutorial/Workshop | TLV | 32465 | 3326 | 6280 | 111 | 107 |
| Tutorial/Workshop | V | 33952 | 3247 | 6394 | 113 | 110 |
| **all doc_types** | **T** | **1428** | **797** | **5733** | **113** | **831** |
| **all doc_types** | **TL** | **1787** | **1017** | **6630** | **127** | **761** |
| **all doc_types** | **TLV** | **26311** | **3501** | **6703** | **128** | **717** |
| **all doc_types** | **V** | **28968** | **3124** | **7143** | **138** | **834** |
| n (per col) | - | - | - | - | - | - |

### Reasoner cost: prefill / decode per rung, and the input-token profile

> **swept**: reasoner config × rung (prefill / decode / input tokens) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: cost rows use the cells every config in a machine group ran; token rows use the complete pool · **page_selection**: oracle · **prompt_mode**: none · **machine**: rows grouped by measuring machine; the V100 and H100 groups are never comparable · **note**: the builder loads its own per-group snapshots, so the plan's own load is unused

_Prefill and decode in seconds, mean over the cells every config in the machine group ran (`n` per rung is that matched intersection, so a difference down a group is the config, not the pool). ⚠ NEVER compare a 2xV100 row against an H100 row. The V100 rows are the pre-recovery `results.v100.jsonl` snapshots; the 32B and Thinking runs only ever ran post-migration on an H100, which prefills the same input roughly 50x faster, so the two groups are separate tables that happen to share columns. The `machine` field on the row is `local` everywhere and cannot distinguish them; the file split is the only handle. Prefill is the input-bound cost set by the representation, decode the output-bound cost set by the prompt and the decode budget. Their sum is not end-to-end latency, which also carries scheduling and detokenisation. All rows are prompt_mode=none, which carries NO instruction (`config.PROMPT_MODES['none']` is the empty string), so the model rambles to the 256-token cap and decode is an uninstructed upper bound; the Thinking row emits reasoning as well, so its decode is not comparable even to the H100 rows beside it. Input-token rows depend only on the rung (identical across every Qwen3-VL spec, which share a tokenizer); InternVL3-8B packs vision differently and is excluded from them. They cover the 840 of 847 answerable questions that were actually fed pages: 7 questions on `mi_phone.pdf` resolve to an EMPTY page set in every run despite carrying valid gold pages, so they are fed no evidence, score 0 everywhere, and would otherwise put a nonsensical ~32-token floor under the image rungs (32 tokens is the bare prompt scaffolding, not a page). Because the V100 groups exclude the cells that OOMed, their inputs are shorter than the complete-pool row: TLV averages 3,501 tokens over the V100 matched cells against 5,049 over the full pool, so the V100 latencies price a lighter input than the token rows show._

| group | config | metric | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2xV100 | Qwen3-VL-8B 16-bit | prefill_s | 1.4 | 1.8 | 26.3 | 29.0 | 717 |
| 2xV100 | Qwen3-VL-8B 16-bit | decode_s | 5.7 | 6.6 | 6.7 | 7.1 | 717 |
| 2xV100 | Qwen3-VL-8B 8-bit | prefill_s | 0.7 | 0.9 | 25.0 | 28.2 | 717 |
| 2xV100 | Qwen3-VL-8B 8-bit | decode_s | 18.4 | 21.2 | 21.2 | 21.8 | 717 |
| 2xV100 | Qwen3-VL-8B 4-bit | prefill_s | 1.5 | 1.8 | 28.0 | 30.6 | 717 |
| 2xV100 | Qwen3-VL-8B 4-bit | decode_s | 9.2 | 10.7 | 10.3 | 11.1 | 717 |
| 2xV100 | Qwen3-VL-2B | prefill_s | 0.4 | 0.4 | 29.8 | 34.6 | 717 |
| 2xV100 | Qwen3-VL-2B | decode_s | 4.8 | 5.5 | 5.8 | 6.3 | 717 |
| 2xV100 | Qwen3-VL-4B | prefill_s | 0.9 | 1.1 | 31.1 | 35.6 | 717 |
| 2xV100 | Qwen3-VL-4B | decode_s | 6.2 | 7.3 | 6.3 | 7.4 | 717 |
| H100 | Qwen3-VL-32B | prefill_s | 0.2 | 0.3 | 0.5 | 0.2 | 683 |
| H100 | Qwen3-VL-32B | decode_s | 5.1 | 6.4 | 6.5 | 6.0 | 683 |
| H100 | Qwen3-VL-32B 4-bit | prefill_s | 0.3 | 0.4 | 0.6 | 0.3 | 683 |
| H100 | Qwen3-VL-32B 4-bit | decode_s | 4.4 | 5.5 | 5.7 | 5.2 | 683 |
| H100 | Qwen3-VL-8B-Thinking | prefill_s | 0.1 | 0.1 | 0.2 | 0.1 | 683 |
| H100 | Qwen3-VL-8B-Thinking | decode_s | 24.3 | 26.6 | 20.3 | 16.1 | 683 |
| 2xV100 | InternVL3-8B | prefill_s | - | - | - | - | 3180 |
| 2xV100 | InternVL3-8B | decode_s | - | - | - | - | 3180 |
| (any) | input tokens | mean | 938 | 1658 | 5091 | 3470 | 840 |
| (any) | input tokens | min-max | 29-26636 | 37-29489 | 1838-58679 | 1822-43227 | 840 |
| n (per col) | - | - | 831 | 761 | 717 | 834 | - |

### Decode cost by prompt mode (TLV, oracle pages)

> **swept**: prompt_mode × decode cost, at TLV · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV only · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **reading**: the uninstructed none row is an upper bound and is flagged; cot/extract_cot carry an 8x decode budget

_Decode cost per prompt mode at one rung, so the input side is held fixed and every difference down the table is the instruction's doing. Same questions, same oracle pages, same reasoner. Read the `instruction` and `budget` columns before comparing any two rows. The `none` mode is marked ⚠ because it carries NO instruction at all (`config.PROMPT_MODES['none']` is the empty string), so nothing asks the model to stop: its decode time and output length are an uninstructed upper bound and must not be averaged in with the five instructed modes, which all end in 'Keep the answer concise.' `cot` and `extract_cot` additionally run under a 2048-token budget against 256 for the rest, so their ceiling is eight times higher and part of their decode cost is headroom the other modes never had. Prefill is printed to show it is flat across modes, which is the check that the input side really is held fixed._

| prompt_mode | instruction | budget | decode_ms | output_tokens | prefill_ms | n |
| --- | --- | --- | --- | --- | --- | --- |
| none ⚠ | none (uninstructed) | 256 | 2438 | 136 | 177 | 847 |
| grounded | concise | 256 | 171 | 10 | 177 | 847 |
| abstain | concise | 256 | 114 | 7 | 178 | 847 |
| abstain_balanced | concise | 256 | 119 | 8 | 179 | 847 |
| cot | concise | 2048 | 2979 | 166 | 178 | 847 |
| extract_cot | concise | 2048 | 4507 | 242 | 181 | 846 |
| n (per col) | - | - | - | - | - | - |

### Routing policies: accuracy vs input-token cost

> **swept**: routing policy · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **prompt_mode**: none · **note**: the builder loads the complete pool itself so the policies sit on the same rows as the ladder they route over, and the plan's own load is unused; the G3 classifier probe rides in the footer · **cost**: mean input tokens, not seconds — the machine-independent quantity, since the two measuring machines prefill the same input ~50x apart

_Cost is the mean INPUT TOKENS a policy feeds the reasoner, not a latency. Tokens are the machine-independent quantity: the same input prefills in ~26 s on the 2xV100s and ~0.5 s on the H100 (see the generation-cost table), so a second-denominated cost column would read as a hardware claim this build cannot support, while the token count is a property of the representation. `rel` is the policy's tokens over the reference rung's. `route_by_doc_class` sends each document class to the rung the frontier rule picks for it (cheapest rung whose upper CI reaches within the margin of that class's best), so its rung choices are exactly the frontier column of the ladder-by-doc_type table. Those choices are fitted on this corpus and read as an upper bound on what the policy transfers. Document class is a document-level property, so the policy needs no per-question prediction; the classifier probe in the footer is the harder job of predicting a question's modality bin, and is reported because the routing argument only holds while the routing decision is near-free._

| policy | accuracy | input_tokens | rel | n | note |
| --- | --- | --- | --- | --- | --- |
| uniform_T | 31.9 | 930 | 0.18 | 847 |  |
| uniform_TL | 38.8 | 1644 | 0.33 | 847 |  |
| uniform_TV | 51.6 | 4333 | 0.86 | 847 |  |
| uniform_TLV | 52.5 | 5049 | 1.00 | 847 |  |
| uniform_V | 45.6 | 3442 | 0.68 | 847 |  |
| route_by_doc_class | 45.6 | 2410 | 0.48 | 847 | 62% of questions to an image-free rung; Academic paper=T, Administration/Industry file=T, Brochure=TL, Financial report=T, Guidebook=T, Research report / Introduction=TV, Tutorial/Workshop=TV |
| n (per col) | 847 | - | - | - | - |
| modality-bin classifier | 11.1% correct (n=135) | - | - | - | predicts a question's bin, not the document class the policy routes on |

## Cross-cutting / levers

### Paired-difference bootstrap intervals for the asserted comparisons

> **swept**: paired difference per asserted comparison (bootstrap CI on the delta) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question; a question enters only if scored on both sides, so n is the intersection pool · **sides**: each comparison names its own run_tags and specs; the builder loads them rather than slicing one pooled read

_Each row is ONE bootstrap interval on a difference, not two marginal intervals read against each other. The two sides of a comparison are measured on the same questions, so their errors are correlated; marginal CIs ignore that correlation and are the wrong instrument for a difference-claim. Convention matches the marginal CIs exactly (scoring.paired reuses scoring.accuracy's quantiles): documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles. Pairing is per question: a question enters only if it has a scored result on BOTH sides, so `n (paired)` is the intersection pool, not either side's own n. Accuracy rows read `right - left` in points, so POSITIVE means the right-hand condition is better. `M-S` rows are a DIFFERENCE OF DIFFERENCES: the multi-page deficit at the right-hand rung minus that deficit at the left-hand rung, recomputed whole on every resample. A deficit is negative when multi-page evidence is worse, so a NEGATIVE difference-of-differences means the deficit WIDENS as you move right. `excludes 0` is the whole interval sitting on one side of zero; a row that does not exclude zero does not support a directional claim, which is the point of the column. Read the note column before quoting a row whose pool is short of the 847-question complete pool._

| comparison | rung(s) | Δ (points) | CI low | CI high | n (paired) | excludes 0 | note |
| --- | --- | --- | --- | --- | --- | --- | --- |
| integration deficit (M-S): TL vs T | TL - T | -1.6 | -7.6 | +5.3 | 838 | no | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): TV vs T | TV - T | -11.4 | -18.3 | -4.8 | 838 | yes | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): TLV vs T | TLV - T | -12.8 | -20.5 | -4.6 | 838 | yes | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): V vs T | V - T | -9.5 | -18.1 | -1.6 | 838 | yes | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| representation margin: TLV vs T | TLV - T | +20.7 | +15.4 | +26.2 | 847 | yes | - |
| parser-free lateral: TLV vs TV | TLV - TV | +0.9 | -1.3 | +3.3 | 847 | no | - |
| scale: 32B vs 8B at V | V | +11.2 | +8.3 | +14.2 | 847 | yes | left (qwen3vl-8b-local): 13 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| scale: 32B vs 8B at T | T | +3.7 | +1.5 | +5.7 | 847 | yes | left (qwen3vl-8b-local): 16 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| family: Qwen3-VL-8B vs InternVL3-8B at TLV | TLV | +21.1 | +17.0 | +24.9 | 807 | yes | left (internvl3-8b-local): 105 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first); right (qwen3vl-8b-local): 130 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| integration deficit (M-S): Thinking vs base 8B at TLV | TLV | +13.9 | +7.3 | +21.0 | 678 | yes | 7 hop=none dropped by design (no integration reading), same rule as the integration tables; left (qwen3vl-8b-local): 130 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first); right (qwen3vl-8b-thinking-local): 8 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first); 343 never generated (run unfinished, stops in corpus order, so the shortfall is unrelated to difficulty) |

### Levers: what each inference-time intervention does, where data exists

> **swept**: inference-time lever × effect · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **sources**: each lever row loads its own run_tag(s) in the builder; blank rows await their runs · **retrieval depth**: PROVISIONAL (partial G2 pool)

_One row per lever: the measured baseline, the lever value, and the delta in points, each with its n. A blank row means the lever's run has not landed; a populated row is never imputed across pools. Metrics differ by row (accuracy at the named rung, or abstention rate on the unanswerable pool) and are named per row: read the metric column, not just the delta. The parser-drop row runs the other way from every other lever: its baseline is the STRONGER side (TLV), so a small negative delta is the point, since TV costs 44% fewer text tokens and skips the parser pass entirely. A lever with both an `acc @ TLV` row and an `M−S @ TLV` row is the same cells read two ways: the accuracy row is how far the level moved, the M−S row is whether the multi-page deficit narrowed with it (a POSITIVE M−S delta means it narrowed). A lever that lifts accuracy but leaves M−S flat did not recover integration, it raised both hops together. The retrieval-depth row is PROVISIONAL (partial G2 pool). The abstention row reads the ORIGINAL three-mode G3 run (targeted vs none); its six-mode re-run replaces it when judged. Deltas across different pools/runs are directional findings, not matched comparisons._

| lever | targets | metric | baseline | lever value | delta | n (base/lever) |
| --- | --- | --- | --- | --- | --- | --- |
| resolution med→high | E3 fidelity | acc @ TLV | 52.5 | 54.7 | +2.1 | 847/847 |
| drop the parser (TLV→TV) | E1 acquisition | acc @ image rung | 52.5 | 51.6 | -0.9 | 847/847 |
| interleaving TLV→TLVi | E4 reasoning | acc @ TLV | 52.8 | 55.0 | +2.2 | 847/847 |
| CoT prompt (grounded→cot) | E4 reasoning | acc @ TLV | 45.7 | 53.1 | +7.4 | 847/847 |
| CoT prompt (M−S) | E4 reasoning | M−S @ TLV | -22.9 | -16.5 | +6.4 | 847/847 |
| extraction (grounded→extract_cot) | E4 reasoning | acc @ TLV | 45.7 | 50.2 | +4.5 | 847/846 |
| extraction (M−S) | E4 reasoning | M−S @ TLV | -22.9 | -16.0 | +6.8 | 847/846 |
| abstention prompt (none→targeted) | E5 faithfulness | abstention @ TLV (unanswerable) | 16.8 | 74.6 | +57.8 | 244/244 |
| retrieval depth k1→k5 (vision) | E2 selection | acc @ V (PROVISIONAL) | 28.9 | 36.2 | +7.2 | 304/304 |
| model swap 8B→InternVL3-8B | reasoner | acc @ TLV | 52.4 | 32.6 | -19.8 | 847/807 |
| thinking variant (M−S) | E4 reasoning | M−S @ TLV | -25.8 | -8.0 | +17.8 | 847/685 |
| n (per col) | - | - | - | - | - | - |

### Prompt levers: accuracy by evidence hop per prompt mode (TLV, oracle pages)

> **swept**: prompt_mode (none / grounded / cot / extract_cot) × evidence hop, at TLV · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: TLV only · **pool**: complete answerable pool — g4-faithfulness-full prompt_mode=none (T/TL/TLV/V) + g1-tv-full (TV), 847 questions x 5 rungs, no OOM attrition · **page_selection**: oracle · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **reading**: whether a prompt lever that lifts pooled accuracy also narrows the multi-page deficit, or only shifts the level

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. Accuracy columns are percentages. `M − S` is multi-page accuracy MINUS single-page accuracy, in points, so it reads as how multi-page evidence performs relative to single-page: a NEGATIVE value means multi-page is worse. Rows are prompt modes at the TLV rung on the complete answerable pool, same questions and same oracle pages throughout, so the only thing that changes down the table is the instruction preamble. The table exists because a pooled accuracy lift does not say WHICH deficit the lever repaired: a prompt can raise single- and multi-page accuracy together and leave the integration gap exactly where it was, which is a different (and weaker) claim than recovering integration. `Δ M − S vs grounded` is this row's gap minus the grounded row's gap, in points, so a POSITIVE value means the lever NARROWED the multi-page deficit and a value near zero means it lifted the level without touching the gap. The `none` row is the uninstructed anchor (the headline ladder's TLV condition, less the handful of hop=none questions), not a lever, and the two abstain rows are faithfulness prompts carried here for completeness: on an answerable pool their accuracy is depressed by false abstention, which the false-abstention table under Faithfulness measures directly._

| prompt_mode | single | multi | M − S | Δ M − S vs grounded | n |
| --- | --- | --- | --- | --- | --- |
| none | 63.5 [58.1-68.8] | 38.5 [32.6-44.7] | -25.0 | -2.1 | 838 |
| grounded | 55.8 [50.9-61.2] | 33.0 [26.8-39.5] | -22.9 | +0.0 | 838 |
| cot | 60.6 [55.6-65.6] | 44.1 [38.4-50.2] | -16.5 | +6.4 | 838 |
| extract_cot | 57.5 [52.7-62.7] | 41.5 [36.1-47.2] | -16.0 | +6.8 | 837 |
| abstain | 50.8 [45.7-56.1] | 29.9 [24.2-36.2] | -20.9 | +1.9 | 838 |
| abstain_balanced | 52.1 [46.9-57.4] | 31.0 [25.3-37.1] | -21.1 | +1.8 | 838 |
| n (per col) | 2880 | 2147 | - | - | - |

### Attribution: representation / retrieval / reasoning loss per rung (PROVISIONAL)

> **swept**: loss channel (representation / retrieval / reasoning) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **retrieval source**: g2-retrieval-full generation rows, loaded by the builder · **status**: PROVISIONAL (partial G2 pool)

_PROVISIONAL (partial G2 pool). The retrieval-loss columns are built on the g2-retrieval-full generation pool, which was only ~36% pulled before the cluster migration with judging still in flight, so every retrieval number here is provisional until a clean re-run. The reasoning residual is a RAW, UNCORRECTED UPPER BOUND: it is simply the shortfall of the best oracle rung from 100%, and it still contains judge false negatives and answers that are correct without matching the gold span. Neither correction exists in the data, so neither has been netted out. Do not read the residual as a reasoning-error estimate. T and TL carry no retrieval column because G2 never ran the text-only rungs; TLV above k=3 and all k>=7 are blank because OOM attrition leaves too few comparable cells. Retrieval loss is measured against the BEST in-scope retrieval setting for that rung, so it is the conservative (smallest defensible) retrieval charge, and it is computed within-question against the same questions' oracle rows._

| rung | oracle acc | representation loss | retrieval ref | retrieved acc | retrieval loss | reasoning residual (raw UB) | oracle n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 31.9 [27.1-36.7] | +20.5 | - | - | - | - | 847 |
| TL | 38.4 [34.4-42.5] | +14.0 | - | - | - | - | 847 |
| TLV | 52.4 [48.3-56.4] | 0.0 (best rung) | joint k1 (paired n=278) | 42.1 | +10.4 | +47.6 | 847 |
| V | 45.5 [41.6-49.6] | +7.0 | joint k5 (paired n=226) | 36.3 | +3.1 | - | 847 |
| n (per col) | 3388 | - | - | - | - | - | - |

## Reconciliation & coverage

### ⚠ RECONCILIATION FAILED

Anchor cells that must reproduce already-trusted numbers, checked after the tables are assembled. **The one remaining FAIL is expected and explained**, and it withholds no table this report cites.

- `G3 re-run none abstention` reads 13.5 against 16.9: the known instability of the no-instruction abstention baseline. The two instructed modes reproduce (grounded 10.5 vs 10.7, abstain 79.3 vs 80.7), so the prompt assembly is intact and only the uninstructed rate moves.

The ladder anchors were re-baselined onto the complete pool once the H100 pass recovered 1,953 OOM cells (TLV 56.8 -> 52.4, TL 39.4 -> 38.4). That is a pool correction rather than drift, and it is verified from both directions: g1-representation-full and the independent g4-faithfulness-full now agree on TLV to 0.1 of a point on the same 847 questions. The survivor-pool figures are preserved per tag in `results.v100.jsonl` and still drive the two reconciliation tables below.

`SKIP` means the check's anchor table is not emitted separately in this report.

```
reconciliation:
  [SKIP] headline T reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B T == headline (expected 31.9, got 31.9)
  [PASS] G4 none T reproduces the headline ladder (expected 31.9, got 31.9)
  [SKIP] headline TL reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B TL == headline (expected 38.4, got 38.4)
  [PASS] G4 none TL reproduces the headline ladder (expected 38.4, got 38.8)
  [SKIP] headline TLV reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B TLV == headline (expected 52.4, got 52.4)
  [PASS] G4 none TLV reproduces the headline ladder (expected 52.4, got 52.5)
  [SKIP] headline V reproduces the trusted ladder
  [PASS] reasoner_unified precision 8B V == headline (expected 45.5, got 45.5)
  [PASS] G4 none V reproduces the headline ladder (expected 45.5, got 45.6)
  [FAIL] G3 re-run none abstention reproduces the legacy rate (expected 16.9, got 13.5)
  [PASS] G3 re-run grounded abstention reproduces the legacy rate (expected 10.7, got 10.549999999999999)
  [PASS] G3 re-run abstain abstention reproduces the legacy rate (expected 80.7, got 79.29999999999998)
```

### Reconciliation: ladder accuracy on the full pool vs the V100 survivor pool

> **swept**: pool (full answerable vs V100 survivor) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **flag**: a rung moving more than 2 points is marked ⚠

_Same reasoner, pages, parser and prompt on both sides; the only difference is which questions survived. Δ is full minus survivor, flagged ⚠ beyond 2 points. A NEGATIVE Δ means the survivor pool was reporting an optimistic number, because the questions OOM removed were the harder ones. The per-rung n gap is the size of that attrition, which is why it is printed rather than described._

| rung | full pool | n (full) | survivor pool | n (survivor) | Δ (full − survivor) |
| --- | --- | --- | --- | --- | --- |
| T | 31.9 | 847 | 31.9 | 831 | -0.0 |
| TL | 38.8 | 847 | 39.4 | 761 | -0.6 |
| TLV | 52.5 | 847 | 56.8 | 717 | -4.2 ⚠ |
| V | 45.6 | 847 | 45.9 | 834 | -0.4 |

### Reconciliation: integration deficit (M − S) on the full pool vs the V100 survivor pool

> **swept**: pool (full answerable vs V100 survivor) × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **flag**: a rung whose deficit moves more than 2 points is marked ⚠ · **reading**: more negative = wider integration deficit

_`M − S` is multi-page minus single-page accuracy in points, so it is NEGATIVE when multi-page evidence is worse, and a MORE negative value is a WIDER deficit. Δ is full minus survivor, flagged ⚠ beyond 2 points: a negative Δ means the survivor pool understated the deficit. The n columns are single/multi per pool, and the multi column is where OOM attrition concentrated, since it tracks page count. hop=none is dropped on both sides, the same rule the other integration tables use._

| rung | full M − S | n (full S/M) | survivor M − S | n (survivor S/M) | Δ deficit |
| --- | --- | --- | --- | --- | --- |
| T | -12.2 | 480/358 | -12.1 | 479/343 | -0.1 |
| TL | -13.7 | 480/358 | -13.1 | 473/279 | -0.6 |
| TLV | -25.0 | 480/358 | -20.3 | 472/236 | -4.7 ⚠ |
| V | -21.7 | 480/358 | -20.8 | 480/345 | -0.9 |

### Pool coverage: cells the earlier V100 run lost to OOM, recovered on the H100

> **swept**: cell pool coverage (shared with the earlier ladder vs recovered) · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none (the condition both runs share)

_`shared cells` are the same question/rung pairs the earlier ladder scored and should reproduce it; `recovered cells` are the ones it never completed. A lower recovered column means the pool the earlier run lost was the harder part of it, so a pooled comparison against the earlier number is not like-for-like._

| rung | earlier run | shared cells | recovered cells | new run (all) | n shared / recovered |
| --- | --- | --- | --- | --- | --- |
| T | 31.9 | 31.9 | - | 31.9 | 847 / 0 |
| TL | 38.4 | 38.8 | - | 38.8 | 847 / 0 |
| TLV | 52.4 | 52.5 | - | 52.5 | 847 / 0 |
| V | 45.5 | 45.6 | - | 45.6 | 847 / 0 |

### Source stratification: oracle accuracy by source dataset and rung

> **swept**: source_dataset stratum × rung · **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none · **strata**: loader dataset id only; no upstream QA provenance exists

_This table cannot separate inherited from native questions, and the blank is the finding. `metadata.source_dataset` is the loader's dataset identifier, not the upstream QA dataset a question came from, so every judged row reads `mmlongbench` and no inherited-minus-native gap column can be computed. MMLongBench-Doc does not publish per-question upstream provenance in the staged config (the parquet carries doc_id, doc_type, question, answer, evidence_pages, evidence_sources, answer_format and nothing else), and no annotation file supplies it. So the memorisation-suspect channel is UNMEASURABLE on current data, not measured and found absent; closing it needs hand-labelling of document origin, which no run spec can produce. The `(uncoded)` stratum is the cells whose metadata is empty because they OOMed before producing an answer; they are shown with their n and no accuracy rather than dropped or imputed._

| source_dataset | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| mmlongbench | 31.9 [27.1-36.7] | 38.4 [34.4-42.5] | 52.4 [48.3-56.4] | 45.5 [41.6-49.6] | 3388 |
| (uncoded) | 16 cells, no acc | 86 cells, no acc | 130 cells, no acc | 13 cells, no acc | 245 |
| n (per col) | 847 | 847 | 847 | 847 | - |
