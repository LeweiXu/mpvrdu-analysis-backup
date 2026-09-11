## Turn 1 — document page 1 (rank 1 of 20)

Figure 1: A demonstration of our task set up. Given a question, the system generates answers attributed from a retrieved knowledge graph. The underlines in question are the retrieved entities, and the underlines in outputs are the citations. [NA] is the “Not Applicable Citation”.

## Turn 2 — document page 5 (rank 2 of 20)

Figure 2: An illustration of how we evaluate the precision and recall for generated citations.
Eval (Liu et al., 2023b), which defines the following four metrics: 1) Coherence: whether the generated text is well-structured and well-organized. 2) Consistency: whether the generated text is consistent with the knowledge provided. 3) Fluency: whether the generated text is well-written and grammatical. 4) Relevance: how well is the generated text relevant to the question.
We use the model text-davinci-003 for evaluation, which assigns an integer score of 1 to 5 for each metric. We follow the prompt provided in G-Eval (Liu et al., 2023b) and customize it based on our task. The full prompts are given in appendix D.
4.2 Citation Evaluation
We evaluate the citation qualities from three aspects: 1) Correctness, which measures whether the generated knowledge matches the given knowledge from the knowledge graph, 2) Precision, which determines how much of the generated citations are helpful to answer the question, and 3) Recall, which measures how much of the minimum knowledge set are covered by the generated citations. We also calculate the F1-Score based on the Precision and Recall to reflect the overall quality of citations.
Correctness We calculate the citation correctness for each citation (0 or 1) and average over all citations. Each citation comprises a triplet of 1) center entity QID, 2) relation 3) neighbour entity value. If the generated citation is complete with all three parts, and exactly matches a triplet from the question's retrieved KG, correctness = 1.
Precision We calculate citation precision for each citation (0 or 1) and average over all citations to get micro precision. Precision = 1 for a citation if and only if 1) it is correct, and 2) it matches one
Figure 3: An illustration of how we evaluate the precision and recall for conscious incompetence ([NA])
knowledge triplet from minimum knowledge set of the question. (See Figure 2.)
Recall We calculate citation recall for each knowledge (0 or 1) in minimum knowledge set, and average over all knowledge to get micro recall. Recall = 1 if and only if the knowledge if hit by a correct citation. (See Figure 2.)
We average over all citations/knowledge in an answer, and average all answer-level precision/recall to get macro precision and recall. we calculate micro and macro F1-Score from corresponding precision and recall.
4.3 Text-Citation Alignment
Other than the text quality and citation quality, we measure whether the generated citations provide support for the corresponding sentences. A piece of useful knowledge is not an ideal citation if it is irrelevant to the sentence it links to. Therefore, we propose the metric “Alignment” which determines whether the generated citations are aligned to the sentences to which they belong. We use a state-of-the-art natural language inference (NLI) model TRUE (Honovich et al., 2022), which is a fine-tuned T5-11B (Raffel et al., 2020) model, to check whether the generated sentence entails the generated citation. Since one sentence could have multiple citations, we run NLI on all sentence-citation pairs and report the percentage of entailment. Additionally, we conduct human evaluation in § 5.4 to showcase if the automatic evaluation is correlated with human judgments.
4.4 Conscious Incompetence Evaluation
Theoretically, each [NA] mark should map to a piece of knowledge absent from the retrieved

## Turn 3 — document page 8 (rank 3 of 20)

none

## Turn 4 — document page 2 (rank 4 of 20)

none

## Turn 5 — document page 13 (rank 5 of 20)

none

## Turn 6 — document page 12 (rank 6 of 20)

none

## Turn 7 — document page 4 (rank 7 of 20)

none

## Turn 8 — document page 3 (rank 8 of 20)

none

## Turn 9 — document page 6 (rank 9 of 20)

none

## Turn 10 — document page 22 (rank 10 of 20)

none

## Turn 11 — document page 15 (rank 11 of 20)

none

## Turn 12 — document page 7 (rank 12 of 20)

none

## Turn 13 — document page 9 (rank 13 of 20)

Table 7: Comparison of evaluation results on General and Specific question setting
| Setting | Model | Align. | Corr. | Prec. | Rec. | F1. | Coh. | Con. | Flu. | Rel. |
|---|---|---|---|---|---|---|---|---|---|---|
| General | GPT-4 (0.5) | 90.9 | 97.6 | 30.8 | 42.1 | 35.6 | 4.38 | 4.77 | 4.48 | 4.48 |
| General | ChatGPT (0.5) | 82.7 | 94.5 | 25.2 | 47.4 | 32.9 | 4.64 | 4.89 | 4.45 | 4.70 |
| Specific | GPT-4 (0.5) | 92.0 | 97.6 | 36.0 | 43.6 | 39.4 | 4.48 | 4.89 | 4.64 | 4.72 |
| Specific | ChatGPT (0.5) | 84.5 | 94.8 | 29.9 | 49.0 | 37.2 | 4.57 | 4.94 | 4.71 | 4.81 |

5.5 General and Specific Questions
We compare experiments results of text, citation (micro), and alignment between the general and specific questions in Table 7. The results show that the same model's answers on specific questions outperform those on general questions in almost all metrics. The finding is not surprising because the specific questions provide clearer instructions to the models on which knowledge to use. In addition, the general questions in the dataset are inherently loosely bonded to the minimum knowledge set, and hence have impacts on the evaluation results. This experiment shows a trade-off between how explicitly the question context mentions the knowledge, and how irreplaceably the knowledge is required by the question. The specific questions target the knowledge more explicitly in the question context, and hence cover the scope of the paragraph better. It stands for an upper bound for knowledge coverage and a lower bound for question naturalness. The general questions implicitly target the knowledge in the question context, and there loosely cover the scope of the paragraph. It stands for an upper bound for question naturalness and a lower bound for knowledge coverage.

## Turn 14 — document page 18 (rank 14 of 20)

none

## Turn 15 — document page 11 (rank 15 of 20)

none

## Turn 16 — document page 17 (rank 16 of 20)

none

## Turn 17 — document page 10 (rank 17 of 20)

none

## Turn 18 — document page 14 (rank 18 of 20)

none

## Turn 19 — document page 16 (rank 19 of 20)

none

## Turn 20 — document page 20 (rank 20 of 20)

none
