## Turn 1 — document page 7 (rank 1 of 20)

Figure 4: F1 score for fact-checking with gold evidence using FLAN-T5 (blue line) and PROGRAMFC (green line) for language models of increasing sizes: FLAN-T5-small (80M), FLAN-T5-base (250M), FLAN-T5-large (780M), FLAN-T5-XL (3B), and FLAN-T5-XXL (11B) on HOVER 2-hop (left), 3-hop (middle), and 4-hop (right).

The figure contains three charts:
- Left chart (HOVER 2-hop): 
  - FLAN-T5-small (80M): 64.59 (FLAN-T5), 68.24 (PROGRAMFC)
  - FLAN-T5-base (250M): 72.56 (FLAN-T5), 76.11 (PROGRAMFC)
  - FLAN-T5-large (780M): 75.65 (FLAN-T5), 73.69 (PROGRAMFC)
  - FLAN-T5-XL (3B): 77.42 (FLAN-T5), 77.01 (PROGRAMFC)
  - FLAN-T5-XXL (11B): 77.42 (FLAN-T5), 77.01 (PROGRAMFC)
- Middle chart (HOVER 3-hop):
  - FLAN-T5-small (80M): 62.23 (FLAN-T5), 67.88 (PROGRAMFC)
  - FLAN-T5-base (250M): 68.05 (FLAN-T5), 68.55 (PROGRAMFC)
  - FLAN-T5-large (780M): 65.66 (FLAN-T5), 66.89 (PROGRAMFC)
  - FLAN-T5-XL (3B): 69.56 (FLAN-T5), 66.75 (PROGRAMFC)
  - FLAN-T5-XXL (11B): 69.56 (FLAN-T5), 66.75 (PROGRAMFC)
- Right chart (HOVER 4-hop):
  - FLAN-T5-small (80M): 62.49 (FLAN-T5), 64.58 (PROGRAMFC)
  - FLAN-T5-base (250M): 68.08 (FLAN-T5), 68.08 (PROGRAMFC)
  - FLAN-T5-large (780M): 63.36 (FLAN-T5), 63.39 (PROGRAMFC)
  - FLAN-T5-XL (3B): 66.75 (FLAN-T5), 66.75 (PROGRAMFC)
  - FLAN-T5-XXL (11B): 66.75 (FLAN-T5), 66.75 (PROGRAMFC)

Figure 5: Retrieval recall@10 for the one-step retrieval and the iterative retrieval in PROGRAMFC.
- HOVER 2-hop: 51.33 (one-step), 74.18 (PROGRAMFC)
- HOVER 3-hop: 50.37 (one-step), 71.13 (PROGRAMFC)
- HOVER 4-hop: 46.43 (one-step), 76.25 (PROGRAMFC)
- FEVEROUS-S: 60.93 (one-step), 65.65 (PROGRAMFC)

## Turn 2 — document page 6 (rank 2 of 20)

Table 1 on page 6 shows the Macro-F1 scores for ProgramFC and baselines on HOVER and FEVEROUS-S datasets. For the gold evidence setting (Gold column), the F1 scores for ProgramFC are:
- HOVER (2-hop): 74.10 (N=1) and 75.65 (N=5)
- HOVER (3-hop): 66.13 (N=1) and 68.48 (N=5)
- HOVER (4-hop): 65.69 (N=1) and 66.75 (N=5)
- FEVEROUS-S: 91.77 (N=1) and 92.69 (N=5)

## Turn 3 — document page 5 (rank 3 of 20)

This page describes the experimental setup, including datasets (HOVER and FEVEROUS-S), baselines, and few-shot learning constraints. It mentions that ProgramFC is compared against FLAN-T5-small and other models, and that evaluation is done on validation sets of HOVER and FEVEROUS-S. However, it does not provide the specific F1 scores for ProgramFC on these datasets with gold evidence, nor does it list the scores in descending order as required by the question. The page contains code examples and figures related to the prompt template and implementation, but no new F1 score data for ProgramFC.

## Turn 4 — document page 8 (rank 4 of 20)

Table 3 on page 8 shows macro-F1 scores for ProgramFC and baselines in the closed-book setting. For ProgramFC, the scores are:
- HOVER 2-hop: 54.27
- HOVER 3-hop: 54.18
- HOVER 4-hop: 52.88
- FEVEROUS: 59.66

This page does not contain F1 scores for ProgramFC on the datasets with gold evidence, which is required by the question. The scores in Table 3 are for the closed-book setting, not the gold evidence setting.

## Turn 5 — document page 15 (rank 5 of 20)

none

## Turn 6 — document page 3 (rank 6 of 20)

none
