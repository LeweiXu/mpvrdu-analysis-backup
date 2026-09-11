## Turn 1 — document page 8 (rank 1 of 20)

In Table 3, under the "InstructGPT" section and the "Self-Ask" row, the macro-F1 score for the HOVER 4-hop dataset is 52.45.

## Turn 2 — document page 15 (rank 2 of 20)

none

## Turn 3 — document page 7 (rank 3 of 20)

Figure 4 shows F1 scores for fact-checking with gold evidence using FLAN-T5 and PROGRAMFC for different model sizes on HOVER 2-hop, 3-hop, and 4-hop datasets. For the HOVER 4-hop dataset, the F1 score for PROGRAMFC (green line) with FLAN-T5-small (80M) is 77.01, and with FLAN-T5-base (250M) is 77.01. The F1 score for PROGRAMFC with FLAN-T5-large (780M) is 77.01, with FLAN-T5-XL (3B) is 77.01, and with FLAN-T5-XXL (11B) is 77.01. Figure 5 shows retrieval recall@10 for one-step and iterative retrieval in PROGRAMFC, with PROGRAMFC outperforming one-step retrieval on all datasets, with the largest improvement of 37.1% on HOVER 4-hop.

## Turn 4 — document page 6 (rank 4 of 20)

Table 1 shows Macro-F1 scores for PROGRAMFC and baselines on HOVER and FEVEROUS-S. For the HOVER (4-hop) dataset in the Gold evidence setting, ProgramFC (N=1) has a score of 65.69, and ProgramFC (N=5) has a score of 66.75. The text mentions that ProgramFC (N=5) outperforms baselines on 4-hop claims by 14.77% on average, and that the performance drop for ProgramFC from 2-hop to 4-hop is only 11.7%. The text also states that ProgramFC (N=5) achieves 66.75 F1 on HOVER 4-hop in the gold setting.

## Turn 5 — document page 3 (rank 5 of 20)

none

## Turn 6 — document page 5 (rank 6 of 20)

This page describes the Codex prompt template (Figure 2) and the implementation of the question-answering sub-task (Figure 3) for different settings (open-book and closed-book). It details the datasets (HOVER and FEVEROUS-S) and baselines used in the experiments. The page mentions that HOVER is divided into 1,126 two-hop, 1,835 three-hop, and 1,039 four-hop claims. It also states that for evaluation in the open-book setting, Wikipedia corpora are used as knowledge sources, and for the closed-book setting, the model must reason without external knowledge. The page does not contain any specific performance metrics for the InstructGPT model with Self-Ask in the closed-book setting on the dataset with the highest ProgramFC retrieval recall@10.
