## Turn 1 — document page 8 (rank 1 of 20)

Table 3: Results of STEP-BACK PROMPTING on Multi-Hop Reasoning. CoT: Chain of Thought prompting, TDB: Take a Deep Breathe prompting, RAG: retrieval augmentation generation. Average accuracy is over 5 evaluation runs with the standard deviations included in the parentheses.

| Method                 | MuSiQue | StrategyQA |
|-----------------------|---------|------------|
| PaLM-2L               | 35.5% (3%) | 82.8% (0.7%) |
| PaLM-2L 1-shot        | 29.0% (0.5%) | 76.6% (0.5%) |
| PaLM-2L + CoT         | 38.7% (3.2%) | 83.6% (0.4%) |
| PaLM-2L + CoT 1-shot  | 38.5% (2.2%) | 76.8% (1.4%) |
| PaLM-2L + TDB         | 39.0% (2.3%) | 82.7% (0.9%) |
| PaLM-2L + RAG         | 39.6% (2.8%) | 84.2% (0.5%) |
| PaLM-2L + Step-Back (ours) | 42.6% (3.1%) | 82.7% (0.4%) |
| PaLM-2L + Step-Back + RAG (ours) | 42.8% (2.0%) | 86.4% (1%) |
| GPT-4                 | 38.5% (0.2%) | 78.3% (1.1%) |

- Reasoning Error: The retrieved context is relevant, but the model still fails to reason through the context to arrive at the right answer.
StepBack rarely fails. In contrast, we find more than half of the errors are due to reasoning errors. 45% of errors are due to failure in retrieving the right information despite that Abstraction provided by step-back makes it a much easier task. This reflects the difficulty level of the TimeQA task. Additional error analysis of TimeQA is in Appendix A.

6 MULTI-HOP REASONING
We evaluate STEP-BACK PROMPTING on challenging Multi-Hop reasoning benchmark MuSiQue (Trivedi et al., 2022) and StrategyQA (Geva et al., 2021). We follow the same protocol as Section 5 to implement STEP-BACK PROMPTING.

6.1 RESULTS
Table 3 shows performance of various baselines on the dev set of MuSiQue and StrategyQA. Baseline performance of PaLM-2L and GPT4 are low (35.5% and 38.5% for PaLM-2L and GPT-4 respectively) in MuSiQue since it is a hard multihop reasoning behchmark. In contrast, ErtartegyQA has stronger baselines (82.8% and 78.3% for PaLM-2L and GPT4 respectively) probably because of the binary classification task. CoT and TDB improve model performance a bit in case of MuSiQue (~ 3% and 3.5% respectively) which can be attributed to the inherent reasoning nature of this task where these methods are shown to be helpful. In case of StrategyQA, there is no significant performance gain with COT and TDB which could be due to the high baseline performance in this task, with limited scope for these prompting methods to improve performance. Often, 1-shot performance is significantly lower than their zero-shot methods which could be attributed to the potential example bias (Zhao et al., 2021; Parmar et al., 2023). RAG improves model performance (~ 4% and 2% for MuSiQue and StrategyQA respectively.). STEP-BACK PROMPTING with the power of abstraction produces the best performance of all methods: 42.8% in MuSiQue and 86.4% in StrategyQA, significantly outperforming GPT-4 on both tasks.

6.2 ANALYSIS
Similar to our observation in previous sections, we find that STEP-BACK PROMPTING with RAG is able to turn 15.4% wrong predictions of base model into correct predictions, while leading to 6.1% errors the other way around. Furthermore, Step-Back + RAG fixes 12.7% errors coming from RAG. The errors introduced to RAG by Step-Back is just 4.4%. More detailed analysis is in Appendix A.2.

## Turn 2 — document page 7 (rank 2 of 20)

In Section 5.2 Results on page 7, the document states:
- Baseline PaLM-2L accuracy on TimeQA: 41.5%
- PaLM-2L + RAG accuracy on TimeQA: 57.4%
- PaLM-2L + Step-Back + RAG accuracy on TimeQA: 68.7%

## Turn 3 — document page 4 (rank 3 of 20)

This page introduces the datasets and models used in the study. It mentions TimeQA as a challenging open-retrieval QA dataset requiring time-sensitive knowledge. It also lists the models used: PaLM-2L and GPT-4. The page describes baseline methods including PaLM-2L, PaLM-2L + CoT, PaLM-2L + TDB, and PaLM-2L + RAG. It notes that RAG is not used for MMLU due to its reasoning nature. The page does not contain any specific accuracy numbers for TimeQA.

## Turn 4 — document page 12 (rank 4 of 20)

## A.1 TIMEQA ERROR ANALYSIS

The text states: "Figure 6 shows that compared to the predictions of baseline PaLM-2L, STEP-BACK PROMPTING is able to fix 39.9% of the predictions where the baseline prediction is wrong, while causing 5.6% errors. Furthermore, Step-Back + RAG fixes 21.6% errors coming from RAG. The % of errors introduced by STEP-BACK PROMPTING to RAG is still relatively low (6.3%)."

This section provides error analysis for TimeQA, but does not contain the absolute accuracy numbers for PaLM-2L or PaLM-2L + RAG on TimeQA. The error analysis is relative to the baseline model's predictions.

## Turn 5 — document page 6 (rank 5 of 20)

Table 2 on this page shows the accuracy of various models on TimeQA:
- PaLM-2L: 41.5%
- PaLM-2L + RAG: 57.4%

## Turn 6 — document page 13 (rank 6 of 20)

Table 4: Stats of the evaluation datasets used in this paper.
| Domain       | Dataset             | Split | Number of Examples |
|--------------|---------------------|-------|--------------------|
| STEM         | MMLU high-school Physics | Test  | 151                |
|              | MMLU high-school Chemistry | Test  | 203                |
| Knowledge QA | TimeQA              | Test  | 5226               |
|              | TimeQA Easy         | Test  | 2613               |
|              | TimeQA Hard         | Test  | 2613               |
|              | SituatedQA          | Test  | 2901               |
| Multi-hop Reasoning | MuSiQue      | Dev   | 2417               |
|              | StrategyQA          | Dev   | 229                |

The page includes a section with example questions and answers for evaluating answer equivalence, but it does not contain any accuracy numbers for PaLM-2L or PaLM-2L + RAG on TimeQA.

## Turn 7 — document page 1 (rank 7 of 20)

The abstract on this page states: "STEP-BACK PROMPTING improves PaLM-2L performance on MMLU Physics and Chemistry by 7% and 11%, TimeQA by 27%, and MuSiQue by 7%."
