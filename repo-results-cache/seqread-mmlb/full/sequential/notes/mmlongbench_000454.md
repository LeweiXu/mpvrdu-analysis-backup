## Turn 1 — document page 5 (rank 1 of 20)

Table 1: Strong performance of STEP-BACK PROMPTING on STEM tasks achieving state-of-the-art surpassing GPT-4. CoT: zero-shot Chain of Thought prompting (Kojima et al., 2022), TDB: Take a Deep Breathe prompting (Yang et al., 2023). The Table reports the average accuracy over 5 evaluation runs, with standard deviations in the parentheses.
| Method | MMLU Physics | MMLU Chemistry |
| :--- | :--- | :--- |
| PaLM-2L | 66.4% (0.8%) | 70.9% (0.9%) |
| PaLM-2L 1-shot | 64% (1.6%) | 75.6% (0.4%) |
| PaLM-2L + CoT | 65% (2%) | 75.3% (1.5%) |
| PaLM-2L + CoT 1-shot | 61.5% (1.8%) | 76.6% (1%) |
| PaLM-2L + TDB | 65.7% (0.7%) | 73.8% (1.1%) |
| PaLM-2L + Step-Back (ours) | 73.2% (1.9%) | 81.8% (1.4%) |
| GPT-4 | 70.3% (2.3%) | 79.9% (1.0%) |

## Turn 2 — document page 6 (rank 2 of 20)

Table 2 on page 6 shows performance on Knowledge QA tasks, including MMLU Physics (represented as "SituatedQA" in the table). The row for "PaLM-2L + Step-Back (ours)" shows a score of 66% for SituatedQA. The text below the table clarifies that SituatedQA corresponds to MMLU high-school Physics. The text also notes that Reasoning and Math skills are critical for MMLU Physics, and that Reasoning Error is the dominant error type for Step-Back.

## Turn 3 — document page 1 (rank 3 of 20)

This page contains the title, abstract, and introduction of the paper. The abstract mentions that STEP-BACK PROMPTING improves PaLM-2L performance on MMLU Physics by 7%. The introduction mentions the paper's focus on reasoning-intensive tasks including STEM, but does not provide specific scores. Figure 1 shows a bar chart comparing model performance, but the chart is not detailed enough to extract the exact score for PaLM-2L + Step-Back on MMLU Physics from this page alone.

## Turn 4 — document page 4 (rank 4 of 20)

This page describes the experimental setup for evaluating STEP-BACK PROMPTING on STEM tasks, specifically MMLU high-school Physics and Chemistry. It explains that the method involves teaching the model to abstract concepts and principles (e.g., Newton's first law, Doppler effect) to aid reasoning. The page details baseline methods including PaLM-2L, PaLM-2L + CoT, PaLM-2L + TDB, and GPT-4, but does not contain any specific performance scores for PaLM-2L + Step-Back on MMLU Physics.

## Turn 5 — document page 13 (rank 5 of 20)

Table 4: Stats of the evaluation datasets used in this paper.
| Domain | Dataset | Split | Number of Examples |
| :--- | :--- | :--- | :--- |
| STEM | MMLU high-school Physics | Test | 151 |
| STEM | MMLU high-school Chemistry | Test | 203 |
| Knowledge QA | TimeQA | Test | 5226 |
| Knowledge QA | TimeQA Easy | Test | 2613 |
| Knowledge QA | TimeQA Hard | Test | 2613 |
| Knowledge QA | SituatedQA | Test | 2901 |
| Multi-hop Reasoning | MuSiQue | Dev | 2417 |
| Multi-hop Reasoning | StrategyQA | Dev | 229 |

## Turn 6 — document page 3 (rank 6 of 20)

The current page discusses the efficacy of STEP-BACK PROMPTING, mentioning that it improves the performance of PaLM-2L across the board, with specific improvements of 7% on MMLU Physics and 11% on MMLU Chemistry. It also notes that STEP-BACK PROMPTING has strong performance improvements over CoT and TDB prompting, and that it fixes a large portion of base model errors. However, this page does not provide the absolute score for PaLM-2L + Step-Back on MMLU Physics.
