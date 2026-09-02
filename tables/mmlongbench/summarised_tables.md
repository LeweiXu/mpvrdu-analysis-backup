# Tables

The same tables as `all_tables.md`, condensed: verbose columns dropped, large cross-tabs cut to their own pooled rows, confidence intervals removed. Every table says what was dropped from it. 847 answerable questions over documents averaging 47.5 pages.

Every table changes ONE variable off the shared baseline below and holds the rest fixed; each caption states what it swept and what it pinned. G2 uses retrieved pages, G3 the unanswerable pool.

> **dataset**: mmlongbench · **scan**: any · **sampling**: full · **parser**: paddleocrvl · **reasoner_spec**: qwen3vl-8b-local · **quantization**: bf16 · **visual_resolution**: med · **representation**: T/TL/TLV/V · **pool**: answerable · **page_selection**: oracle · **prompt_mode**: none

## Representation

### Headline: cost-ordered ladder accuracy by doc_type (oracle pages)

> **swept**: representation ladder T/TL/TV/TLV/V

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | T | TL | TV | TLV | V | frontier | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 36.4 a5.2 w58.4 | 33.1 a1.9 w64.9 | 44.8 a0.0 w55.2 | 42.9 a1.3 w55.8 | 33.8 a0.6 w65.6 | T | 770 |
| Administration/Industry file | 50.0 a0.0 w50.0 | 56.2 a1.6 w42.2 | 67.2 a0.0 w32.8 | 67.2 a0.0 w32.8 | 54.7 a0.0 w45.3 | T | 320 |
| Brochure | 28.6 a3.9 w67.5 | 32.5 a3.9 w63.6 | 45.5 a0.0 w54.5 | 45.5 a0.0 w54.5 | 40.3 a0.0 w59.7 | TL | 385 |
| Financial report | 49.1 a0.9 w50.0 | 52.8 a0.9 w46.3 | 50.0 a0.9 w49.1 | 51.9 a0.9 w47.2 | 38.9 a1.9 w59.3 | T | 540 |
| Guidebook | 35.8 a7.5 w56.7 | 40.0 a1.7 w58.3 | 49.2 a2.5 w48.3 | 51.7 a2.5 w45.8 | 45.0 a0.8 w54.2 | T | 600 |
| Research report / Introduction | 22.6 a10.4 w67.0 | 27.4 a6.6 w66.0 | 46.7 a2.4 w50.9 | 47.6 a1.9 w50.5 | 45.3 a1.4 w53.3 | TV | 1060 |
| Tutorial/Workshop | 14.3 a17.0 w68.8 | 48.2 a2.7 w49.1 | 69.6 a2.7 w27.7 | 73.2 a1.8 w25.0 | 67.9 a1.8 w30.4 | TV | 560 |
| **all doc_types** | **31.9 a7.3 w60.8** | **38.8 a3.2 w58.0** | **51.6 a1.4 w47.0** | **52.5 a1.4 w46.0** | **45.6 a1.1 w53.4** | **TV** | **4235** |
| n (per col) | 847 | 847 | 847 | 847 | 847 | - | - |

### Fidelity: paired within-question verdict transitions by doc_type

> **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × doc_type · **pairing**: within-question, both rungs status==ok

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%)); confidence intervals removed. The full table is in `all_tables.md`._

| pairing | doc_type | wrong→right (%) | right→wrong (%) | paired n |
| --- | --- | --- | --- | --- |
| TL->TLV | Academic paper | 13.6 (21) | 3.9 (6) | 154 |
| TL->TLV | Administration/Industry file | 14.1 (9) | 3.1 (2) | 64 |
| TL->TLV | Brochure | 15.6 (12) | 2.6 (2) | 77 |
| TL->TLV | Financial report | 8.3 (9) | 9.3 (10) | 108 |
| TL->TLV | Guidebook | 13.3 (16) | 1.7 (2) | 120 |
| TL->TLV | Research report / Introduction | 24.5 (52) | 4.2 (9) | 212 |
| TL->TLV | Tutorial/Workshop | 26.8 (30) | 1.8 (2) | 112 |
| TL->TLV | **All doc_types** | 17.6 (149) | 3.9 (33) | 847 |
| T->TL | Academic paper | 5.2 (8) | 8.4 (13) | 154 |
| T->TL | Administration/Industry file | 14.1 (9) | 7.8 (5) | 64 |
| T->TL | Brochure | 9.1 (7) | 5.2 (4) | 77 |
| T->TL | Financial report | 13.0 (14) | 9.3 (10) | 108 |
| T->TL | Guidebook | 7.5 (9) | 3.3 (4) | 120 |
| T->TL | Research report / Introduction | 9.9 (21) | 5.2 (11) | 212 |
| T->TL | Tutorial/Workshop | 33.9 (38) | 0.0 (0) | 112 |
| T->TL | **All doc_types** | 12.5 (106) | 5.5 (47) | 847 |
| T->TLV | Academic paper | 13.6 (21) | 7.1 (11) | 154 |
| T->TLV | Administration/Industry file | 20.3 (13) | 3.1 (2) | 64 |
| T->TLV | Brochure | 22.1 (17) | 5.2 (4) | 77 |
| T->TLV | Financial report | 13.0 (14) | 10.2 (11) | 108 |
| T->TLV | Guidebook | 17.5 (21) | 1.7 (2) | 120 |
| T->TLV | Research report / Introduction | 29.7 (63) | 4.7 (10) | 212 |
| T->TLV | Tutorial/Workshop | 58.9 (66) | 0.0 (0) | 112 |
| T->TLV | **All doc_types** | 25.4 (215) | 4.7 (40) | 847 |
| T->TV | Academic paper | 12.3 (19) | 3.9 (6) | 154 |
| T->TV | Administration/Industry file | 18.8 (12) | 1.6 (1) | 64 |
| T->TV | Brochure | 19.5 (15) | 2.6 (2) | 77 |
| T->TV | Financial report | 11.1 (12) | 10.2 (11) | 108 |
| T->TV | Guidebook | 15.0 (18) | 1.7 (2) | 120 |
| T->TV | Research report / Introduction | 28.3 (60) | 4.2 (9) | 212 |
| T->TV | Tutorial/Workshop | 55.4 (62) | 0.0 (0) | 112 |
| T->TV | **All doc_types** | 23.4 (198) | 3.7 (31) | 847 |
| TV->TLV | Academic paper | 7.8 (12) | 9.7 (15) | 154 |
| TV->TLV | Administration/Industry file | 4.7 (3) | 4.7 (3) | 64 |
| TV->TLV | Brochure | 9.1 (7) | 9.1 (7) | 77 |
| TV->TLV | Financial report | 5.6 (6) | 3.7 (4) | 108 |
| TV->TLV | Guidebook | 5.0 (6) | 2.5 (3) | 120 |
| TV->TLV | Research report / Introduction | 7.1 (15) | 6.1 (13) | 212 |
| TV->TLV | Tutorial/Workshop | 8.0 (9) | 4.5 (5) | 112 |
| TV->TLV | **All doc_types** | 6.8 (58) | 5.9 (50) | 847 |
| n (per col) | TL->TLV: 847, T->TL: 847, T->TLV: 847, T->TV: 847, TV->TLV: 847 | - | - | - |

### Fidelity (overall): paired verdict transitions per rung pairing

> **view**: summary — pooled across all doc_types · **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × doc_type · **pairing**: within-question, both rungs status==ok

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%)); confidence intervals removed. The full table is in `all_tables.md`._

| pairing | wrong→right (%) | right→wrong (%) | paired n |
| --- | --- | --- | --- |
| TL->TLV | 17.6 (149) | 3.9 (33) | 847 |
| T->TL | 12.5 (106) | 5.5 (47) | 847 |
| T->TLV | 25.4 (215) | 4.7 (40) | 847 |
| T->TV | 23.4 (198) | 3.7 (31) | 847 |
| TV->TLV | 6.8 (58) | 5.9 (50) | 847 |
| n (per col) | - | - | - |

### Fidelity: paired within-question verdict transitions by evidence source

> **swept**: rung transition (TL→TLV, T→TL, T→TLV, T→TV, TV→TLV) × evidence source · **pairing**: within-question, both rungs status==ok · **All sources row**: pooled over questions, each counted once; not a column sum, has its own paired n

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%)); confidence intervals removed. The full table is in `all_tables.md`._

| pairing | evidence_source | wrong→right (%) | right→wrong (%) | paired n |
| --- | --- | --- | --- | --- |
| TL->TLV | (none) | 10.5 (2) | 0.0 (0) | 19 |
| TL->TLV | Chart | 29.8 (53) | 3.4 (6) | 178 |
| TL->TLV | Figure | 22.4 (65) | 1.4 (4) | 290 |
| TL->TLV | Generalized-text (Layout) | 16.9 (20) | 3.4 (4) | 118 |
| TL->TLV | Pure-text (Plain-text) | 10.3 (30) | 2.7 (8) | 291 |
| TL->TLV | Table | 7.8 (17) | 7.8 (17) | 217 |
| TL->TLV | **All sources** | 17.6 (149) | 3.9 (33) | 847 |
| T->TL | (none) | 10.5 (2) | 0.0 (0) | 19 |
| T->TL | Chart | 6.2 (11) | 5.6 (10) | 178 |
| T->TL | Figure | 13.4 (39) | 5.2 (15) | 290 |
| T->TL | Generalized-text (Layout) | 14.4 (17) | 5.1 (6) | 118 |
| T->TL | Pure-text (Plain-text) | 12.7 (37) | 4.1 (12) | 291 |
| T->TL | Table | 16.1 (35) | 8.3 (18) | 217 |
| T->TL | **All sources** | 12.5 (106) | 5.5 (47) | 847 |
| T->TLV | (none) | 21.1 (4) | 0.0 (0) | 19 |
| T->TLV | Chart | 30.9 (55) | 3.9 (7) | 178 |
| T->TLV | Figure | 33.1 (96) | 3.8 (11) | 290 |
| T->TLV | Generalized-text (Layout) | 28.8 (34) | 5.9 (7) | 118 |
| T->TLV | Pure-text (Plain-text) | 19.2 (56) | 3.1 (9) | 291 |
| T->TLV | Table | 18.0 (39) | 10.1 (22) | 217 |
| T->TLV | **All sources** | 25.4 (215) | 4.7 (40) | 847 |
| T->TV | (none) | 15.8 (3) | 0.0 (0) | 19 |
| T->TV | Chart | 26.4 (47) | 2.8 (5) | 178 |
| T->TV | Figure | 32.4 (94) | 2.4 (7) | 290 |
| T->TV | Generalized-text (Layout) | 25.4 (30) | 4.2 (5) | 118 |
| T->TV | Pure-text (Plain-text) | 17.5 (51) | 3.1 (9) | 291 |
| T->TV | Table | 15.2 (33) | 8.8 (19) | 217 |
| T->TV | **All sources** | 23.4 (198) | 3.7 (31) | 847 |
| TV->TLV | (none) | 5.3 (1) | 0.0 (0) | 19 |
| TV->TLV | Chart | 9.6 (17) | 6.2 (11) | 178 |
| TV->TLV | Figure | 7.6 (22) | 8.3 (24) | 290 |
| TV->TLV | Generalized-text (Layout) | 8.5 (10) | 6.8 (8) | 118 |
| TV->TLV | Pure-text (Plain-text) | 5.2 (15) | 3.4 (10) | 291 |
| TV->TLV | Table | 6.0 (13) | 4.6 (10) | 217 |
| TV->TLV | **All sources** | 6.8 (58) | 5.9 (50) | 847 |
| n (per col) | TL->TLV: 847, T->TL: 847, T->TLV: 847, T->TV: 847, TV->TLV: 847 | - | - | - |

### Composition: accuracy by evidence source and rung (appendix)

> **swept**: evidence source × rung

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | T | TL | TV | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| (none) | 52.6 a5.3 w42.1 | 63.2 a5.3 w31.6 | 68.4 a0.0 w31.6 | 73.7 a0.0 w26.3 | 52.6 a5.3 w42.1 | 95 |
| Chart | 18.5 a12.9 w68.5 | 19.1 a8.4 w72.5 | 42.1 a1.7 w56.2 | 45.5 a1.7 w52.8 | 43.3 a1.1 w55.6 | 890 |
| Figure | 15.5 a10.7 w73.8 | 23.8 a2.8 w73.4 | 45.5 a2.1 w52.4 | 44.8 a2.8 w52.4 | 40.3 a1.4 w58.3 | 1450 |
| Generalized-text (Layout) | 28.0 a1.7 w70.3 | 37.3 a4.2 w58.5 | 49.2 a0.8 w50.0 | 50.8 a0.0 w49.2 | 44.1 a0.8 w55.1 | 590 |
| Pure-text (Plain-text) | 39.2 a4.1 w56.7 | 47.8 a1.7 w50.5 | 53.6 a1.4 w45.0 | 55.3 a1.4 w43.3 | 44.3 a0.3 w55.3 | 1455 |
| Table | 40.6 a6.0 w53.5 | 48.4 a0.9 w50.7 | 47.0 a2.8 w50.2 | 48.4 a2.3 w49.3 | 37.8 a1.8 w60.4 | 1085 |
| n (per col) | 847 | 847 | 847 | 847 | 847 | - |

### Vision margin: paired bootstrap on best-image minus best-text, by doc_type

> **swept**: vision margin (best image rung − best text rung) × doc_type · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question across all five rungs; a question enters only if scored at every rung

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED (columns dropped: CI low, CI high, excludes 0); confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | Δ vision (points) | best image | best text | n (paired) |
| --- | --- | --- | --- | --- |
| Academic paper | +8.4 | TV | T | 154 |
| Administration/Industry file | +10.9 | TV | TL | 64 |
| Brochure | +13.0 | TV | TL | 77 |
| Financial report | -0.9 | TLV | TL | 108 |
| Guidebook | +11.7 | TLV | TL | 120 |
| Research report / Introduction | +20.3 | TLV | TL | 212 |
| Tutorial/Workshop | +25.0 | TLV | TL | 112 |
| all doc_types | +13.7 | TLV | TL | 847 |

### Vision margin: paired bootstrap on best-image minus best-text, by evidence source

> **swept**: vision margin (best image rung − best text rung) × evidence source · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question across all five rungs; a question enters only if scored at every rung

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED (columns dropped: CI low, CI high, excludes 0); confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | Δ vision (points) | best image | best text | n (paired) |
| --- | --- | --- | --- | --- |
| (none) | +10.5 | TLV | TL | 19 |
| Chart | +26.4 | TLV | TL | 178 |
| Figure | +21.7 | TV | TL | 290 |
| Generalized-text (Layout) | +13.6 | TLV | TL | 118 |
| Pure-text (Plain-text) | +7.6 | TLV | TL | 291 |
| Table | +0.0 | TLV | TL | 217 |
| All sources | +13.7 | TLV | TL | 847 |

### Parser comparison: TL/TLV accuracy by doc_type

> **swept**: parser (paddleocrvl / mineru / unlimited)

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | paddleocrvl TL | paddleocrvl TLV | mineru TL | mineru TLV | unlimited TL | unlimited TLV | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Academic paper | 35.1 | 39.6 | 19.5 | 35.1 | 39.0 | 40.9 | 154 |
| Administration/Industry file | 56.2 | 70.3 | 40.6 | 62.5 | 64.1 | 68.8 | 64 |
| Brochure | 32.5 | 41.6 | 16.9 | 40.3 | 36.4 | 49.4 | 77 |
| Financial report | 51.9 | 54.6 | 41.7 | 47.2 | 54.6 | 53.7 | 108 |
| Guidebook | 37.5 | 51.7 | 25.0 | 50.0 | 37.5 | 50.8 | 120 |
| Research report / Introduction | 26.9 | 48.1 | 19.8 | 45.3 | 26.9 | 50.5 | 212 |
| Tutorial/Workshop | 46.4 | 74.1 | 36.6 | 68.8 | 46.4 | 72.3 | 112 |
| n (per col) | 847 | 847 | 847 | 847 | 847 | 847 | - |

### Parser comparison (overall): TL/TLV accuracy per parser

> **view**: summary — pooled across all doc_types · **swept**: parser (paddleocrvl / mineru / unlimited)

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| parser | TL | TLV | n |
| --- | --- | --- | --- |
| paddleocrvl | 38.4 | 52.4 | 847 |
| mineru | 26.8 | 48.3 | 847 |
| unlimited | 40.4 | 53.4 | 847 |
| n (per col) | 2541 | 2541 | - |

### Parser fidelity by scan status: text-only vs text+vision, digital vs scanned

> **swept**: text source × scan status × (text-only / text+vision) · **delta column**: paired bootstrap on vision − text, not two marginals · **scanned pool**: 201 questions over 31 documents; the bootstrap resamples documents, so these intervals are wide

