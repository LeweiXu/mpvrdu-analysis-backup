## Turn 1 — document page 6 (rank 1 of 19)

In the "Datasets" section under "4 Experiments", the text describes the evaluation sets for each dataset:
- PrOntoQA: uses the hardest 5-hop subset for evaluation.
- ProofWriter: uses the hardest depth-5 subset, with 600 examples randomly sampled from the test set.
- FOLIO: uses the entire FOLIO test set for evaluation, consisting of 204 examples.
- LogicalDeduction: uses the full test set consisting of 300 examples.
- AR-LSAT: uses the test set which has 231 multiple-choice questions.

## Turn 2 — document page 5 (rank 2 of 19)

The current page contains Table 1, which lists the symbolic formulations and solvers for five datasets. The row for "First-Order Logic" (FOL) shows that Prover9 is the solver used for the FOLIO dataset. The text in section 3.2 "Symbolic Reasoner" confirms that Prover9 is used as the FOL inference engine for FOLIO. However, this page does not specify the number of examples in the FOLIO dataset used for evaluation. The NOTES from page 6 state that FOLIO uses the entire test set for evaluation, which consists of 204 examples. This information is not on the current page.

## Turn 3 — document page 8 (rank 3 of 19)

none

## Turn 4 — document page 14 (rank 4 of 19)

Table 5: Statistics of the logical reasoning datasets.
| Dataset       | Reasoning | Test Size | #Opts |
|---------------|-----------|-----------|-------|
| PrOntoQA      | Deductive | 500       | 2     |
| ProofWriter   | Deductive | 600       | 3     |
| FOLIO         | FOL       | 204       | 3     |
| LogicalDeduction | CSP   | 300       | 3,5,7 |
| AR-LSAT       | AR        | 230       | 5     |

## Turn 5 — document page 7 (rank 5 of 19)

Table 3 presents the execution rate (Exe_Rate) and execution accuracy (Exe_Acc) for LOGIC-LM on each dataset. For FOLIO, the execution rate with self-refinement (+) is 84.3%, and the execution accuracy is 64.3%. The table also shows that for FOLIO, the execution rate without self-refinement (-) is 66.7%, and the execution accuracy is 61.8%. This data is relevant to the performance of the symbolic solver Prover9 on the FOLIO dataset, as Prover9 is the solver used for FOLIO, as noted in previous pages. However, this page does not state the number of examples in the FOLIO dataset used for evaluation.

## Turn 6 — document page 2 (rank 6 of 19)

This page introduces the LOGIC-LM framework and lists the five datasets used for evaluation: ProofWriter, PrOntoQA, FOLIO, AR-LSAT, and LogicalDeduction. It mentions that FOLIO involves First-Order Logic (FOL) reasoning problems and that a FOL inference engine is used, which is consistent with Prover9 being the solver for FOLIO as noted in previous pages. However, this page does not contain any information about the number of examples in the FOLIO dataset used for evaluation.

## Turn 7 — document page 1 (rank 7 of 19)

none

## Turn 8 — document page 4 (rank 8 of 19)

This page describes the symbolic formulations used in the framework, including Logic Programming (LP) Language and First-Order Logic (FOL). It explains how problems are translated into symbolic languages and how different types of reasoning problems (deductive, FOL, CSP, analytical) are handled. The page mentions that Prover9 is used as the FOL inference engine for FOLIO, but does not provide any information about the number of examples in the FOLIO dataset used for evaluation. The page also references Table 1 for examples of FOL formulas, but Table 1 is not shown on this page.

## Turn 9 — document page 10 (rank 9 of 19)

none