_A regroup of already-generated cells, not new inference: `scan_label` is a per-row covariate on every judged row (backfilled from annotations/auto_scan.csv), so this is the pooled parser comparison re-aggregated by scan class. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| text source (rungs) | digital: text-only | digital: text+vision | digital: Δ (vision − text) | scanned: text-only | scanned: text+vision | scanned: Δ (vision − text) |
| --- | --- | --- | --- | --- | --- | --- |
| PaddleOCR-VL (TL→TLV) | 40.1 (n=646) | 49.7 (n=646) | +9.6 | 32.8 (n=201) | 61.2 (n=201) | +28.4 |
| MinerU (TL→TLV) | 26.6 (n=646) | 46.0 (n=646) | +19.3 | 27.4 (n=201) | 55.7 (n=201) | +28.4 |
| Unlimited-OCR (TL→TLV) | 42.3 (n=646) | 50.2 (n=646) | +7.9 | 34.3 (n=201) | 63.7 (n=201) | +29.4 |
| PyMuPDF (raw embedded text) (T→TV) | 40.6 (n=646) | 49.7 (n=646) | +9.1 | 4.0 (n=201) | 57.7 (n=201) | +53.7 |
| **spread (max − min)** | 15.6 | 4.2 | 11.5 | 30.3 | 8.0 | 25.4 |

### Parser fidelity by evidence source and scan status: text-only vs text+vision

> **swept**: text source × evidence source × scan status × (text-only / text+vision) · **delta column**: paired bootstrap on vision − text, not two marginals · **transition columns**: paired within-question R→W / W→R across the vision step, on the same pairs as the delta · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **scanned pool**: 201 questions over 31 documents split five ways; most scanned per-source cells are thin and daggered

_The `parser_scan` table cut by evidence source. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| text source (rungs) | evidence_source | digital: text-only | digital: text+vision | digital: Δ (vision − text) | digital: R→W (%) | digital: W→R (%) | digital: paired n | scanned: text-only | scanned: text+vision | scanned: Δ (vision − text) | scanned: R→W (%) | scanned: W→R (%) | scanned: paired n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PaddleOCR-VL (TL→TLV) | Chart | 23.8 (n=130) | 40.8 (n=130) | +16.9 | 3.8 (5) | 20.8 (27) | 130 | 4.2 (n=48) | 54.2 (n=48) | +50.0 | 0.0 (0) | 50.0 (24) | 48 |
| PaddleOCR-VL (TL→TLV) | Figure | 17.4 (n=184) | 37.0 (n=184) | +19.6 | 1.6 (3) | 21.2 (39) | 184 | 31.1 (n=106) | 57.5 (n=106) | +26.4 | 0.9 (1) | 27.4 (29) | 106 |
| PaddleOCR-VL (TL→TLV) | Generalized-text (Layout) | 43.8 (n=80) | 47.5 (n=80) | +3.7 | 3.8 (3) | 7.5 (6) | 80 | 26.3 (n=38) | 57.9 (n=38) | +31.6 | 0.0 (0) | 31.6 (12) | 38 |
| PaddleOCR-VL (TL→TLV) | Pure-text (Plain-text) | 50.9 (n=226) | 54.9 (n=226) | +4.0 | 3.5 (8) | 7.5 (17) | 226 | 35.4 (n=65) | 55.4 (n=65) | +20.0 | 0.0 (0) | 20.0 (13) | 65 |
| PaddleOCR-VL (TL→TLV) | Table | 47.6 (n=185) | 46.5 (n=185) | -1.1 | 5.9 (11) | 4.9 (9) | 185 | 59.4 (n=32) | 71.9 (n=32) | +12.5 | 3.1 (1) | 15.6 (5) | 32 |
| PaddleOCR-VL (TL→TLV) | **All sources** | 40.1 (n=646) | 49.7 (n=646) | +9.6 | 3.7 (24) | 13.3 (86) | 646 | 32.8 (n=201) | 61.2 (n=201) | +28.4 | 1.0 (2) | 29.4 (59) | 201 |
| MinerU (TL→TLV) | Chart | 17.7 (n=130) | 38.5 (n=130) | +20.8 | 3.1 (4) | 23.8 (31) | 130 | 14.6 (n=48) | 47.9 (n=48) | +33.3 | 2.1 (1) | 35.4 (17) | 48 |
| MinerU (TL→TLV) | Figure | 12.5 (n=184) | 38.6 (n=184) | +26.1 | 1.6 (3) | 27.7 (51) | 184 | 25.5 (n=106) | 50.9 (n=106) | +25.5 | 1.9 (2) | 27.4 (29) | 106 |
| MinerU (TL→TLV) | Generalized-text (Layout) | 20.0 (n=80) | 43.8 (n=80) | +23.8 | 2.5 (2) | 26.2 (21) | 80 | 18.4 (n=38) | 50.0 (n=38) | +31.6 | 2.6 (1) | 34.2 (13) | 38 |
| MinerU (TL→TLV) | Pure-text (Plain-text) | 30.1 (n=226) | 49.1 (n=226) | +19.0 | 3.1 (7) | 22.1 (50) | 226 | 30.8 (n=65) | 53.8 (n=65) | +23.1 | 0.0 (0) | 23.1 (15) | 65 |
| MinerU (TL→TLV) | Table | 36.8 (n=185) | 42.7 (n=185) | +5.9 | 5.9 (11) | 11.9 (22) | 185 | 56.2 (n=32) | 65.6 (n=32) | +9.4 | 6.2 (2) | 15.6 (5) | 32 |
| MinerU (TL→TLV) | **All sources** | 26.6 (n=646) | 46.0 (n=646) | +19.3 | 3.4 (22) | 22.8 (147) | 646 | 27.4 (n=201) | 55.7 (n=201) | +28.4 | 2.0 (4) | 30.3 (61) | 201 |
| Unlimited-OCR (TL→TLV) | Chart | 23.8 (n=130) | 42.3 (n=130) | +18.5 | 3.8 (5) | 22.3 (29) | 130 | 2.1 (n=48) | 58.3 (n=48) | +56.2 | 0.0 (0) | 56.2 (27) | 48 |
| Unlimited-OCR (TL→TLV) | Figure | 20.7 (n=184) | 38.0 (n=184) | +17.4 | 2.7 (5) | 20.1 (37) | 184 | 34.0 (n=106) | 58.5 (n=106) | +24.5 | 0.9 (1) | 25.5 (27) | 106 |
| Unlimited-OCR (TL→TLV) | Generalized-text (Layout) | 43.8 (n=80) | 52.5 (n=80) | +8.8 | 2.5 (2) | 11.2 (9) | 80 | 36.8 (n=38) | 60.5 (n=38) | +23.7 | 0.0 (0) | 23.7 (9) | 38 |
| Unlimited-OCR (TL→TLV) | Pure-text (Plain-text) | 50.4 (n=226) | 53.1 (n=226) | +2.7 | 4.4 (10) | 7.1 (16) | 226 | 36.9 (n=65) | 56.9 (n=65) | +20.0 | 0.0 (0) | 20.0 (13) | 65 |
| Unlimited-OCR (TL→TLV) | Table | 49.7 (n=185) | 48.1 (n=185) | -1.6 | 6.5 (12) | 4.9 (9) | 185 | 59.4 (n=32) | 71.9 (n=32) | +12.5 | 6.2 (2) | 18.8 (6) | 32 |
| Unlimited-OCR (TL→TLV) | **All sources** | 42.3 (n=646) | 50.2 (n=646) | +7.9 | 4.6 (30) | 12.5 (81) | 646 | 34.3 (n=201) | 63.7 (n=201) | +29.4 | 1.5 (3) | 30.8 (62) | 201 |
| PyMuPDF (raw embedded text) (T→TV) | Chart | 24.6 (n=130) | 37.7 (n=130) | +13.1 | 3.8 (5) | 16.9 (22) | 130 | 0.0 (n=48) | 54.2 (n=48) | +54.2 | 0.0 (0) | 54.2 (26) | 48 |
| PyMuPDF (raw embedded text) (T→TV) | Figure | 19.6 (n=184) | 41.3 (n=184) | +21.7 | 3.3 (6) | 25.0 (46) | 184 | 7.5 (n=106) | 52.8 (n=106) | +45.3 | 0.9 (1) | 46.2 (49) | 106 |
| PyMuPDF (raw embedded text) (T→TV) | Generalized-text (Layout) | 40.0 (n=80) | 47.5 (n=80) | +7.5 | 3.8 (3) | 11.2 (9) | 80 | 2.6 (n=38) | 52.6 (n=38) | +50.0 | 2.6 (1) | 52.6 (20) | 38 |
| PyMuPDF (raw embedded text) (T→TV) | Pure-text (Plain-text) | 50.0 (n=226) | 54.4 (n=226) | +4.4 | 4.4 (10) | 8.8 (20) | 226 | 3.1 (n=65) | 50.8 (n=65) | +47.7 | 0.0 (0) | 47.7 (31) | 65 |
| PyMuPDF (raw embedded text) (T→TV) | Table | 48.1 (n=185) | 44.9 (n=185) | -3.2 | 10.3 (19) | 7.0 (13) | 185 | 0.0 (n=32) | 59.4 (n=32) | +59.4 | 0.0 (0) | 59.4 (19) | 32 |
| PyMuPDF (raw embedded text) (T→TV) | **All sources** | 40.6 (n=646) | 49.7 (n=646) | +9.1 | 4.8 (31) | 13.9 (90) | 646 | 4.0 (n=201) | 57.7 (n=201) | +53.7 | 0.5 (1) | 54.2 (109) | 201 |

### Resolution sweep: TLV/V accuracy by doc_type and preset

> **swept**: visual_resolution (low / med / high)

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | rung | low | med | high | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | TLV | 37.0 | 40.3 | 46.8 | 462 |
| Academic paper | V | 19.5 | 30.5 | 38.3 | 462 |
| Administration/Industry file | TLV | 64.1 | 68.8 | 70.3 | 192 |
| Administration/Industry file | V | 42.2 | 51.6 | 64.1 | 192 |
| Brochure | TLV | 40.3 | 42.9 | 48.1 | 231 |
| Brochure | V | 39.0 | 45.5 | 49.4 | 231 |
| Financial report | TLV | 54.6 | 52.8 | 53.7 | 324 |
| Financial report | V | 21.3 | 36.1 | 46.3 | 324 |
| Guidebook | TLV | 48.3 | 50.8 | 51.7 | 360 |
| Guidebook | V | 38.3 | 47.5 | 47.5 | 360 |
| Research report / Introduction | TLV | 42.9 | 49.5 | 50.0 | 636 |
| Research report / Introduction | V | 38.2 | 47.2 | 47.6 | 636 |
| Tutorial/Workshop | TLV | 71.4 | 74.1 | 74.1 | 336 |
| Tutorial/Workshop | V | 74.1 | 67.9 | 70.5 | 336 |
| **all doc_types** | **TLV** | **49.2** | **52.5** | **54.7** | **2541** |
| **all doc_types** | **V** | **37.8** | **45.7** | **50.2** | **2541** |
| n (per col) | - | 1694 | 1694 | 1694 | - |

### Resolution sweep: TLV/V accuracy by evidence source and preset

> **swept**: visual_resolution (low / med / high) × evidence source · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: does high resolution recover the pixel-limited sources (Chart, Figure) specifically, or lift every source alike

_Same sweep as the doc_type table, cut by the evidence modality a question draws on instead of by document class. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | rung | low | med | high | n |
| --- | --- | --- | --- | --- | --- |
| (none) | TLV | 63.2 (n=19) | 68.4 (n=19) | 73.7 (n=19) | 57 |
| (none) | V | 36.8 (n=19) | 47.4 (n=19) | 52.6 (n=19) | 57 |
| Chart | TLV | 38.2 (n=178) | 44.9 (n=178) | 48.3 (n=178) | 534 |
| Chart | V | 34.3 (n=178) | 44.9 (n=178) | 48.3 (n=178) | 534 |
| Figure | TLV | 39.7 (n=290) | 45.5 (n=290) | 48.3 (n=290) | 870 |
| Figure | V | 38.3 (n=290) | 40.0 (n=290) | 43.8 (n=290) | 870 |
| Generalized-text (Layout) | TLV | 46.6 (n=118) | 50.0 (n=118) | 54.2 (n=118) | 354 |
| Generalized-text (Layout) | V | 47.5 (n=118) | 49.2 (n=118) | 53.4 (n=118) | 354 |
| Pure-text (Plain-text) | TLV | 52.9 (n=291) | 55.0 (n=291) | 55.0 (n=291) | 873 |
| Pure-text (Plain-text) | V | 38.8 (n=291) | 45.4 (n=291) | 51.5 (n=291) | 873 |
| Table | TLV | 48.8 (n=217) | 49.8 (n=217) | 48.8 (n=217) | 651 |
| Table | V | 25.3 (n=217) | 37.3 (n=217) | 42.4 (n=217) | 651 |
| **All sources** | **TLV** | **49.2 (n=847)** | **52.5 (n=847)** | **54.7 (n=847)** | **2541** |
| **All sources** | **V** | **37.8 (n=847)** | **45.7 (n=847)** | **50.2 (n=847)** | **2541** |
| n (per col) | - | 1694 | 1694 | 1694 | - |

### Mined: ladder accuracy, scanned vs digital, by doc_type and rung

> **swept**: scan (digital vs scanned), all rungs

_oracle pages, primary reasoner. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | rung | digital | scanned | n_digital | n_scanned |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 39.0 | - | 154 | 0 |
| Academic paper | TL | 35.1 | - | 154 | 0 |
| Academic paper | TLV | 39.6 | - | 154 | 0 |
| Academic paper | V | 31.2 | - | 154 | 0 |
| Administration/Industry file | T | 60.4 | 0.0 | 53 | 11 |
| Administration/Industry file | TL | 56.6 | 54.5 | 53 | 11 |
| Administration/Industry file | TLV | 69.8 | 72.7 | 53 | 11 |
| Administration/Industry file | V | 49.1 | 54.5 | 53 | 11 |
| Brochure | T | 31.3 | 0.0 | 67 | 10 |
| Brochure | TL | 32.8 | 30.0 | 67 | 10 |
| Brochure | TLV | 40.3 | 50.0 | 67 | 10 |
| Brochure | V | 44.8 | 50.0 | 67 | 10 |
| Financial report | T | 50.0 | - | 108 | 0 |
| Financial report | TL | 51.9 | - | 108 | 0 |
| Financial report | TLV | 54.6 | - | 108 | 0 |
| Financial report | V | 36.1 | - | 108 | 0 |
| Guidebook | T | 38.2 | 0.0 | 110 | 10 |
| Guidebook | TL | 39.1 | 20.0 | 110 | 10 |
| Guidebook | TLV | 53.6 | 30.0 | 110 | 10 |
| Guidebook | V | 49.1 | 30.0 | 110 | 10 |
| Research report / Introduction | T | 34.4 | 1.2 | 131 | 81 |
| Research report / Introduction | TL | 32.8 | 17.3 | 131 | 81 |
| Research report / Introduction | TLV | 47.3 | 49.4 | 131 | 81 |
| Research report / Introduction | V | 42.7 | 50.6 | 131 | 81 |
| Tutorial/Workshop | T | 34.8 | 7.9 | 23 | 89 |
| Tutorial/Workshop | TL | 47.8 | 46.1 | 23 | 89 |
| Tutorial/Workshop | TLV | 69.6 | 75.3 | 23 | 89 |
| Tutorial/Workshop | V | 65.2 | 69.7 | 23 | 89 |
| **all doc_types** | **T** | **40.6** | **4.0** | **646** | **201** |
| **all doc_types** | **TL** | **40.1** | **32.8** | **646** | **201** |
| **all doc_types** | **TLV** | **49.7** | **61.2** | **646** | **201** |
| **all doc_types** | **V** | **41.5** | **58.2** | **646** | **201** |
| n (per col) | - | 2584 | 804 | - | - |

### Mined: ladder accuracy, scanned vs digital, by evidence source and rung

> **swept**: scan (digital vs scanned) × evidence source × rung · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **n**: per-cell n rides inline; a thin cell reads as survivorship, not robustness, so this is a trend table rather than a precision one

_Same digital/scanned split as the doc_type table, cut by the evidence modality a question draws on. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | rung | digital | scanned | n |
| --- | --- | --- | --- | --- |
| (none) | TL | 66.7 (n=18) | 0.0 (n=1) | 19 |
| (none) | TLV | 66.7 (n=18) | 100.0 (n=1) | 19 |
| (none) | V | 44.4 (n=18) | 100.0 (n=1) | 19 |
| Chart | TL | 23.8 (n=130) | 4.2 (n=48) | 178 |
| Chart | TLV | 40.8 (n=130) | 54.2 (n=48) | 178 |
| Chart | V | 41.5 (n=130) | 52.1 (n=48) | 178 |
| Figure | TL | 17.4 (n=184) | 31.1 (n=106) | 290 |
| Figure | TLV | 37.0 (n=184) | 57.5 (n=106) | 290 |
| Figure | V | 33.2 (n=184) | 52.8 (n=106) | 290 |
| Generalized-text (Layout) | TL | 43.8 (n=80) | 26.3 (n=38) | 118 |
| Generalized-text (Layout) | TLV | 47.5 (n=80) | 57.9 (n=38) | 118 |
| Generalized-text (Layout) | V | 47.5 (n=80) | 50.0 (n=38) | 118 |
| Pure-text (Plain-text) | TL | 50.9 (n=226) | 35.4 (n=65) | 291 |
| Pure-text (Plain-text) | TLV | 54.9 (n=226) | 55.4 (n=65) | 291 |
| Pure-text (Plain-text) | V | 42.5 (n=226) | 50.8 (n=65) | 291 |
| Table | TL | 47.6 (n=185) | 59.4 (n=32) | 217 |
| Table | TLV | 46.5 (n=185) | 71.9 (n=32) | 217 |
| Table | V | 32.4 (n=185) | 65.6 (n=32) | 217 |
| **All sources** | **TL** | **40.1 (n=646)** | **32.8 (n=201)** | **847** |
| **All sources** | **TLV** | **49.7 (n=646)** | **61.2 (n=201)** | **847** |
| **All sources** | **V** | **41.5 (n=646)** | **58.2 (n=201)** | **847** |
| n (per col) | - | 1938 | 603 | - |

## Selection

### Selection: sufficiency and robustness under constructed page sets

> **swept**: page_set condition (sufficiency / robustness) × ranking source × rung · **pivot**: all-gold row loaded from g1-representation-full (oracle, hop=multi) by the builder

_Rows group on the pageset condition grammar (ranking source, gold rule, distractor count); the robustness gold-count BLOCKS come from the corpus gold-page annotation (the +k design filters questions by exact gold count and feeds ALL their gold pages, so the block is a property of the question, not the rule). SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| condition | ranker | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- |
| **oracle (all gold, hop=multi)** | - | 25.4 (n=358) | 30.7 (n=358) | 38.0 (n=358) | 33.5 (n=358) | 1432 |
| drop bottom 1 | colqwen3 | 11.4 (n=352) | 13.4 (n=352) | 18.5 (n=352) | 15.1 (n=352) | 1408 |
| drop top 1 | colqwen3 | 10.8 (n=352) | 11.1 (n=352) | 15.9 (n=352) | 13.9 (n=352) | 1408 |
| keep bottom 1 | colqwen3 | 9.4 (n=352) | 9.7 (n=352) | 10.5 (n=352) | 9.9 (n=352) | 1408 |
| keep top 1 | colqwen3 | 9.1 (n=352) | 10.2 (n=352) | 12.8 (n=352) | 11.1 (n=352) | 1408 |
| **oracle (gold 1, d=0)** | - | 37.1 (n=480) | 44.6 (n=480) | 63.7 (n=480) | 55.0 (n=480) | 1920 |
| gold 1 + 1 distractors | colqwen3 | 39.5 (n=474) | 48.9 (n=474) | 63.7 (n=474) | 55.7 (n=474) | 1896 |
| gold 1 + 2 distractors | colqwen3 | 38.8 (n=474) | 47.9 (n=474) | 64.3 (n=474) | 56.1 (n=474) | 1896 |
| gold 1 + 3 distractors | colqwen3 | 40.9 (n=474) | 47.0 (n=474) | 63.1 (n=474) | 55.1 (n=474) | 1896 |
| gold 1 + 4 distractors | colqwen3 | - (n=0) | - (n=0) | 63.3 (n=313) | - (n=0) | 313 |
| gold 1 + 5 distractors | colqwen3 | - (n=0) | - (n=0) | 63.3 (n=256) | - (n=0) | 256 |
| gold 1 + 6 distractors | colqwen3 | - (n=0) | - (n=0) | 65.3 (n=196) | - (n=0) | 196 |
| **oracle (gold 2, d=0)** | - | 28.9 (n=246) | 33.3 (n=246) | 37.8 (n=246) | 34.6 (n=246) | 984 |
| gold 2 + 1 distractors | colqwen3 | 25.7 (n=241) | 34.0 (n=241) | 38.6 (n=241) | 34.4 (n=241) | 964 |
| gold 2 + 2 distractors | colqwen3 | 25.3 (n=241) | 33.6 (n=241) | 35.7 (n=241) | 32.4 (n=241) | 964 |
| gold 2 + 3 distractors | colqwen3 | 21.6 (n=241) | 28.2 (n=241) | 33.6 (n=241) | 33.2 (n=241) | 964 |
| gold 2 + 4 distractors | colqwen3 | - (n=0) | - (n=0) | 44.4 (n=117) | - (n=0) | 117 |
| gold 2 + 5 distractors | colqwen3 | - (n=0) | - (n=0) | 45.8 (n=83) | - (n=0) | 83 |
| **oracle (gold 3, d=0)** | - | 25.0 (n=40) | 30.0 (n=40) | 47.5 (n=40) | 42.5 (n=40) | 160 |
| gold 3 + 1 distractors | colqwen3 | 22.5 (n=40) | 40.0 (n=40) | 45.0 (n=40) | 40.0 (n=40) | 160 |
| gold 3 + 2 distractors | colqwen3 | 27.5 (n=40) | 37.5 (n=40) | 40.0 (n=40) | 30.0 (n=40) | 160 |
| gold 3 + 3 distractors | colqwen3 | 25.0 (n=40) | 35.0 (n=40) | 40.0 (n=40) | 32.5 (n=40) | 160 |
| n (per col) | - | 7346 | 7346 | 8311 | 7346 | - |

### Selection: paired within-question verdict transitions from the oracle page set

> **swept**: page_set transition (oracle → each sufficiency rule / +k distractors) × ranking source × rung · **pivot**: oracle cells loaded from g1-representation-full by the builder and paired per (question, rung) · **pairing**: within-question, oracle and perturbed page set both status==ok at that rung · **deep distractor counts**: the +4/+5/+6 columns come from g5c (TLV, colqwen3 only) and lose cells to OOM: paired n falls 474 -> 313 -> 256 -> 196 at gold 1. Attrition is nested, so a high-k cell is the surviving LIGHTEST questions and the slope across columns reads easier than it is. Compare down a column, not across one; the matched-set slope is selection_distractor_matched

_Paired on (question_id, rung) against the SAME question's oracle cell, loaded from the G1 cache: a question counts at a rung only when both the oracle and the perturbed page set produced a status==ok row there. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%); cut to the table's own pooled rows); confidence intervals removed. The full table is in `all_tables.md`._

| block | transition | ranker | rung | wrong→right (%) | right→wrong (%) | paired n |
| --- | --- | --- | --- | --- | --- | --- |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | **All rungs** | 2.7 (38) | 22.4 (316) | 1408 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | **All rungs** | 3.2 (45) | 21.1 (297) | 1408 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | **All rungs** | 2.9 (41) | 21.4 (302) | 1408 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | **All rungs** | 2.8 (39) | 22.3 (314) | 1408 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | **All rungs** | 2.1 (30) | 24.4 (344) | 1408 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | **All rungs** | 2.3 (32) | 24.9 (350) | 1408 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | **All rungs** | 2.0 (28) | 24.6 (347) | 1408 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | **All rungs** | 2.3 (32) | 23.9 (337) | 1408 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | **All rungs** | 6.3 (119) | 4.9 (93) | 1896 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | **All rungs** | 7.8 (147) | 6.5 (124) | 1896 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | **All rungs** | 6.9 (130) | 6.2 (118) | 1896 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | **All rungs** | 8.1 (154) | 7.1 (134) | 1896 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | **All rungs** | 7.8 (147) | 6.6 (126) | 1896 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | **All rungs** | 8.8 (167) | 8.0 (152) | 1896 |
| robustness (gold 1) | oracle -> +4 distractors | colqwen3 | **All rungs** | 6.7 (21) | 9.6 (30) | 313 |
| robustness (gold 1) | oracle -> +5 distractors | colqwen3 | **All rungs** | 7.0 (18) | 10.2 (26) | 256 |
| robustness (gold 1) | oracle -> +6 distractors | colqwen3 | **All rungs** | 8.2 (16) | 12.2 (24) | 196 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | **All rungs** | 6.8 (66) | 7.0 (67) | 964 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | **All rungs** | 6.6 (64) | 7.8 (75) | 964 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | **All rungs** | 6.6 (64) | 7.5 (72) | 964 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | **All rungs** | 7.0 (67) | 9.5 (92) | 964 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | **All rungs** | 7.8 (75) | 7.8 (75) | 964 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | **All rungs** | 5.7 (55) | 10.9 (105) | 964 |
| robustness (gold 2) | oracle -> +4 distractors | colqwen3 | **All rungs** | 12.0 (14) | 12.0 (14) | 117 |
| robustness (gold 2) | oracle -> +5 distractors | colqwen3 | **All rungs** | 8.4 (7) | 10.8 (9) | 83 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | **All rungs** | 6.2 (10) | 6.2 (10) | 160 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | **All rungs** | 8.1 (13) | 7.5 (12) | 160 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | **All rungs** | 10.0 (16) | 9.4 (15) | 160 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | **All rungs** | 5.0 (8) | 7.5 (12) | 160 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | **All rungs** | 6.9 (11) | 11.9 (19) | 160 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | **All rungs** | 5.6 (9) | 8.8 (14) | 160 |
| n (per col) | - | - | - | - | - | - |

### Selection: paired verdict transitions from the oracle page set, by evidence source

> **swept**: page_set transition (oracle → each sufficiency rule / +k distractors) × ranking source × evidence source · **pivot**: oracle cells loaded from g1-representation-full by the builder and paired per (question, rung) · **pairing**: within-question, oracle and perturbed page set both status==ok; pooled over the four rungs · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: does a dropped gold page or an added distractor cost text-carried and graphical evidence alike, or land on one of them

_Same pairing as the by-rung table (see it for the definition), POOLED over the rungs a condition ran: paired n counts (question, rung) cells and `questions` counts the distinct questions behind them, so paired n is about four times `questions` for the conditions that ran all four rungs. SUMMARISED (columns dropped: right→right (%), wrong→wrong (%); cut to the table's own pooled rows); confidence intervals removed. The full table is in `all_tables.md`._

| block | transition | ranker | evidence_source | wrong→right (%) | right→wrong (%) | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | bm25 | **All sources** | 2.7 (38) | 22.4 (316) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop bottom 1 | colqwen3 | **All sources** | 3.2 (45) | 21.1 (297) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | bm25 | **All sources** | 2.9 (41) | 21.4 (302) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> drop top 1 | colqwen3 | **All sources** | 2.8 (39) | 22.3 (314) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | bm25 | **All sources** | 2.1 (30) | 24.4 (344) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep bottom 1 | colqwen3 | **All sources** | 2.3 (32) | 24.9 (350) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | bm25 | **All sources** | 2.0 (28) | 24.6 (347) | 1408 | 352 |
| sufficiency (hop=multi) | oracle -> keep top 1 | colqwen3 | **All sources** | 2.3 (32) | 23.9 (337) | 1408 | 352 |
| robustness (gold 1) | oracle -> +1 distractor | bm25 | **All sources** | 6.3 (119) | 4.9 (93) | 1896 | 474 |
| robustness (gold 1) | oracle -> +1 distractor | colqwen3 | **All sources** | 7.8 (147) | 6.5 (124) | 1896 | 474 |
| robustness (gold 1) | oracle -> +2 distractors | bm25 | **All sources** | 6.9 (130) | 6.2 (118) | 1896 | 474 |
| robustness (gold 1) | oracle -> +2 distractors | colqwen3 | **All sources** | 8.1 (154) | 7.1 (134) | 1896 | 474 |
| robustness (gold 1) | oracle -> +3 distractors | bm25 | **All sources** | 7.8 (147) | 6.6 (126) | 1896 | 474 |
| robustness (gold 1) | oracle -> +3 distractors | colqwen3 | **All sources** | 8.8 (167) | 8.0 (152) | 1896 | 474 |
| robustness (gold 1) | oracle -> +4 distractors | colqwen3 | **All sources** | 6.7 (21) | 9.6 (30) | 313 | 313 |
| robustness (gold 1) | oracle -> +5 distractors | colqwen3 | **All sources** | 7.0 (18) | 10.2 (26) | 256 | 256 |
| robustness (gold 1) | oracle -> +6 distractors | colqwen3 | **All sources** | 8.2 (16) | 12.2 (24) | 196 | 196 |
| robustness (gold 2) | oracle -> +1 distractor | bm25 | **All sources** | 6.8 (66) | 7.0 (67) | 964 | 241 |
| robustness (gold 2) | oracle -> +1 distractor | colqwen3 | **All sources** | 6.6 (64) | 7.8 (75) | 964 | 241 |
| robustness (gold 2) | oracle -> +2 distractors | bm25 | **All sources** | 6.6 (64) | 7.5 (72) | 964 | 241 |
| robustness (gold 2) | oracle -> +2 distractors | colqwen3 | **All sources** | 7.0 (67) | 9.5 (92) | 964 | 241 |
| robustness (gold 2) | oracle -> +3 distractors | bm25 | **All sources** | 7.8 (75) | 7.8 (75) | 964 | 241 |
| robustness (gold 2) | oracle -> +3 distractors | colqwen3 | **All sources** | 5.7 (55) | 10.9 (105) | 964 | 241 |
| robustness (gold 2) | oracle -> +4 distractors | colqwen3 | **All sources** | 12.0 (14) | 12.0 (14) | 117 | 117 |
| robustness (gold 2) | oracle -> +5 distractors | colqwen3 | **All sources** | 8.4 (7) | 10.8 (9) | 83 | 83 |
| robustness (gold 3) | oracle -> +1 distractor | bm25 | **All sources** | 6.2 (10) | 6.2 (10) | 160 | 40 |
| robustness (gold 3) | oracle -> +1 distractor | colqwen3 | **All sources** | 8.1 (13) | 7.5 (12) | 160 | 40 |
| robustness (gold 3) | oracle -> +2 distractors | bm25 | **All sources** | 10.0 (16) | 9.4 (15) | 160 | 40 |
| robustness (gold 3) | oracle -> +2 distractors | colqwen3 | **All sources** | 5.0 (8) | 7.5 (12) | 160 | 40 |
| robustness (gold 3) | oracle -> +3 distractors | bm25 | **All sources** | 6.9 (11) | 11.9 (19) | 160 | 40 |
| robustness (gold 3) | oracle -> +3 distractors | colqwen3 | **All sources** | 5.6 (9) | 8.8 (14) | 160 | 40 |
| n (per col) | - | - | - | - | - | - | - |

### Withholding gold pages: verdict flips from the oracle page set, by evidence source

> **swept**: withheld/isolated gold page × evidence source (both flip directions) · **ranker**: colqwen3 only, matching the main text and figure · **pairing**: within-question against the oracle, pooled over the four rungs · **reading**: R→W is what the change breaks, W→R what it repairs; the pair is the whole effect

_Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: added distractor count × gold count × evidence source (both flip directions) · **ranker**: colqwen3 only, matching the main text and figure · **pairing**: within-question against the oracle, pooled over the four rungs · **blocks**: one block per gold-page count; each reads against its own d=0 oracle and blocks are not comparable · **deep distractor counts**: the +4/+5/+6 columns come from g5c (TLV, colqwen3 only) and lose cells to OOM: paired n falls 474 -> 313 -> 256 -> 196 at gold 1. Attrition is nested, so a high-k cell is the surviving LIGHTEST questions and the slope across columns reads easier than it is. Compare down a column, not across one; the matched-set slope is selection_distractor_matched

_Paired within-question against the same question's oracle cell at the TLV rung, so a cell counts questions where both sides produced an ok row there; ranking source is colqwen3. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| gold pages | evidence_source | +1 distractor R→W | +1 distractor W→R | +2 distractors R→W | +2 distractors W→R | +3 distractors R→W | +3 distractors W→R | +4 distractors R→W | +4 distractors W→R | +5 distractors R→W | +5 distractors W→R | +6 distractors R→W | +6 distractors W→R | paired n | questions |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 gold page | (none)† | 0.0 | 14.3 | 0.0 | 14.3 | 0.0 | 14.3 | 0.0 | 14.3 | 0.0 | 20.0 | 0.0 | 0.0 | 14 | 14 |
| 1 gold page | Chart | 9.3 | 7.2 | 10.3 | 9.3 | 17.5 | 8.2 | 12.0 | 8.4 | 17.6 | 6.8 | 20.8 | 7.5 | 97 | 97 |
| 1 gold page | Figure | 7.4 | 6.8 | 11.1 | 10.5 | 9.3 | 9.9 | 9.8 | 5.3 | 9.8 | 4.5 | 9.0 | 7.9 | 162 | 162 |
| 1 gold page | Generalized-text (Layout) | 10.7 | 5.4 | 8.9 | 7.1 | 7.1 | 3.6 | 10.2 | 0.0 | 12.8 | 2.6 | 19.4 | 2.8 | 56 | 56 |
| 1 gold page | Pure-text (Plain-text) | 7.2 | 6.5 | 5.9 | 5.9 | 7.2 | 5.9 | 5.7 | 6.9 | 4.5 | 7.5 | 6.0 | 10.0 | 153 | 153 |
| 1 gold page | Table | 8.7 | 4.8 | 5.8 | 3.8 | 6.7 | 6.7 | 8.6 | 5.7 | 0.0 | 8.7 | 6.7 | 0.0 | 104 | 104 |
| 1 gold page | **All sources** | 7.8 | 7.0 | 8.2 | 8.0 | 9.7 | 8.2 | 9.6 | 6.7 | 10.2 | 7.0 | 12.2 | 8.2 | 474 | 474 |
| 2-3 gold pages | (none)† | 0.0 | 25.0 | 0.0 | 25.0 | 0.0 | 25.0 | 0.0 | 100.0 | - | - | - | - | 4 | 4 |
| 2-3 gold pages | Chart | 4.9 | 8.2 | 6.6 | 4.9 | 9.8 | 8.2 | 11.1 | 19.4 | 20.0 | 20.0 | - | - | 61 | 61 |
| 2-3 gold pages | Figure | 7.1 | 9.4 | 8.2 | 5.9 | 10.6 | 2.4 | 6.2 | 6.2 | 4.9 | 0.0 | - | - | 85 | 85 |
| 2-3 gold pages | Generalized-text (Layout) | 5.1 | 7.7 | 15.4 | 2.6 | 20.5 | 7.7 | 24.0 | 8.0 | 15.8 | 0.0 | - | - | 39 | 39 |
| 2-3 gold pages | Pure-text (Plain-text) | 8.3 | 4.6 | 10.1 | 4.6 | 11.0 | 4.6 | 17.4 | 10.9 | 15.6 | 9.4 | - | - | 109 | 109 |
| 2-3 gold pages | Table | 7.8 | 7.8 | 6.8 | 4.9 | 8.7 | 4.9 | 15.8 | 5.3 | 0.0 | 10.0 | - | - | 103 | 103 |
| 2-3 gold pages | **All sources** | 7.8 | 7.5 | 9.6 | 6.0 | 11.4 | 6.0 | 12.0 | 12.0 | 10.8 | 8.4 | - | - | 281 | 281 |
| n (per col) | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |

### Adding distractor pages: dilution slope on the matched question set

> **swept**: added distractor count × gold count, on the question set surviving every count · **ranker**: colqwen3 only, matching the main text and figure · **rung**: TLV only · **pairing**: one fixed question set per gold block: answered at the oracle and at every distractor count the block ran · **reading**: this is the slope to quote. The per-condition distractor tables pair each count against the oracle separately, so their columns sit on different pools once OOM attrition starts

_The dilution slope on a FIXED question set. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| gold pages | condition | accuracy (%) | delta (pts) | matched n |
| --- | --- | --- | --- | --- |
| 1 gold page | oracle (d=0) | 69.4 | - | 196 |
| 1 gold page | +1 distractor | 68.4 | -1.0 | 196 |
| 1 gold page | +2 distractors | 65.8 | -3.6 | 196 |
| 1 gold page | +3 distractors | 67.3 | -2.0 | 196 |
| 1 gold page | +4 distractors | 66.3 | -3.1 | 196 |
| 1 gold page | +5 distractors | 65.3 | -4.1 | 196 |
| 1 gold page | +6 distractors | 65.3 | -4.1 | 196 |
| 2 gold pages | oracle (d=0) | 48.2 | - | 83 |
| 2 gold pages | +1 distractor | 48.2 | +0.0 | 83 |
| 2 gold pages | +2 distractors | 44.6 | -3.6 | 83 |
| 2 gold pages | +3 distractors | 41.0 | -7.2 | 83 |
| 2 gold pages | +4 distractors | 48.2 | +0.0 | 83 |
| 2 gold pages | +5 distractors | 45.8 | -2.4 | 83 |
| 3 gold pages | oracle (d=0) | 47.5 | - | 40 |
| 3 gold pages | +1 distractor | 45.0 | -2.5 | 40 |
| 3 gold pages | +2 distractors | 40.0 | -7.5 | 40 |
| 3 gold pages | +3 distractors | 40.0 | -7.5 | 40 |

### Retrieval accuracy (summary): best-F1 operating point per method

> **view**: summary — pooled across all doc_types · **swept**: retriever × k (page P/R/F1)

_best_k = the depth k with the highest mean F1 for that method (all doc_types). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: retriever × k (overall P/R/F1)

_ SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| retriever | modality | k | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 0.338 | 0.255 | 0.279 | 847 |
| bge-m3 | text | 5 | 0.147 | 0.482 | 0.212 | 847 |
| bge-m3 | text | 10 | 0.100 | 0.611 | 0.163 | 847 |
| bge-m3\|colqwen2.5 | joint | 1 | 0.485 | 0.552 | 0.486 | 847 |
| bge-m3\|colqwen2.5 | joint | 5 | 0.167 | 0.798 | 0.259 | 847 |
| bm25 | text | 1 | 0.295 | 0.222 | 0.242 | 847 |
| bm25 | text | 5 | 0.140 | 0.460 | 0.201 | 847 |
| bm25 | text | 10 | 0.095 | 0.585 | 0.154 | 847 |
| bm25\|colmodernvbert | joint | 1 | 0.442 | 0.512 | 0.445 | 847 |
| bm25\|colmodernvbert | joint | 5 | 0.159 | 0.776 | 0.248 | 847 |
| colmodernvbert | vision | 1 | 0.588 | 0.460 | 0.496 | 847 |
| colmodernvbert | vision | 5 | 0.227 | 0.725 | 0.322 | 847 |
| colmodernvbert | vision | 10 | 0.140 | 0.817 | 0.222 | 847 |
| colqwen2.5 | vision | 1 | 0.633 | 0.488 | 0.528 | 847 |
| colqwen2.5 | vision | 5 | 0.236 | 0.749 | 0.335 | 847 |
| colqwen2.5 | vision | 10 | 0.144 | 0.838 | 0.229 | 847 |
| colqwen3 | vision | 1 | 0.702 | 0.541 | 0.586 | 847 |
| colqwen3 | vision | 5 | 0.255 | 0.806 | 0.361 | 847 |
| colqwen3 | vision | 10 | 0.152 | 0.874 | 0.241 | 847 |
| n (per col) | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 at every depth, from the full rankings

> **swept**: retriever × k ∈ {1,3,5,7,10} (complete depth sweep, P/R/F1 as %) · **units**: PERCENTAGES, unlike the other retrieval tables · **provenance column**: measured = read off the side artifact; derived (union) = a joint arm rebuilt from its two constituents at the same depth, after the union rule is verified against every stored joint row

_P/R/F1 as PERCENTAGES (the other retrieval tables emit fractions), macro-averaged over the 847 answerable questions, one row per (retriever, k). SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| retriever | modality | k | P | R | F1 | n | provenance |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 33.8 | 25.5 | 27.9 | 847 | scored |
| bge-m3 | text | 5 | 14.7 | 48.2 | 21.2 | 847 | scored |
| bge-m3 | text | 10 | 10.0 | 61.1 | 16.3 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 1 | 48.5 | 55.2 | 48.6 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 5 | 16.7 | 79.8 | 25.9 | 847 | scored |
| bge-m3\|colqwen2.5 | joint | 10 | 10.7 | 87.5 | 17.9 | 847 | from ranking |
| bm25 | text | 1 | 29.5 | 22.2 | 24.2 | 847 | scored |
| bm25 | text | 5 | 14.0 | 46.0 | 20.1 | 847 | scored |
| bm25 | text | 10 | 9.5 | 58.5 | 15.4 | 847 | scored |
| bm25\|colmodernvbert | joint | 1 | 44.2 | 51.2 | 44.5 | 847 | scored |
| bm25\|colmodernvbert | joint | 5 | 15.9 | 77.6 | 24.8 | 847 | scored |
| bm25\|colmodernvbert | joint | 10 | 10.2 | 85.3 | 17.2 | 847 | from ranking |
| colmodernvbert | vision | 1 | 58.8 | 46.0 | 49.6 | 847 | scored |
| colmodernvbert | vision | 5 | 22.7 | 72.5 | 32.2 | 847 | scored |
| colmodernvbert | vision | 10 | 14.0 | 81.7 | 22.2 | 847 | scored |
| colqwen2.5 | vision | 1 | 63.3 | 48.8 | 52.8 | 847 | scored |
| colqwen2.5 | vision | 5 | 23.6 | 74.9 | 33.5 | 847 | scored |
| colqwen2.5 | vision | 10 | 14.4 | 83.8 | 22.9 | 847 | scored |
| colqwen3 | vision | 1 | 70.2 | 54.1 | 58.6 | 847 | scored |
| colqwen3 | vision | 5 | 25.5 | 80.6 | 36.1 | 847 | scored |
| colqwen3 | vision | 10 | 15.2 | 87.4 | 24.1 | 847 | scored |
| n (per col) | - | - | - | - | - | - | - |

### Retrieval accuracy: page P/R/F1 by method and render DPI

> **swept**: render dpi × retriever × k

_ SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| retriever | modality | k | dpi | P | R | F1 | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bge-m3 | text | 1 | 200 | 0.338 | 0.255 | 0.279 | 847 |
| bge-m3 | text | 5 | 200 | 0.147 | 0.482 | 0.212 | 847 |
| bge-m3 | text | 10 | 200 | 0.100 | 0.611 | 0.163 | 847 |
| bge-m3\|colqwen2.5 | joint | 1 | 200 | 0.485 | 0.552 | 0.486 | 847 |
| bge-m3\|colqwen2.5 | joint | 5 | 200 | 0.167 | 0.798 | 0.259 | 847 |
| bm25 | text | 1 | 200 | 0.295 | 0.222 | 0.242 | 847 |
| bm25 | text | 5 | 200 | 0.140 | 0.460 | 0.201 | 847 |
| bm25 | text | 10 | 200 | 0.095 | 0.585 | 0.154 | 847 |
| bm25\|colmodernvbert | joint | 1 | 200 | 0.442 | 0.512 | 0.445 | 847 |
| bm25\|colmodernvbert | joint | 5 | 200 | 0.159 | 0.776 | 0.248 | 847 |
| colmodernvbert | vision | 1 | 200 | 0.588 | 0.460 | 0.496 | 847 |
| colmodernvbert | vision | 5 | 200 | 0.227 | 0.725 | 0.322 | 847 |
| colmodernvbert | vision | 10 | 200 | 0.140 | 0.817 | 0.222 | 847 |
| colqwen2.5 | vision | 1 | 200 | 0.633 | 0.488 | 0.528 | 847 |
| colqwen2.5 | vision | 5 | 200 | 0.236 | 0.749 | 0.335 | 847 |
| colqwen2.5 | vision | 10 | 200 | 0.144 | 0.838 | 0.229 | 847 |
| colqwen3 | vision | 1 | 200 | 0.702 | 0.541 | 0.586 | 847 |
| colqwen3 | vision | 5 | 200 | 0.255 | 0.806 | 0.361 | 847 |
| colqwen3 | vision | 10 | 200 | 0.152 | 0.874 | 0.241 | 847 |
| n (per col) | - | - | - | - | - | - | - |

### Top-k sweep: accuracy vs retrieval depth by modality

> **swept**: retrieval depth k · **inference arms**: spec ran bge-m3 text / colqwen2.5 vision / joint; BASELINE captions the text arm as bm25 (the config default the spec overrode) — cite the spec · **status**: PROVISIONAL (partial G2 pool)

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| k | text | vision | joint | n |
| --- | --- | --- | --- | --- |
| 1 | 17.5 | 33.4 | 37.2 | 1824 |
| 3 | 23.6 | 38.8 | 39.1 | 1536 |
| 5 | 21.9 | 39.6 | 37.3 | 1057 |
| 7 | 42.9 | 28.6 | 50.0 | 18 |
| n (per col) | 1570 | 1584 | 1281 | - |

### Matched vs cross: accuracy by retrieval modality and doc_type (TLV)

> **swept**: retrieval modality (matched vs cross) · **inference arms**: spec ran bge-m3 text / colqwen2.5 vision / joint; BASELINE captions the text arm as bm25 (the config default the spec overrode) — cite the spec · **status**: PROVISIONAL (partial G2 pool)

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | text | vision | joint | n |
| --- | --- | --- | --- | --- |
| Academic paper | 14.6 | 20.1 | 22.3 | 591 |
| Administration/Industry file | 41.0 | 46.2 | 43.5 | 294 |
| Brochure | 19.4 | 26.7 | 28.1 | 383 |
| Financial report | 15.2 | 31.2 | 44.4 | 130 |
| Guidebook | 28.7 | 33.5 | 36.7 | 558 |
| Research report / Introduction | 15.4 | 36.9 | 36.6 | 1889 |
| Tutorial/Workshop | 29.2 | 60.2 | 63.2 | 590 |
| n (per col) | 1570 | 1584 | 1281 | - |

## Integration

### Integration: accuracy by evidence hop, per doc_type and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × rung · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 34.5 | 39.7 | +5.2 | 152 |
| Academic paper | TL | 29.8 | 38.2 | +8.5 | 152 |
| Academic paper | TV | 46.4 | 44.1 | -2.3 | 152 |
| Academic paper | TLV | 39.3 | 47.1 | +7.8 | 152 |
| Academic paper | V | 31.0 | 38.2 | +7.3 | 152 |
| Administration/Industry file | T | 58.5 | 40.0 | -18.5 | 61 |
| Administration/Industry file | TL | 68.3 | 40.0 | -28.3 | 61 |
| Administration/Industry file | TV | 80.5 | 50.0 | -30.5 | 61 |
| Administration/Industry file | TLV | 87.8 | 35.0 | -52.8 | 61 |
| Administration/Industry file | V | 68.3 | 35.0 | -33.3 | 61 |
| Brochure | T | 24.5 | 35.7 | +11.2 | 77 |
| Brochure | TL | 30.6 | 35.7 | +5.1 | 77 |
| Brochure | TV | 42.9 | 50.0 | +7.1 | 77 |
| Brochure | TLV | 51.0 | 35.7 | -15.3 | 77 |
| Brochure | V | 44.9 | 32.1 | -12.8 | 77 |
| Financial report | T | 60.3 | 34.1 | -26.2 | 107 |
| Financial report | TL | 68.3 | 31.8 | -36.4 | 107 |
| Financial report | TV | 71.4 | 20.5 | -51.0 | 107 |
| Financial report | TLV | 74.6 | 20.5 | -54.1 | 107 |
| Financial report | V | 52.4 | 20.5 | -31.9 | 107 |
| Guidebook | T | 42.5 | 25.5 | -16.9 | 120 |
| Guidebook | TL | 46.6 | 29.8 | -16.8 | 120 |
| Guidebook | TV | 56.2 | 38.3 | -17.9 | 120 |
| Guidebook | TLV | 60.3 | 38.3 | -22.0 | 120 |
| Guidebook | V | 53.4 | 31.9 | -21.5 | 120 |
| Research report / Introduction | T | 28.0 | 17.1 | -10.9 | 212 |
| Research report / Introduction | TL | 34.6 | 20.0 | -14.6 | 212 |
| Research report / Introduction | TV | 61.7 | 31.4 | -30.3 | 212 |
| Research report / Introduction | TLV | 64.5 | 30.5 | -34.0 | 212 |
| Research report / Introduction | V | 61.7 | 28.6 | -33.1 | 212 |
| Tutorial/Workshop | T | 23.8 | 0.0 | -23.8 | 109 |
| Tutorial/Workshop | TL | 54.0 | 41.3 | -12.7 | 109 |
| Tutorial/Workshop | TV | 84.1 | 52.2 | -32.0 | 109 |
| Tutorial/Workshop | TLV | 81.0 | 65.2 | -15.7 | 109 |
| Tutorial/Workshop | V | 81.0 | 52.2 | -28.8 | 109 |
| **all doc_types** | **T** | **37.3** | **25.1** | **-12.2** | **838** |
| **all doc_types** | **TL** | **45.0** | **31.3** | **-13.7** | **838** |
| **all doc_types** | **TV** | **62.1** | **38.5** | **-23.5** | **838** |
| **all doc_types** | **TLV** | **63.5** | **38.5** | **-25.0** | **838** |
| **all doc_types** | **V** | **55.2** | **33.5** | **-21.7** | **838** |
| n (per col) | - | 2400 | 1790 | - | - |

### Integration: accuracy by evidence hop, per evidence source and rung (oracle pages)

> **swept**: evidence hop (single vs multi) × evidence source × rung · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Built on the COMPLETE answerable pool: all 847 answerable questions at every rung with no OOM attrition. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | rung | single | multi | M − S | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 (n=14) | 20.0 (n=5) | -44.3 | 19 |
| (none) | TL | 78.6 (n=14) | 20.0 (n=5) | -58.6 | 19 |
| (none) | TV | 85.7 (n=14) | 20.0 (n=5) | -65.7 | 19 |
| (none) | TLV | 92.9 (n=14) | 20.0 (n=5) | -72.9 | 19 |
| (none) | V | 64.3 (n=14) | 20.0 (n=5) | -44.3 | 19 |
| Chart | T | 20.4 (n=98) | 16.5 (n=79) | -4.0 | 177 |
| Chart | TL | 19.4 (n=98) | 19.0 (n=79) | -0.4 | 177 |
| Chart | TV | 53.1 (n=98) | 29.1 (n=79) | -23.9 | 177 |
| Chart | TLV | 56.1 (n=98) | 32.9 (n=79) | -23.2 | 177 |
| Chart | V | 54.1 (n=98) | 30.4 (n=79) | -23.7 | 177 |
| Figure | T | 19.3 (n=166) | 10.1 (n=119) | -9.2 | 285 |
| Figure | TL | 25.3 (n=166) | 21.8 (n=119) | -3.5 | 285 |
| Figure | TV | 50.6 (n=166) | 39.5 (n=119) | -11.1 | 285 |
| Figure | TLV | 49.4 (n=166) | 39.5 (n=119) | -9.9 | 285 |
| Figure | V | 45.8 (n=166) | 33.6 (n=119) | -12.2 | 285 |
| Generalized-text (Layout) | T | 30.4 (n=56) | 26.7 (n=60) | -3.7 | 116 |
| Generalized-text (Layout) | TL | 44.6 (n=56) | 31.7 (n=60) | -13.0 | 116 |
| Generalized-text (Layout) | TV | 60.7 (n=56) | 40.0 (n=60) | -20.7 | 116 |
| Generalized-text (Layout) | TLV | 66.1 (n=56) | 38.3 (n=60) | -27.7 | 116 |
| Generalized-text (Layout) | V | 55.4 (n=56) | 35.0 (n=60) | -20.4 | 116 |
| Pure-text (Plain-text) | T | 46.8 (n=154) | 31.3 (n=134) | -15.4 | 288 |
| Pure-text (Plain-text) | TL | 56.5 (n=154) | 38.8 (n=134) | -17.7 | 288 |
| Pure-text (Plain-text) | TV | 64.3 (n=154) | 42.5 (n=134) | -21.7 | 288 |
| Pure-text (Plain-text) | TLV | 67.5 (n=154) | 42.5 (n=134) | -25.0 | 288 |
| Pure-text (Plain-text) | V | 53.9 (n=154) | 34.3 (n=134) | -19.6 | 288 |
| Table | T | 47.1 (n=104) | 35.5 (n=110) | -11.7 | 214 |
| Table | TL | 66.3 (n=104) | 32.7 (n=110) | -33.6 | 214 |
| Table | TV | 66.3 (n=104) | 30.0 (n=110) | -36.3 | 214 |
| Table | TLV | 66.3 (n=104) | 31.8 (n=110) | -34.5 | 214 |
| Table | V | 51.9 (n=104) | 25.5 (n=110) | -26.5 | 214 |
| **All sources** | **T** | **37.3 (n=480)** | **25.1 (n=358)** | **-12.2** | **838** |
| **All sources** | **TL** | **45.0 (n=480)** | **31.3 (n=358)** | **-13.7** | **838** |
| **All sources** | **TV** | **62.1 (n=480)** | **38.5 (n=358)** | **-23.5** | **838** |
| **All sources** | **TLV** | **63.5 (n=480)** | **38.5 (n=358)** | **-25.0** | **838** |
| **All sources** | **V** | **55.2 (n=480)** | **33.5 (n=358)** | **-21.7** | **838** |
| n (per col) | - | 2400 | 1790 | - | - |

### Integration detail: accuracy by gold evidence-page count and rung (oracle pages)

> **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence pages | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| 1 | 37.1 a9.2 w53.8 (n=480) | 44.6 a5.2 w50.2 (n=480) | 63.7 a1.0 w35.2 (n=480) | 55.0 a1.2 w43.8 (n=480) | 1920 |
| 2 | 28.9 a7.7 w63.4 (n=246) | 33.3 a4.9 w61.8 (n=246) | 37.8 a2.4 w59.8 (n=246) | 34.6 a2.0 w63.4 (n=246) | 984 |
| 3 | 25.0 a7.5 w67.5 (n=40) | 30.0 a2.5 w67.5 (n=40) | 47.5 a0.0 w52.5 (n=40) | 42.5 a2.5 w55.0 (n=40) | 160 |
| 4-5 | 13.9 a8.3 w77.8 (n=36) | 25.0 a2.8 w72.2 (n=36) | 44.4 a2.8 w52.8 (n=36) | 36.1 a2.8 w61.1 (n=36) | 144 |
| 6+ | 13.9 a2.8 w83.3 (n=36) | 19.4 a0.0 w80.6 (n=36) | 22.2 a0.0 w77.8 (n=36) | 13.9 a0.0 w86.1 (n=36) | 144 |
| n (per col) | 838 | 838 | 838 | 838 | - |

### Integration detail (overall): how each rung degrades with evidence-page count

> **view**: summary — pooled across all doc_types · **swept**: hop_bucket (1 / 2 / 3 / 4-5 / 6+) × rung · **hop**: bucketed evidence-page count, zero-evidence questions dropped · **tail buckets**: 4-5 and 6+ are small; included for trend, not precision

_Rows are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` itself is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | 1 | 2 | 3 | 4-5 | 6+ | 1 → 6+ | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 37.1 (n=480) | 28.9 (n=246) | 25.0 (n=40) | 13.9 (n=36) | 13.9 (n=36) | -23.2 | 838 |
| TL | 44.6 (n=480) | 33.3 (n=246) | 30.0 (n=40) | 25.0 (n=36) | 19.4 (n=36) | -25.1 | 838 |
| TLV | 63.7 (n=480) | 37.8 (n=246) | 47.5 (n=40) | 44.4 (n=36) | 22.2 (n=36) | -41.5 | 838 |
| V | 55.0 (n=480) | 34.6 (n=246) | 42.5 (n=40) | 36.1 (n=36) | 13.9 (n=36) | -41.1 | 838 |
| n (per col) | 1920 | 984 | 160 | 144 | 144 | - | - |

### Integration cross-tab: accuracy by doc_type, rung, and evidence-page bucket (oracle pages)

> **swept**: doc_type × rung × evidence-page bucket (1 / 2 / 3+) · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail

_Buckets are the number of gold evidence pages the question cites, taken from the corpus annotation that `hop` is derived from (NOT from `page_indices`, which for a no-gold-page question carries a stand-in page and would misbucket it); zero-evidence questions are dropped. 3+ merges the finer 3 / 4-5 / 6+ buckets of the integration-detail table. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| doc_type | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| Academic paper | T | 36.9 (n=84) | 45.8 (n=48) | 35.0 (n=20) | 152 |
| Academic paper | TL | 32.1 (n=84) | 43.8 (n=48) | 30.0 (n=20) | 152 |
| Academic paper | TLV | 38.1 (n=84) | 37.5 (n=48) | 50.0 (n=20) | 152 |
| Academic paper | V | 29.8 (n=84) | 33.3 (n=48) | 35.0 (n=20) | 152 |
| Administration/Industry file | T | 58.5 (n=41) | 18.2 (n=11) | 66.7 (n=9) | 61 |
| Administration/Industry file | TL | 68.3 (n=41) | 27.3 (n=11) | 55.6 (n=9) | 61 |
| Administration/Industry file | TLV | 85.4 (n=41) | 45.5 (n=11) | 55.6 (n=9) | 61 |
| Administration/Industry file | V | 65.9 (n=41) | 18.2 (n=11) | 33.3 (n=9) | 61 |
| Brochure | T | 22.4 (n=49) | 47.1 (n=17) | 18.2 (n=11) | 77 |
| Brochure | TL | 30.6 (n=49) | 35.3 (n=17) | 36.4 (n=11) | 77 |
| Brochure | TLV | 44.9 (n=49) | 23.5 (n=17) | 54.5 (n=11) | 77 |
| Brochure | V | 44.9 (n=49) | 47.1 (n=17) | 45.5 (n=11) | 77 |
| Financial report | T | 60.3 (n=63) | 36.6 (n=41) | 33.3 (n=3) | 107 |
| Financial report | TL | 68.3 (n=63) | 31.7 (n=41) | 0.0 (n=3) | 107 |
| Financial report | TLV | 76.2 (n=63) | 26.8 (n=41) | 0.0 (n=3) | 107 |
| Financial report | V | 47.6 (n=63) | 22.0 (n=41) | 0.0 (n=3) | 107 |
| Guidebook | T | 41.1 (n=73) | 37.5 (n=32) | 0.0 (n=15) | 120 |
| Guidebook | TL | 45.2 (n=73) | 34.4 (n=32) | 6.7 (n=15) | 120 |
| Guidebook | TLV | 58.9 (n=73) | 43.8 (n=32) | 33.3 (n=15) | 120 |
| Guidebook | V | 54.8 (n=73) | 37.5 (n=32) | 33.3 (n=15) | 120 |
| Research report / Introduction | T | 28.0 (n=107) | 17.1 (n=70) | 11.4 (n=35) | 212 |
| Research report / Introduction | TL | 32.7 (n=107) | 24.3 (n=70) | 14.3 (n=35) | 212 |
| Research report / Introduction | TLV | 67.3 (n=107) | 34.3 (n=70) | 17.1 (n=35) | 212 |
| Research report / Introduction | V | 64.5 (n=107) | 30.0 (n=70) | 20.0 (n=35) | 212 |
| Tutorial/Workshop | T | 22.2 (n=63) | 0.0 (n=27) | 0.0 (n=19) | 109 |
| Tutorial/Workshop | TL | 52.4 (n=63) | 40.7 (n=27) | 36.8 (n=19) | 109 |
| Tutorial/Workshop | TLV | 85.7 (n=63) | 63.0 (n=27) | 57.9 (n=19) | 109 |
| Tutorial/Workshop | V | 81.0 (n=63) | 63.0 (n=27) | 42.1 (n=19) | 109 |
| **All** | T | 37.1 (n=480) | 28.9 (n=246) | 17.9 (n=112) | 838 |
| **All** | TL | 44.6 (n=480) | 33.3 (n=246) | 25.0 (n=112) | 838 |
| **All** | TLV | 63.7 (n=480) | 37.8 (n=246) | 38.4 (n=112) | 838 |
| **All** | V | 55.0 (n=480) | 34.6 (n=246) | 31.2 (n=112) | 838 |
| n (per col) | - | 1920 | 984 | 448 | - |

### Integration cross-tab: accuracy by evidence source, rung, and evidence-page bucket (oracle pages)

> **swept**: evidence source × rung × evidence-page bucket (1 / 2 / 3+) · **buckets**: gold evidence-page count from the corpus annotation, zero-evidence questions dropped; 3+ merges the detail table's 3 / 4-5 / 6+ tail · **multi-source questions**: counted once in every source they cite, so the blocks overlap; the All rows pool each question once and are not a column sum

_The evidence-source companion to the doc_type integration cross-tab: same buckets, same rungs, the modality a question draws on replacing the document class. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | rung | 1 | 2 | 3+ | n |
| --- | --- | --- | --- | --- | --- |
| (none) | T | 64.3 (n=14) | 0.0 (n=4) | 100.0 (n=1) | 19 |
| (none) | TL | 78.6 (n=14) | 0.0 (n=4) | 100.0 (n=1) | 19 |
| (none) | TLV | 85.7 (n=14) | 0.0 (n=4) | 100.0 (n=1) | 19 |
| (none) | V | 57.1 (n=14) | 0.0 (n=4) | 100.0 (n=1) | 19 |
| Chart | T | 20.4 (n=98) | 18.6 (n=59) | 5.0 (n=20) | 177 |
| Chart | TL | 17.3 (n=98) | 22.0 (n=59) | 15.0 (n=20) | 177 |
| Chart | TLV | 58.2 (n=98) | 32.2 (n=59) | 15.0 (n=20) | 177 |
| Chart | V | 57.1 (n=98) | 33.9 (n=59) | 15.0 (n=20) | 177 |
| Figure | T | 18.1 (n=166) | 12.9 (n=70) | 8.2 (n=49) | 285 |
| Figure | TL | 24.7 (n=166) | 20.0 (n=70) | 18.4 (n=49) | 285 |
| Figure | TLV | 49.4 (n=166) | 34.3 (n=70) | 44.9 (n=49) | 285 |
| Figure | V | 45.2 (n=166) | 37.1 (n=70) | 30.6 (n=49) | 285 |
| Generalized-text (Layout) | T | 33.9 (n=56) | 32.4 (n=34) | 11.5 (n=26) | 116 |
| Generalized-text (Layout) | TL | 48.2 (n=56) | 35.3 (n=34) | 23.1 (n=26) | 116 |
| Generalized-text (Layout) | TLV | 64.3 (n=56) | 44.1 (n=34) | 34.6 (n=26) | 116 |
| Generalized-text (Layout) | V | 62.5 (n=56) | 41.2 (n=34) | 30.8 (n=26) | 116 |
| Pure-text (Plain-text) | T | 46.8 (n=154) | 35.1 (n=94) | 25.0 (n=40) | 288 |
| Pure-text (Plain-text) | TL | 55.8 (n=154) | 41.5 (n=94) | 32.5 (n=40) | 288 |
| Pure-text (Plain-text) | TLV | 66.2 (n=154) | 44.7 (n=94) | 40.0 (n=40) | 288 |
| Pure-text (Plain-text) | V | 55.8 (n=154) | 30.9 (n=94) | 35.0 (n=40) | 288 |
| Table | T | 49.0 (n=104) | 32.7 (n=98) | 50.0 (n=12) | 214 |
| Table | TL | 67.3 (n=104) | 34.7 (n=98) | 25.0 (n=12) | 214 |
| Table | TLV | 69.2 (n=104) | 31.6 (n=98) | 41.7 (n=12) | 214 |
| Table | V | 51.0 (n=104) | 25.5 (n=98) | 25.0 (n=12) | 214 |
| **All** | T | 37.1 (n=480) | 28.9 (n=246) | 17.9 (n=112) | 838 |
| **All** | TL | 44.6 (n=480) | 33.3 (n=246) | 25.0 (n=112) | 838 |
| **All** | TLV | 63.7 (n=480) | 37.8 (n=246) | 38.4 (n=112) | 838 |
| **All** | V | 55.0 (n=480) | 34.6 (n=246) | 31.2 (n=112) | 838 |
| n (per col) | - | 1920 | 984 | 448 | - |

### Integration: accuracy by evidence hop for the TLV vs TLVi ordering pair

> **swept**: evidence hop (single vs multi) × page ordering (TLV vs TLVi) · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse)

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| ordering | single | multi | M − S | n |
| --- | --- | --- | --- | --- |
| TLV | 64.0 | 38.5 | -25.4 | 838 |
| TLVi | 65.4 | 41.9 | -23.5 | 838 |
| n (per col) | 960 | 716 | - | - |

## Faithfulness

### Faithfulness: answerable accuracy by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **anchor**: the none row reproduces the G1 headline ladder 31.9 / 39.4 / 56.8 / 45.9; drift is flagged in the note

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 31.9 (n=847) a7.3 w60.8 | 38.8 (n=847) a3.2 w58.0 | 52.5 (n=847) a1.4 w46.0 ⚠ | 45.6 (n=847) a1.1 w53.4 |
| grounded | 26.8 (n=847) a9.6 w63.6 | 34.4 (n=847) a1.3 w64.3 | 45.7 (n=847) a0.8 w53.5 | 39.9 (n=847) a0.6 w59.5 |
| abstain | 23.3 (n=847) a52.2 w24.6 | 29.3 (n=847) a47.1 w23.6 | 41.4 (n=847) a27.4 w31.2 | 33.5 (n=847) a32.5 w34.0 |
| abstain_balanced | 23.8 (n=847) a47.8 w28.3 | 30.0 (n=847) a42.9 w27.2 | 42.6 (n=847) a22.9 w34.5 | 35.2 (n=847) a27.7 w37.1 |
| cot | 29.5 (n=847) a2.8 w67.7 | 36.0 (n=847) a4.1 w59.9 | 53.1 (n=847) a1.1 w45.8 | 49.7 (n=847) a0.4 w49.9 |
| extract_cot | 28.0 (n=847) a2.4 w69.7 | 36.5 (n=847) a5.7 w57.9 | 50.2 (n=846) a2.0 w47.8 | 44.4 (n=847) a2.4 w53.2 |
| n (per col) | 5082 | 5082 | 5081 | 5082 |

### Faithfulness: answerable abstention rate by prompt mode and rung (oracle pages)

> **swept**: prompt_mode × rung (answerable pool, oracle pages) · **direction**: abstaining is an error only where the RUNG carried the evidence; read the d component, not the pooled rate

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_mode | T | TL | TLV | V |
| --- | --- | --- | --- | --- |
| none | 7.4 (n=847) 3.2d/22.1s | 3.3 (n=847) 2.3d/6.8s | 1.7 (n=847) 1.4d/2.6s | 1.1 (n=847) 0.8d/2.1s |
| grounded | 9.6 (n=847) 2.1d/35.3s | 1.3 (n=847) 1.2d/1.6s | 0.8 (n=847) 0.6d/1.6s | 0.6 (n=847) 0.5d/1.1s |
| abstain | 52.2 (n=847) 38.4d/100.0s | 47.1 (n=847) 44.1d/57.4s | 27.4 (n=847) 29.7d/19.5s | 32.5 (n=847) 35.5d/22.1s |
| abstain_balanced | 47.8 (n=847) 32.7d/100.0s | 42.9 (n=847) 39.6d/54.2s | 22.9 (n=847) 25.3d/14.7s | 27.7 (n=847) 30.1d/19.5s |
| cot | 2.8 (n=847) 2.0d/5.8s | 4.3 (n=847) 3.2d/7.9s | 1.1 (n=847) 1.4d/0.0s | 0.4 (n=847) 0.5d/0.0s |
| extract_cot | 2.5 (n=847) 2.4d/2.6s | 5.7 (n=847) 4.4d/10.0s | 2.1 (n=846) 1.7d/3.7s | 2.4 (n=847) 2.7d/1.1s |
| n (per col) | 5082 | 5082 | 5081 | 5082 |

### Faithfulness: unanswerable abstention rate by prompt mode and rung (bm25 k=3 pages)

> **swept**: prompt_mode × rung (unanswerable pool, bm25 k=3 pages) · **direction**: abstaining is CORRECT here; higher is better · **anchor**: grounded ≈ 10.7 and abstain ≈ 80.7 (legacy generic/targeted)

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: prompt_mode × evidence source × rung (answerable pool, oracle pages) · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Chart | 18.5 (n=178) a12.9 w68.5 | 19.1 (n=178) a8.4 w72.5 | 45.5 (n=178) a1.7 w52.8 | 43.3 (n=178) a1.1 w55.6 |
| none | Figure | 15.5 (n=290) a10.7 w73.8 | 23.8 (n=290) a2.8 w73.4 | 44.8 (n=290) a2.8 w52.4 | 40.3 (n=290) a1.4 w58.3 |
| none | Generalized-text (Layout) | 28.0 (n=118) a1.7 w70.3 | 37.3 (n=118) a4.2 w58.5 | 50.8 (n=118) a0.0 w49.2 | 44.1 (n=118) a0.8 w55.1 |
| none | Pure-text (Plain-text) | 39.2 (n=291) a4.1 w56.7 | 47.8 (n=291) a1.7 w50.5 | 55.3 (n=291) a1.4 w43.3 | 44.3 (n=291) a0.3 w55.3 |
| none | Table | 40.6 (n=217) a6.0 w53.5 | 48.4 (n=217) a0.9 w50.7 | 48.4 (n=217) a2.3 w49.3 | 37.8 (n=217) a1.8 w60.4 |
| none | (none) | 52.6 (n=19) a5.3 w42.1† | 63.2 (n=19) a5.3 w31.6† | 73.7 (n=19) a0.0 w26.3† | 52.6 (n=19) a5.3 w42.1† |
| none | **All sources** | 31.9 (n=847) a7.3 w60.8 | 38.8 (n=847) a3.2 w58.0 | 52.5 (n=847) a1.4 w46.0 | 45.6 (n=847) a1.1 w53.4 |
| grounded | Chart | 16.3 (n=178) a16.9 w66.9 | 16.3 (n=178) a2.8 w80.9 | 33.7 (n=178) a1.1 w65.2 | 31.5 (n=178) a0.6 w68.0 |
| grounded | Figure | 12.1 (n=290) a10.3 w77.6 | 22.4 (n=290) a0.3 w77.2 | 42.4 (n=290) a0.7 w56.9 | 39.3 (n=290) a1.0 w59.7 |
| grounded | Generalized-text (Layout) | 18.6 (n=118) a7.6 w73.7 | 29.7 (n=118) a0.8 w69.5 | 42.4 (n=118) a0.0 w57.6 | 44.9 (n=118) a0.0 w55.1 |
| grounded | Pure-text (Plain-text) | 37.8 (n=291) a6.5 w55.7 | 45.0 (n=291) a0.7 w54.3 | 51.2 (n=291) a1.0 w47.8 | 41.6 (n=291) a0.7 w57.7 |
| grounded | Table | 29.5 (n=217) a10.1 w60.4 | 39.2 (n=217) a1.4 w59.4 | 40.1 (n=217) a0.9 w59.0 | 30.9 (n=217) a0.0 w69.1 |
| grounded | (none) | 42.1 (n=19) a0.0 w57.9† | 57.9 (n=19) a0.0 w42.1† | 52.6 (n=19) a0.0 w47.4† | 42.1 (n=19) a0.0 w57.9† |
| grounded | **All sources** | 26.8 (n=847) a9.6 w63.6 | 34.4 (n=847) a1.3 w64.3 | 45.7 (n=847) a0.8 w53.5 | 39.9 (n=847) a0.6 w59.5 |
| abstain | Chart | 13.5 (n=178) a52.2 w34.3 | 12.4 (n=178) a59.0 w28.7 | 28.7 (n=178) a25.3 w46.1 | 26.4 (n=178) a27.5 w46.1 |
| abstain | Figure | 7.2 (n=290) a76.2 w16.6 | 14.1 (n=290) a65.2 w20.7 | 34.5 (n=290) a35.2 w30.3 | 31.0 (n=290) a38.3 w30.7 |
| abstain | Generalized-text (Layout) | 19.5 (n=118) a55.9 w24.6 | 25.4 (n=118) a44.1 w30.5 | 41.5 (n=118) a19.5 w39.0 | 37.3 (n=118) a25.4 w37.3 |
| abstain | Pure-text (Plain-text) | 34.0 (n=291) a41.9 w24.1 | 40.5 (n=291) a35.4 w24.1 | 45.7 (n=291) a23.7 w30.6 | 36.1 (n=291) a30.9 w33.0 |
| abstain | Table | 26.3 (n=217) a42.4 w31.3 | 38.2 (n=217) a36.4 w25.3 | 39.2 (n=217) a30.0 w30.9 | 26.7 (n=217) a39.6 w33.6 |
| abstain | (none) | 36.8 (n=19) a36.8 w26.3† | 52.6 (n=19) a31.6 w15.8† | 57.9 (n=19) a26.3 w15.8† | 42.1 (n=19) a36.8 w21.1† |
| abstain | **All sources** | 23.3 (n=847) a52.2 w24.6 | 29.3 (n=847) a47.1 w23.6 | 41.4 (n=847) a27.4 w31.2 | 33.5 (n=847) a32.5 w34.0 |
| abstain_balanced | Chart | 14.0 (n=178) a44.9 w41.0 | 12.9 (n=178) a51.7 w35.4 | 30.9 (n=178) a18.5 w50.6 | 25.8 (n=178) a24.2 w50.0 |
| abstain_balanced | Figure | 7.9 (n=290) a71.7 w20.3 | 14.5 (n=290) a62.1 w23.4 | 36.2 (n=290) a31.0 w32.8 | 33.4 (n=290) a33.1 w33.4 |
| abstain_balanced | Generalized-text (Layout) | 19.5 (n=118) a52.5 w28.0 | 28.8 (n=118) a41.5 w29.7 | 41.5 (n=118) a18.6 w39.8 | 39.0 (n=118) a21.2 w39.8 |
| abstain_balanced | Pure-text (Plain-text) | 33.7 (n=291) a39.5 w26.8 | 39.5 (n=291) a32.6 w27.8 | 47.4 (n=291) a18.9 w33.7 | 36.4 (n=291) a25.4 w38.1 |
| abstain_balanced | Table | 26.3 (n=217) a37.8 w35.9 | 37.8 (n=217) a30.0 w32.3 | 37.3 (n=217) a25.3 w37.3 | 30.0 (n=217) a34.6 w35.5 |
| abstain_balanced | (none) | 42.1 (n=19) a26.3 w31.6† | 57.9 (n=19) a31.6 w10.5† | 63.2 (n=19) a21.1 w15.8† | 42.1 (n=19) a31.6 w26.3† |
| abstain_balanced | **All sources** | 23.8 (n=847) a47.8 w28.3 | 30.0 (n=847) a42.9 w27.2 | 42.6 (n=847) a22.9 w34.5 | 35.2 (n=847) a27.7 w37.1 |
| cot | Chart | 21.3 (n=178) a3.9 w74.7 | 16.9 (n=178) a13.5 w69.7 | 45.5 (n=178) a1.1 w53.4 | 44.4 (n=178) a1.1 w54.5 |
| cot | Figure | 11.7 (n=290) a1.7 w86.6 | 18.3 (n=290) a2.1 w79.7 | 45.2 (n=290) a0.3 w54.5 | 44.8 (n=290) a0.0 w55.2 |
| cot | Generalized-text (Layout) | 24.6 (n=118) a0.0 w75.4 | 37.3 (n=118) a2.5 w60.2 | 50.0 (n=118) a0.8 w49.2 | 55.9 (n=118) a0.0 w44.1 |
| cot | Pure-text (Plain-text) | 34.7 (n=291) a4.1 w61.2 | 45.0 (n=291) a3.1 w51.9 | 54.6 (n=291) a1.0 w44.3 | 48.1 (n=291) a0.7 w51.2 |
| cot | Table | 40.6 (n=217) a3.2 w56.2 | 51.2 (n=217) a2.8 w46.1 | 55.3 (n=217) a2.3 w42.4 | 47.5 (n=217) a0.0 w52.5 |
| cot | (none) | 42.1 (n=19) a10.5 w47.4† | 57.9 (n=19) a5.3 w36.8† | 63.2 (n=19) a5.3 w31.6† | 52.6 (n=19) a0.0 w47.4† |
| cot | **All sources** | 29.5 (n=847) a2.8 w67.7 | 36.0 (n=847) a4.1 w59.9 | 53.1 (n=847) a1.1 w45.8 | 49.7 (n=847) a0.4 w49.9 |
| extract_cot | Chart | 13.5 (n=178) a5.1 w81.5 | 17.4 (n=178) a14.0 w68.5 | 39.3 (n=178) a2.2 w58.4 | 38.8 (n=178) a2.2 w59.0 |
| extract_cot | Figure | 10.7 (n=290) a2.1 w87.2 | 21.0 (n=290) a4.1 w74.8 | 44.1 (n=290) a0.7 w55.2 | 41.7 (n=290) a1.4 w56.9 |
| extract_cot | Generalized-text (Layout) | 20.3 (n=118) a1.7 w78.0 | 37.3 (n=118) a3.4 w59.3 | 50.8 (n=118) a0.8 w48.3 | 52.5 (n=118) a1.7 w45.8 |
| extract_cot | Pure-text (Plain-text) | 37.5 (n=291) a1.4 w61.2 | 45.0 (n=291) a3.4 w51.5 | 51.7 (n=290) a2.4 w45.9 | 44.3 (n=291) a3.1 w52.6 |
| extract_cot | Table | 41.5 (n=217) a1.8 w56.7 | 49.8 (n=217) a4.1 w46.1 | 52.5 (n=217) a4.6 w42.9 | 39.6 (n=217) a5.1 w55.3 |
| extract_cot | (none) | 31.6 (n=19) a5.3 w63.2† | 52.6 (n=19) a5.3 w42.1† | 57.9 (n=19) a10.5 w31.6† | 42.1 (n=19) a5.3 w52.6† |
| extract_cot | **All sources** | 28.0 (n=847) a2.4 w69.7 | 36.5 (n=847) a5.7 w57.9 | 50.2 (n=846) a2.0 w47.8 | 44.4 (n=847) a2.4 w53.2 |
| n (per col) | - | - | - | - | - |

### Faithfulness: answerable abstention rate by prompt mode, evidence source and rung

> **swept**: prompt_mode × evidence source × rung (answerable pool, oracle pages) · **direction**: abstaining is an error only where the RUNG carried the evidence; read the d component, not the pooled rate · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_mode | evidence_source | T | TL | TLV | V |
| --- | --- | --- | --- | --- | --- |
| none | Chart | 12.9 (n=178) 3.8d/37.5s | 8.4 (n=178) 5.4d/16.7s | 2.8 (n=178) 1.5d/6.2s | 1.1 (n=178) 0.0d/4.2s |
| none | Figure | 10.7 (n=290) 6.9d/17.8s | 2.8 (n=290) 2.1d/4.0s | 2.8 (n=290) 3.2d/2.0s | 1.4 (n=290) 1.1d/2.0s |
| none | Generalized-text (Layout) | 2.5 (n=118) 2.4d/2.9s | 4.2 (n=118) 1.2d/11.8s | 0.0 (n=118) 0.0d/0.0s | 0.8 (n=118) 0.0d/2.9s |
| none | Pure-text (Plain-text) | 4.5 (n=291) 1.7d/15.0s | 1.7 (n=291) 0.4d/6.7s | 1.7 (n=291) 1.3d/3.3s | 0.3 (n=291) 0.0d/1.7s |
| none | Table | 6.0 (n=217) 1.6d/33.3s | 1.4 (n=217) 1.1d/3.3s | 2.3 (n=217) 1.6d/6.7s | 1.8 (n=217) 1.1d/6.7s |
| none | (none) | 5.3 (n=19) 0.0d/100.0s† | 5.3 (n=19) 5.6d/0.0s† | 0.0 (n=19) 0.0d/0.0s† | 5.3 (n=19) 5.6d/0.0s† |
| none | **All sources** | 7.4 (n=847) 3.2d/22.1s | 3.3 (n=847) 2.3d/6.8s | 1.7 (n=847) 1.4d/2.6s | 1.1 (n=847) 0.8d/2.1s |
| grounded | Chart | 16.9 (n=178) 3.8d/52.1s | 2.8 (n=178) 2.3d/4.2s | 1.1 (n=178) 0.0d/4.2s | 0.6 (n=178) 0.0d/2.1s |
| grounded | Figure | 10.3 (n=290) 2.6d/24.8s | 0.3 (n=290) 0.5d/0.0s | 0.7 (n=290) 0.5d/1.0s | 1.0 (n=290) 1.1d/1.0s |
| grounded | Generalized-text (Layout) | 7.6 (n=118) 0.0d/26.5s | 0.8 (n=118) 0.0d/2.9s | 0.0 (n=118) 0.0d/0.0s | 0.0 (n=118) 0.0d/0.0s |
| grounded | Pure-text (Plain-text) | 6.5 (n=291) 1.7d/25.0s | 0.7 (n=291) 0.4d/1.7s | 1.0 (n=291) 0.4d/3.3s | 0.7 (n=291) 0.4d/1.7s |
| grounded | Table | 10.1 (n=217) 1.1d/66.7s | 1.4 (n=217) 1.6d/0.0s | 0.9 (n=217) 1.1d/0.0s | 0.0 (n=217) 0.0d/0.0s |
| grounded | (none) | 0.0 (n=19) 0.0d/0.0s† | 0.0 (n=19) 0.0d/0.0s† | 0.0 (n=19) 0.0d/0.0s† | 0.0 (n=19) 0.0d/0.0s† |
| grounded | **All sources** | 9.6 (n=847) 2.1d/35.3s | 1.3 (n=847) 1.2d/1.6s | 0.8 (n=847) 0.6d/1.6s | 0.6 (n=847) 0.5d/1.1s |
| abstain | Chart | 52.2 (n=178) 34.6d/100.0s | 59.0 (n=178) 49.2d/85.4s | 25.3 (n=178) 22.3d/33.3s | 27.5 (n=178) 26.9d/29.2s |
| abstain | Figure | 76.2 (n=290) 63.5d/100.0s | 65.2 (n=290) 68.8d/58.4s | 35.2 (n=290) 45.5d/15.8s | 38.3 (n=290) 48.1d/19.8s |
| abstain | Generalized-text (Layout) | 55.9 (n=118) 38.1d/100.0s | 44.1 (n=118) 39.3d/55.9s | 19.5 (n=118) 23.8d/8.8s | 25.4 (n=118) 27.4d/20.6s |
| abstain | Pure-text (Plain-text) | 41.9 (n=291) 26.8d/100.0s | 35.4 (n=291) 29.9d/56.7s | 23.7 (n=291) 22.1d/30.0s | 30.9 (n=291) 28.6d/40.0s |
| abstain | Table | 42.4 (n=217) 33.2d/100.0s | 36.4 (n=217) 36.4d/36.7s | 30.0 (n=217) 32.6d/13.3s | 39.6 (n=217) 42.2d/23.3s |
| abstain | (none) | 36.8 (n=19) 33.3d/100.0s† | 31.6 (n=19) 27.8d/100.0s† | 26.3 (n=19) 27.8d/0.0s† | 36.8 (n=19) 38.9d/0.0s† |
| abstain | **All sources** | 52.2 (n=847) 38.4d/100.0s | 47.1 (n=847) 44.1d/57.4s | 27.4 (n=847) 29.7d/19.5s | 32.5 (n=847) 35.5d/22.1s |
| abstain_balanced | Chart | 44.9 (n=178) 24.6d/100.0s | 51.7 (n=178) 41.5d/79.2s | 18.5 (n=178) 15.4d/27.1s | 24.2 (n=178) 22.3d/29.2s |
| abstain_balanced | Figure | 71.7 (n=290) 56.6d/100.0s | 62.1 (n=290) 65.6d/55.4s | 31.0 (n=290) 41.8d/10.9s | 33.1 (n=290) 42.3d/15.8s |
| abstain_balanced | Generalized-text (Layout) | 52.5 (n=118) 33.3d/100.0s | 41.5 (n=118) 36.9d/52.9s | 18.6 (n=118) 25.0d/2.9s | 21.2 (n=118) 21.4d/20.6s |
| abstain_balanced | Pure-text (Plain-text) | 39.5 (n=291) 23.8d/100.0s | 32.6 (n=291) 26.4d/56.7s | 18.9 (n=291) 17.7d/23.3s | 25.4 (n=291) 23.4d/33.3s |
| abstain_balanced | Table | 37.8 (n=217) 27.8d/100.0s | 30.0 (n=217) 30.5d/26.7s | 25.3 (n=217) 27.3d/13.3s | 34.6 (n=217) 36.9d/20.0s |
| abstain_balanced | (none) | 26.3 (n=19) 22.2d/100.0s† | 31.6 (n=19) 27.8d/100.0s† | 21.1 (n=19) 22.2d/0.0s† | 31.6 (n=19) 33.3d/0.0s† |
| abstain_balanced | **All sources** | 47.8 (n=847) 32.7d/100.0s | 42.9 (n=847) 39.6d/54.2s | 22.9 (n=847) 25.3d/14.7s | 27.7 (n=847) 30.1d/19.5s |
| cot | Chart | 3.9 (n=178) 3.1d/6.2s | 13.5 (n=178) 10.0d/22.9s | 1.1 (n=178) 1.5d/0.0s | 1.1 (n=178) 1.5d/0.0s |
| cot | Figure | 1.7 (n=290) 1.1d/3.0s | 2.4 (n=290) 1.6d/4.0s | 0.3 (n=290) 0.5d/0.0s | 0.0 (n=290) 0.0d/0.0s |
| cot | Generalized-text (Layout) | 0.0 (n=118) 0.0d/0.0s | 3.4 (n=118) 2.4d/5.9s | 0.8 (n=118) 1.2d/0.0s | 0.0 (n=118) 0.0d/0.0s |
| cot | Pure-text (Plain-text) | 4.1 (n=291) 2.6d/10.0s | 3.1 (n=291) 2.2d/6.7s | 1.0 (n=291) 1.3d/0.0s | 0.7 (n=291) 0.9d/0.0s |
| cot | Table | 3.2 (n=217) 1.6d/13.3s | 2.8 (n=217) 1.6d/10.0s | 2.3 (n=217) 2.7d/0.0s | 0.0 (n=217) 0.0d/0.0s |
| cot | (none) | 10.5 (n=19) 11.1d/0.0s† | 5.3 (n=19) 5.6d/0.0s† | 5.3 (n=19) 5.6d/0.0s† | 0.0 (n=19) 0.0d/0.0s† |
| cot | **All sources** | 2.8 (n=847) 2.0d/5.8s | 4.3 (n=847) 3.2d/7.9s | 1.1 (n=847) 1.4d/0.0s | 0.4 (n=847) 0.5d/0.0s |
| extract_cot | Chart | 5.6 (n=178) 5.4d/6.2s | 14.0 (n=178) 10.0d/25.0s | 2.2 (n=178) 0.8d/6.2s | 2.2 (n=178) 2.3d/2.1s |
| extract_cot | Figure | 2.1 (n=290) 2.6d/1.0s | 4.1 (n=290) 3.2d/5.9s | 1.0 (n=290) 1.1d/1.0s | 1.4 (n=290) 1.6d/1.0s |
| extract_cot | Generalized-text (Layout) | 1.7 (n=118) 2.4d/0.0s | 3.4 (n=118) 1.2d/8.8s | 0.8 (n=118) 0.0d/2.9s | 1.7 (n=118) 2.4d/0.0s |
| extract_cot | Pure-text (Plain-text) | 1.4 (n=291) 0.9d/3.3s | 3.4 (n=291) 2.2d/8.3s | 2.4 (n=290) 1.3d/6.7s | 3.1 (n=291) 3.5d/1.7s |
| extract_cot | Table | 1.8 (n=217) 1.6d/3.3s | 4.1 (n=217) 3.2d/10.0s | 4.6 (n=217) 3.2d/13.3s | 5.1 (n=217) 4.8d/6.7s |
| extract_cot | (none) | 5.3 (n=19) 5.6d/0.0s† | 5.3 (n=19) 5.6d/0.0s† | 10.5 (n=19) 11.1d/0.0s† | 5.3 (n=19) 5.6d/0.0s† |
| extract_cot | **All sources** | 2.5 (n=847) 2.4d/2.6s | 5.7 (n=847) 4.4d/10.0s | 2.1 (n=846) 1.7d/3.7s | 2.4 (n=847) 2.7d/1.1s |
| n (per col) | - | - | - | - | - |

### Faithfulness: unanswerable abstention rate by prompt mode, evidence source and rung

> **swept**: prompt_mode × evidence source × rung (unanswerable pool, bm25 k=3 pages) · **⚠ not usable per source**: an unanswerable question has no gold evidence pages, so the pool is essentially unlabelled; see the note · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once

_Pins: paddleocrvl, qwen3vl-8b-local, bf16, med resolution, decode budget 256 default and 2048 for cot/extract_cot, delimiter "Answer:". SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: prompt_mode transition (none→abstain, none→abstain_balanced) × rung (answerable pool, oracle pages) · **pairing**: within-question at one rung, both modes status==ok; only the instruction changes, pages are the oracle set on both sides · **R→W split**: `as refusal` vs `as wrong answer` sum to R→W, so the table separates what the instruction refuses from what it merely gets wrong · **net column**: W→R − R→W in points, i.e. the mode's accuracy change against the uninstructed prompt

_Paired on question_id at one rung: a question counts only when BOTH prompt modes produced a status==ok row there, so every rate is a within-question flip and not two marginal accuracies read against each other. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: prompt_mode (none / generic / targeted; legacy names of the six-mode set) · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_condition | abstention_rate | answered | n |
| --- | --- | --- | --- |
| none | 17.1 | 809 | 976 |
| generic | 10.3 | 875 | 976 |
| targeted | 79.4 | 201 | 976 |
| n (per col) | - | - | - |

### Mined: abstention rate on unanswerable questions by prompt mode and doc_type

> **swept**: prompt_mode × doc_type · **page_selection note**: described as similarity (bm25, k=3); rows are emitted under base retrieved_text_k3 with provenance=retrieved

_ SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: abstention detection scope (extracted answer vs whole generation) · **delimiter**: Answer: (configured by the faithfulness specs)

_Same judged rows, two detection scopes. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: reasoner block (precision / scale / matched budget / family / reasoning variant) · **memory**: weight footprint, not peak VRAM · **note**: the reasoning-variant arm is loaded by the builder from g6-thinking under G6_reasoning (TLV only), since a plan entry names one task

_Weight footprint (MB, `~` = derived for quantized variants) replaces peak VRAM: the measured figure is device-0 only. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| block | model_spec | weights_mb | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| precision | qwen3vl-8b-local | 17534 | 31.9 (n=847) | 38.4 (n=847) | 52.4 (n=847) | 45.5 (n=847) | 3388 |
| precision | qwen3vl-8b-local-8bit | 10285~ | 32.5 (n=847) | 37.9 (n=847) | 53.6 (n=847) | 45.7 (n=847) | 3388 |
| precision | qwen3vl-8b-local-4bit | 6775~ | 31.8 (n=847) | 39.4 (n=847) | 51.8 (n=847) | 45.5 (n=847) | 3388 |
| scale | qwen3vl-2b-local | 4255 | 24.7 (n=847) | 31.9 (n=847) | 38.3 (n=847) | 31.9 (n=847) | 3388 |
| scale | qwen3vl-4b-local | 8876 | 32.3 (n=847) | 38.6 (n=847) | 50.4 (n=847) | 42.4 (n=847) | 3388 |
| scale | qwen3vl-8b-local | 17534 | 31.9 (n=847) | 38.4 (n=847) | 52.4 (n=847) | 45.5 (n=847) | 3388 |
| scale | qwen3vl-32b-local | 66715 | 35.5 (n=847) | 43.9 (n=847) | 59.6 (n=846) | 56.7 (n=847) | 3387 |
| matched budget (~17 GB) | qwen3vl-8b-local | 17534 | 31.9 (n=847) | 38.4 (n=847) | 52.4 (n=847) | 45.5 (n=847) | 3388 |
| matched budget (~17 GB) | qwen3vl-32b-local-4bit | 19951~ | 37.0 (n=847) | 42.1 (n=847) | 59.1 (n=847) | 52.3 (n=847) | 3388 |
| scale (Gemma-3) | gemma3-4b-local | 8600 | 22.1 (n=846) | 30.4 (n=843) | 39.9 (n=828) | 33.8 (n=829) | 3346 |
| scale (Gemma-3) | gemma3-12b-local | 24375 | 30.4 (n=840) | 37.5 (n=802) | 50.9 (n=737) | 42.6 (n=775) | 3154 |
| family | qwen3vl-8b-local | 17534 | 31.9 (n=847) | 38.4 (n=847) | 52.4 (n=847) | 45.5 (n=847) | 3388 |
| family | internvl3-8b-local | 15889 | 19.3 (n=845) | 25.3 (n=842) | 32.6 (n=807) | 24.1 (n=845) | 3339 |
| family | glm4v-9b-local | 20586 | 27.4 (n=839) | 33.6 (n=800) | 44.3 (n=783) | 31.0 (n=845) | 3267 |
| family | minicpmv-8b-local | 17392 | 30.8 (n=814) | 37.9 (n=730) | 61.9 (n=640) | 53.8 (n=809) | 2993 |
| reasoning variant (M−S) | qwen3vl-8b-local | 17534 | -11.7 (nS=480, nM=358) | -13.9 (nS=480, nM=358) | -25.8 (nS=480, nM=358) | -21.5 (nS=480, nM=358) | 3388 |
| reasoning variant (M−S) | qwen3vl-8b-thinking-local | 17534 | - | - | -9.1 (nS=474, nM=252) | - | 735 |
| n (per col) | - | - | 10113 | 9946 | 10458 | 10032 | - |

### Reasoner scale vs evidence hop: accuracy by gold evidence-page bucket, per rung

> **swept**: reasoner size × gold evidence-page bucket × rung · **multi**: cumulative: two or more gold pages, pooling the 2 and 3+ columns · **reading**: does scale close the M−S deficit, or lift both hop buckets together · **note**: each size loads its own run_tags in the builder

_Accuracy on oracle pages, bucketed by the number of gold evidence pages the question cites (from the corpus annotation, not from `page_indices`). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: reasoner_spec (size + family) · **note**: 8b bf16 baseline from the representation run

_latency_ms is end-to-end and decode-inflated (~20x by the verbose-answer change); prefill_ms is the clean cost signal, and reads `-` for a backend that cannot measure a prefill/decode split. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| model_spec | T | TL | TLV | V | weights_mb | peak_vram_mb | prefill_ms | latency_ms | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| internvl3-8b-local | 19.3 | 25.3 | 32.6 | 24.1 | 15889 | 64151 | - | 5196 | 3339 |
| qwen3vl-2b-local | 24.7 | 31.9 | 38.3 | 31.9 | 4255 | 14264 | 17992 | 23760 | 3388 |
| qwen3vl-4b-local | 32.3 | 38.6 | 50.4 | 42.4 | 8876 | 17266 | 17365 | 24123 | 3388 |
| qwen3vl-8b-local | 31.9 | 38.4 | 52.4 | 45.5 | 17534 | 26995 | 13488 | 19844 | 3388 |
| n (per col) | 3386 | 3383 | 3348 | 3386 | - | - | - | - | - |

### Reasoner: accuracy by evidence source, rung, and reasoner spec

> **swept**: reasoner_spec (size + family) × evidence source × rung · **note**: 8b bf16 baseline from the representation run · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: whether the InternVL3 deficit sits on the image step (Chart, Figure) or spreads evenly over the sources

_The reasoner sweep cut by the evidence modality a question draws on, one rung per row. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| evidence_source | rung | internvl3-8b-local | qwen3vl-2b-local | qwen3vl-4b-local | qwen3vl-8b-local | Δ family (InternVL3 − Qwen 8B) | n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| (none) | T | 36.8 (n=19)† | 42.1 (n=19)† | 57.9 (n=19)† | 52.6 (n=19)† | -15.8 | 76 |
| (none) | TL | 42.1 (n=19)† | 57.9 (n=19)† | 57.9 (n=19)† | 63.2 (n=19)† | -21.1 | 76 |
| (none) | TLV | 38.9 (n=18)† | 52.6 (n=19)† | 68.4 (n=19)† | 68.4 (n=19)† | -29.5 | 75 |
| (none) | V | 26.3 (n=19)† | 42.1 (n=19)† | 42.1 (n=19)† | 47.4 (n=19)† | -21.1 | 76 |
| Chart | T | 12.9 (n=178) | 13.5 (n=178) | 16.9 (n=178) | 18.0 (n=178) | -5.1 | 712 |
| Chart | TL | 12.4 (n=178) | 14.0 (n=178) | 19.7 (n=178) | 18.5 (n=178) | -6.2 | 712 |
| Chart | TLV | 20.5 (n=171) | 21.3 (n=178) | 41.0 (n=178) | 44.4 (n=178) | -23.9 | 705 |
| Chart | V | 14.7 (n=177) | 24.2 (n=178) | 34.3 (n=178) | 44.4 (n=178) | -29.7 | 711 |
| Figure | T | 11.7 (n=290) | 12.8 (n=290) | 17.2 (n=290) | 15.2 (n=290) | -3.4 | 1160 |
| Figure | TL | 19.4 (n=289) | 21.7 (n=290) | 23.8 (n=290) | 22.4 (n=290) | -3.0 | 1159 |
| Figure | TLV | 30.1 (n=279) | 35.2 (n=290) | 43.1 (n=290) | 44.5 (n=290) | -14.4 | 1149 |
| Figure | V | 29.3 (n=290) | 34.1 (n=290) | 43.8 (n=290) | 40.3 (n=290) | -11.0 | 1160 |
| Generalized-text (Layout) | T | 18.6 (n=118) | 22.9 (n=118) | 27.1 (n=118) | 28.0 (n=118) | -9.3 | 472 |
| Generalized-text (Layout) | TL | 29.3 (n=116) | 29.7 (n=118) | 34.7 (n=118) | 38.1 (n=118) | -8.8 | 470 |
| Generalized-text (Layout) | TLV | 45.8 (n=107) | 36.4 (n=118) | 46.6 (n=118) | 50.8 (n=118) | -5.1 | 461 |
| Generalized-text (Layout) | V | 33.1 (n=118) | 36.4 (n=118) | 50.0 (n=118) | 48.3 (n=118) | -15.3 | 472 |
| Pure-text (Plain-text) | T | 27.0 (n=289) | 32.6 (n=291) | 38.8 (n=291) | 39.5 (n=291) | -12.5 | 1162 |
| Pure-text (Plain-text) | TL | 34.0 (n=288) | 41.6 (n=291) | 48.1 (n=291) | 47.4 (n=291) | -13.4 | 1161 |
| Pure-text (Plain-text) | TLV | 37.6 (n=279) | 40.9 (n=291) | 51.9 (n=291) | 55.0 (n=291) | -17.3 | 1152 |
| Pure-text (Plain-text) | V | 25.2 (n=290) | 29.2 (n=291) | 39.5 (n=291) | 44.3 (n=291) | -19.2 | 1163 |
| Table | T | 14.7 (n=217) | 25.3 (n=217) | 39.6 (n=217) | 41.0 (n=217) | -26.3 | 868 |
| Table | TL | 23.1 (n=216) | 34.6 (n=217) | 51.2 (n=217) | 49.3 (n=217) | -26.2 | 867 |
| Table | TLV | 23.7 (n=207) | 37.8 (n=217) | 48.8 (n=217) | 50.2 (n=217) | -26.6 | 858 |
| Table | V | 11.5 (n=217) | 26.7 (n=217) | 35.9 (n=217) | 37.3 (n=217) | -25.8 | 868 |
| **All sources** | **T** | **19.3 (n=845)** | **24.7 (n=847)** | **32.3 (n=847)** | **31.9 (n=847)** | **-12.6** | **3386** |
| **All sources** | **TL** | **25.3 (n=842)** | **31.9 (n=847)** | **38.6 (n=847)** | **38.4 (n=847)** | **-13.1** | **3383** |
| **All sources** | **TLV** | **32.6 (n=807)** | **38.3 (n=847)** | **50.4 (n=847)** | **52.4 (n=847)** | **-19.8** | **3348** |
| **All sources** | **V** | **24.1 (n=845)** | **31.9 (n=847)** | **42.4 (n=847)** | **45.5 (n=847)** | **-21.3** | **3386** |
| n (per col) | - | 3339 | 3388 | 3388 | 3388 | - | - |

### Weight footprint per model_spec and quantization level

> **swept**: model_spec × quantization (weight-only memory) · **source**: annotations/model_weights.csv, a static checkpoint property; no run, no device-0 truncation · **memory axis**: weight footprint, NOT peak VRAM

_Weight footprint is a STATIC property of the checkpoint: the summed safetensors tensor bytes, so unlike the measured peak VRAM it is complete rather than device-0 only, needs no re-run, and is the figure a memory claim should cite. SUMMARISED (columns dropped: method, quantizable_params; rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| model_spec | quant | weights_mb | in study |
| --- | --- | --- | --- |
| gemma3-12b-local | 16bit | 24375 | yes |
| gemma3-4b-local | 16bit | 8600 | yes |
| glm4v-9b-local | 16bit | 20586 | yes |
| internvl3-8b-local | 16bit | 15889 | yes |
| minicpmv-8b-local | 16bit | 17392 | yes |
| qwen3vl-2b-local | 16bit | 4255 | yes |
| qwen3vl-32b-local | 16bit | 66715 | yes |
| qwen3vl-32b-local-4bit | 4bit | 19951 | yes |
| qwen3vl-4b-local | 16bit | 8876 | yes |
| qwen3vl-8b-local | 16bit | 17534 | yes |
| qwen3vl-8b-local-8bit | 8bit | 10285 | yes |
| qwen3vl-8b-local-4bit | 4bit | 6775 | yes |
| qwen3vl-8b-thinking-local | 16bit | 17534 | yes |
| n (per col) | - | - | - |

### Mined: quantization sensitivity (accuracy + VRAM delta) by doc_type

> **swept**: quantization (bf16 / 8bit / 4bit) · **note**: 16-bit baseline from the representation run

_delta is vs the 16-bit baseline of the same model; blank when no baseline is in the cache. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **view**: summary — pooled across all doc_types · **swept**: quantization (bf16 / 8bit / 4bit) · **note**: 16-bit baseline from the representation run

_One row per quantization level, so accuracy is directly comparable across the rungs within a level. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| quant | T | TL | TLV | V | overall acc | weights_mb | vram_mb (max) | acc_delta_vs_16bit | vram_delta_mb | n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 4bit | 31.8 (-0.1) | 39.4 (+1.1) | 51.8 (-0.6) | 45.5 (+0.0) | 42.1 | 6775~ | 15830 | +0.1 | -11165 | 3388 |
| 8bit | 32.5 (+0.6) | 37.9 (-0.5) | 53.6 (+1.2) | 45.7 (+0.2) | 42.4 | 10285~ | 21395 | +0.4 | -5600 | 3388 |
| 16bit | 31.9 (+0.0) | 38.4 (+0.0) | 52.4 (+0.0) | 45.5 (+0.0) | 42.0 | 17534 | 26995 | +0.0 | +0 | 3388 |
| n (per col) | 2541 | 2541 | 2541 | 2541 | - | - | - | - | - | - |

### Mined: quantization sensitivity by evidence source and rung

> **swept**: quantization (bf16 / 8bit / 4bit) × evidence source × rung · **note**: 16-bit baseline from the representation run · **source blocks**: overlapping — a question citing Chart + Table is counted in both, so block n do not sum to the corpus; the All sources rows pool each question once · **reading**: whether the small pooled 4-bit cost concentrates on the numeric, dense-table sources or is flat across them

_The same quantization sweep, cut by the evidence modality a question draws on and held at one rung per row, so the delta is a quantization effect and not a rung mix. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: spec / rung / resolution (peak VRAM) · **note**: pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

_headroom_mb = 16384 - peak_vram_mb_max; a negative value means the config OOMs a V100. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

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
| qwen3vl-8b-local | TLV | med | 14143 | 12134 | 2241 | 1436 |
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

> **view**: summary — pooled across all doc_types · **swept**: spec / rung / resolution (peak VRAM) · **note**: pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

_peak = max over all rungs/resolutions; negative headroom means the spec OOMs a V100 at its heaviest config. ⚠ VRAM is SINGLE-DEVICE and understates the true footprint. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: rung / resolution / pages-fed (OOM rate) · **note**: OOM from status rows, pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

_rate = oom cells / all cells in the group, over the 16 GB V100 runs. SUMMARISED (rows restricted to the report's quoted slice); confidence intervals removed. The full table is in `all_tables.md`._

| rung | resolution | pages_fed | oom_rate | n_oom | n_total |
| --- | --- | --- | --- | --- | --- |
| T | med | 1 | 0.1 | 2 | 2928 |
| T | med | 2-5 | 0.8 | 16 | 1896 |
| T | med | 6-10 | 16.7 | 29 | 174 |
| T | med | 11-20 | 50.0 | 15 | 30 |
| TL | med | 1 | 0.7 | 21 | 2928 |
| TL | med | 2-5 | 13.0 | 246 | 1896 |
| TL | med | 6-10 | 27.0 | 47 | 174 |
| TL | med | 11-20 | 46.7 | 14 | 30 |
| TL | med | 21+ | 100.0 | 12 | 12 |
| TLV | high | 1 | 2.7 | 13 | 488 |
| TLV | high | 2-5 | 37.0 | 117 | 316 |
| TLV | high | 6-10 | 100.0 | 29 | 29 |
| TLV | high | 11-20 | 100.0 | 5 | 5 |
| TLV | high | 21+ | 100.0 | 2 | 2 |
| TLV | low | 1 | 1.6 | 8 | 488 |
| TLV | low | 2-5 | 25.9 | 82 | 316 |
| TLV | low | 6-10 | 62.1 | 18 | 29 |
| TLV | low | 11-20 | 100.0 | 5 | 5 |
| TLV | low | 21+ | 100.0 | 2 | 2 |
| TLV | med | 1 | 1.0 | 33 | 3416 |
| TLV | med | 2-5 | 20.7 | 458 | 2212 |
| TLV | med | 6-10 | 61.6 | 125 | 203 |
| TLV | med | 11-20 | 97.1 | 34 | 35 |
| TLV | med | 21+ | 100.0 | 14 | 14 |
| V | high | 2-5 | 0.3 | 1 | 316 |
| V | high | 6-10 | 100.0 | 29 | 29 |
| V | high | 11-20 | 100.0 | 5 | 5 |
| V | high | 21+ | 100.0 | 2 | 2 |
| V | low | 11-20 | 20.0 | 1 | 5 |
| V | low | 21+ | 100.0 | 2 | 2 |
| V | med | 6-10 | 6.4 | 13 | 203 |
| V | med | 11-20 | 57.1 | 20 | 35 |
| V | med | 21+ | 100.0 | 14 | 14 |
| n (per col) | - | - | - | - | - |

### OOM frontier (overall): OOM rate by rung and resolution

> **view**: summary — pooled across all doc_types · **swept**: rung / resolution / pages-fed (OOM rate) · **note**: OOM from status rows, pooled across all G1 runs · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling

_rate = oom cells / all cells; pooled over page buckets and G1 runs. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | high | low | med | n_total |
| --- | --- | --- | --- | --- |
| T | - | - | 1.2 | 5082 |
| TL | - | - | 6.7 | 5082 |
| TLV | 19.6 | 13.6 | 11.2 | 7623 |
| V | 4.4 | 0.4 | 0.8 | 7623 |
| n (per col) | 1694 | 1694 | 22022 | - |

### Mined: prefill vs decode cost per rung per doc_type

> **swept**: representation (prefill / input tokens) · **snapshot**: predictions.v100.jsonl — the pre-recovery V100 rows, kept when the H100 pass upgraded 1,953 of these cells; the live predictions no longer record the V100 ceiling · **TV**: absent: TV only ever ran on the H100, and a latency column cannot mix the two machines. TV's cost sits in the token counts, which are machine-independent: 929 text + 3,404 visual against TLV's 1,644 + 3,404, i.e. 44% less text and 14% less total input on the same questions

_`prefill_ms` and `input_tokens` are the INPUT-bound cost, set by the representation. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: reasoner config × rung (prefill / decode / input tokens) · **machine**: rows grouped by measuring machine; the V100 and H100 groups are never comparable · **note**: the builder loads its own per-group snapshots, so the plan's own load is unused

_Prefill and decode in seconds, mean over the cells every config in the machine group ran (`n` per rung is that matched intersection, so a difference down a group is the config, not the pool). ⚠ NEVER compare a 2xV100 row against an H100 row. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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
| H100 | Qwen3-VL-32B | prefill_s | 0.2 | 0.4 | 0.6 | 0.2 | 846 |
| H100 | Qwen3-VL-32B | decode_s | 5.3 | 6.5 | 6.6 | 6.2 | 846 |
| H100 | Qwen3-VL-32B 4-bit | prefill_s | 0.3 | 0.4 | 0.6 | 0.3 | 846 |
| H100 | Qwen3-VL-32B 4-bit | decode_s | 4.6 | 5.6 | 5.8 | 5.4 | 846 |
| 2xV100 | InternVL3-8B | prefill_s | - | - | - | - | 3180 |
| 2xV100 | InternVL3-8B | decode_s | - | - | - | - | 3180 |
| (any) | input tokens | mean | 938 | 1658 | 5091 | 3470 | 840 |
| (any) | input tokens | min-max | 29-26636 | 37-29489 | 1838-58679 | 1822-43227 | 840 |
| n (per col) | - | - | 831 | 761 | 717 | 834 | - |

### Decode cost by prompt mode (TLV, oracle pages)

> **swept**: prompt_mode × decode cost, at TLV · **reading**: the uninstructed none row is an upper bound and is flagged; cot/extract_cot carry an 8x decode budget

_Decode cost per prompt mode at one rung, so the input side is held fixed and every difference down the table is the instruction's doing. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: routing policy · **note**: the builder loads the complete pool itself so the policies sit on the same rows as the ladder they route over, and the plan's own load is unused; the G3 classifier probe rides in the footer · **cost**: mean input tokens, not seconds — the machine-independent quantity, since the two measuring machines prefill the same input ~50x apart

_Cost is the mean INPUT TOKENS a policy feeds the reasoner, not a latency. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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

> **swept**: paired difference per asserted comparison (bootstrap CI on the delta) · **unit**: documents resampled with replacement, 1000 resamples, seed 0, 2.5%/97.5% quantiles — same convention as the marginal CIs · **pairing**: per question; a question enters only if scored on both sides, so n is the intersection pool · **sides**: each comparison names its own run_tags and specs; the builder loads them rather than slicing one pooled read

_Each row is ONE bootstrap interval on a difference, not two marginal intervals read against each other. SUMMARISED (columns dropped: CI low, CI high, excludes 0); confidence intervals removed. The full table is in `all_tables.md`._

| comparison | rung(s) | Δ (points) | n (paired) | note |
| --- | --- | --- | --- | --- |
| integration deficit (M-S): TL vs T | TL - T | -1.6 | 838 | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): TV vs T | TV - T | -11.4 | 838 | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): TLV vs T | TLV - T | -12.8 | 838 | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| integration deficit (M-S): V vs T | V - T | -9.5 | 838 | 9 hop=none dropped by design (no integration reading), same rule as the integration tables |
| representation margin: TLV vs T | TLV - T | +20.7 | 847 | - |
| parser-free lateral: TLV vs TV | TLV - TV | +0.9 | 847 | - |
| scale: 32B vs 8B at V | V | +11.2 | 847 | left (qwen3vl-8b-local): 13 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| scale: 32B vs 8B at T | T | +3.7 | 847 | left (qwen3vl-8b-local): 16 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| family: Qwen3-VL-8B vs InternVL3-8B at TLV | TLV | +21.1 | 807 | left (internvl3-8b-local): 105 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first); right (qwen3vl-8b-local): 130 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |
| integration deficit (M-S): Thinking vs base 8B at TLV | TLV | +11.8 | 726 | 9 hop=none dropped by design (no integration reading), same rule as the integration tables; left (qwen3vl-8b-local): 130 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first); right (qwen3vl-8b-thinking-local): 112 OOM/error (survivorship: OOM tracks page count, so it removes long multi-page questions first) |

### Levers: what each inference-time intervention does, where data exists

> **swept**: inference-time lever × effect · **sources**: each lever row loads its own run_tag(s) in the builder; blank rows await their runs · **retrieval depth**: PROVISIONAL (partial G2 pool)

_One row per lever: the measured baseline, the lever value, and the delta in points, each with its n. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

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
| retrieval depth k1→k5 (vision) | E2 selection | acc @ V (PROVISIONAL) | 29.8 | 37.2 | +7.4 | 312/312 |
| model swap 8B→InternVL3-8B | reasoner | acc @ TLV | 52.4 | 32.6 | -19.8 | 847/807 |
| thinking variant (M−S) | E4 reasoning | M−S @ TLV | -25.8 | -9.1 | +16.7 | 847/735 |
| n (per col) | - | - | - | - | - | - |

### Inference-time reasoning: accuracy and the integration gap, matched to each control

> **swept**: inference-time reasoning arm (self-consistency / self-refinement / thinking checkpoint) × accuracy and M−S · **controls**: loaded by the builder from g4-faithfulness-full; the strategies carry the grounded instruction so their control is grounded, the thinking checkpoint is plain so its control is none · **pairing**: per arm, the questions the arm and its control both answered; OOM attrition differs by arm, so an unmatched read compares different pools · **reading**: the M−S delta is the point: accuracy that rises while M−S stays flat was spent on questions that were already single-page answerable

_Every arm runs at the combined encoding (TLV) over the answerable pool on oracle pages, so the only thing that changes is how the answer is computed. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| arm | control | control acc (%) | arm acc (%) | delta acc (pts) | control M−S | arm M−S | delta M−S (pts) | matched n | cells ok/ran |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| self-consistency | grounded @ TLV | 51.2 | 51.2 | +0.0 | -18.4 | -15.0 | +3.5 | 602 | 602/847 |
| self-refinement | grounded @ TLV | 48.2 | 49.0 | +0.8 | -19.6 | -17.0 | +2.6 | 778 | 778/847 |
| thinking checkpoint | Instruct @ TLV (none) | 57.0 | 62.2 | +5.2 | -19.9 | -9.1 | +10.8 | 735 | 735/847 |

### Prompt levers: accuracy by evidence hop per prompt mode (TLV, oracle pages)

> **swept**: prompt_mode (none / grounded / cot / extract_cot) × evidence hop, at TLV · **hop**: single/multi only, hop=none dropped · **gap column**: M − S = multi-page minus single-page accuracy, in points (negative = multi-page is worse) · **reading**: whether a prompt lever that lifts pooled accuracy also narrows the multi-page deficit, or only shifts the level

_hop=none is dropped: those rows are answerable questions that recorded no gold evidence pages, not unanswerable ones, so they carry no integration signal. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| prompt_mode | single | multi | M − S | Δ M − S vs grounded | n |
| --- | --- | --- | --- | --- | --- |
| none | 63.5 | 38.5 | -25.0 | -2.1 | 838 |
| grounded | 55.8 | 33.0 | -22.9 | +0.0 | 838 |
| cot | 60.6 | 44.1 | -16.5 | +6.4 | 838 |
| extract_cot | 57.5 | 41.5 | -16.0 | +6.8 | 837 |
| abstain | 50.8 | 29.9 | -20.9 | +1.9 | 838 |
| abstain_balanced | 52.1 | 31.0 | -21.1 | +1.8 | 838 |
| n (per col) | 2880 | 2147 | - | - | - |

### Attribution: representation / retrieval / reasoning loss per rung (PROVISIONAL)

> **swept**: loss channel (representation / retrieval / reasoning) · **retrieval source**: g2-retrieval-full generation rows, loaded by the builder · **status**: PROVISIONAL (partial G2 pool)

_PROVISIONAL (partial G2 pool). SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | oracle acc | representation loss | retrieval ref | retrieved acc | retrieval loss | reasoning residual (raw UB) | oracle n |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T | 31.9 | +20.5 | - | - | - | - | 847 |
| TL | 38.4 | +14.0 | - | - | - | - | 847 |
| TLV | 52.4 | 0.0 (best rung) | joint k3 (paired n=135) | 43.7 | +14.8 | +47.6 | 847 |
| V | 45.5 | +7.0 | joint k3 (paired n=312) | 37.2 | +3.8 | - | 847 |
| n (per col) | 3388 | - | - | - | - | - | - |

## Reconciliation & coverage

### Reconciliation: ladder accuracy on the full pool vs the V100 survivor pool

> **swept**: pool (full answerable vs V100 survivor) × rung · **flag**: a rung moving more than 2 points is marked ⚠

_Same reasoner, pages, parser and prompt on both sides; the only difference is which questions survived. Δ is full minus survivor, flagged ⚠ beyond 2 points. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | full pool | n (full) | survivor pool | n (survivor) | Δ (full − survivor) |
| --- | --- | --- | --- | --- | --- |
| T | 31.9 | 847 | 31.9 | 831 | -0.0 |
| TL | 38.8 | 847 | 39.4 | 761 | -0.6 |
| TLV | 52.5 | 847 | 56.8 | 717 | -4.2 ⚠ |
| V | 45.6 | 847 | 45.9 | 834 | -0.4 |

### Reconciliation: integration deficit (M − S) on the full pool vs the V100 survivor pool

> **swept**: pool (full answerable vs V100 survivor) × rung · **flag**: a rung whose deficit moves more than 2 points is marked ⚠ · **reading**: more negative = wider integration deficit

_`M − S` is multi-page minus single-page accuracy in points, so it is NEGATIVE when multi-page evidence is worse, and a MORE negative value is a WIDER deficit. Δ is full minus survivor, flagged ⚠ beyond 2 points: a negative Δ means the survivor pool understated the deficit. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | full M − S | n (full S/M) | survivor M − S | n (survivor S/M) | Δ deficit |
| --- | --- | --- | --- | --- | --- |
| T | -12.2 | 480/358 | -12.1 | 479/343 | -0.1 |
| TL | -13.7 | 480/358 | -13.1 | 473/279 | -0.6 |
| TLV | -25.0 | 480/358 | -20.3 | 472/236 | -4.7 ⚠ |
| V | -21.7 | 480/358 | -20.8 | 480/345 | -0.9 |

### Pool coverage: cells the earlier V100 run lost to OOM, recovered on the H100

> **swept**: cell pool coverage (shared with the earlier ladder vs recovered)

_`shared cells` are the same question/rung pairs the earlier ladder scored and should reproduce it; `recovered cells` are the ones it never completed. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| rung | earlier run | shared cells | recovered cells | new run (all) | n shared / recovered |
| --- | --- | --- | --- | --- | --- |
| T | 31.9 | 31.9 | - | 31.9 | 847 / 0 |
| TL | 38.4 | 38.8 | - | 38.8 | 847 / 0 |
| TLV | 52.4 | 52.5 | - | 52.5 | 847 / 0 |
| V | 45.5 | 45.6 | - | 45.6 | 847 / 0 |

### Source stratification: oracle accuracy by source dataset and rung

> **swept**: source_dataset stratum × rung · **strata**: loader dataset id only; no upstream QA provenance exists

_This table cannot separate inherited from native questions, and the blank is the finding. SUMMARISED: confidence intervals removed. The full table is in `all_tables.md`._

| source_dataset | T | TL | TLV | V | n |
| --- | --- | --- | --- | --- | --- |
| mmlongbench | 31.9 | 38.4 | 52.4 | 45.5 | 3388 |
| (uncoded) | 16 cells, no acc | 86 cells, no acc | 130 cells, no acc | 13 cells, no acc | 245 |
| n (per col) | 847 | 847 | 847 | 847 | - |
