## Turn 1 — document page 2 (rank 1 of 20)

In the "Setting of Conscious Incompetence" section, the text states: "A sentence can map to both [NA] and a list of sub-graph knowledge if it can [be verified, but the knowledge is absent in the knowledge graph G]."

## Turn 2 — document page 5 (rank 2 of 20)

## Figure 3: An illustration of how we evaluate the precision and recall for conscious incompetence ([NA])

The figure shows two scenarios:
- **Left side (Sentence 1 [k1][k2], Sentence 2 [k3][NA], Sentence 3 [k6][k9])**: The "Absent Knowledge Set" is [k2][k4][k5]. The "Model Output" includes [k1][k2] and [k3][k4][k5] (with [k4] and [k5] being absent from the output). The "NA Precision" is calculated as 1/2 = 0.5, and "NA Recall" is 1/3 = 0.33.
- **Right side (Sentence 1 [k1][k2], Sentence 2 [k3][NA], Sentence 3 [k6][k9])**: The "Absent Knowledge Set" is [k2][k4][k5]. The "Model Output" includes [k1][k2] and [k3][k4][k5] (with [k4] and [k5] being absent from the output). The "NA Precision" is calculated as 1/2 = 0.5, and "NA Recall" is 1/3 = 0.33.

The text in Section 4.4 "Conscious Incompetence Evaluation" states: "Theoretically, each [NA] mark should map to a piece of knowledge absent from the retrieved knowledge graph G."

## Turn 3 — document page 1 (rank 3 of 20)

This page introduces the paper's context and motivation. It discusses the problem of hallucination in LLMs and the need for language attribution. It mentions the proposed "Conscious Incompetence" setting, which considers incomplete knowledge repositories. However, it does not contain the specific definition or condition under which a sentence can map to both [NA] and a list of sub-graph knowledge. The definition is provided in a later section.

## Turn 4 — document page 4 (rank 4 of 20)

## Section 3.3: Generation

The text states: "We construct a prompt (Table 13 in appendix D) which includes 1) instruction to the models to generate attributed answers. 2) retrieved knowledge graph, and 3) the question. We employ one-shot in-context learning (Brown et al., 2020) by prepending one human written demonstration. In the one-shot demonstration, we use the special token [NA] to represent the “Not Applicable Citations” for conscious incompetence. We deliberately omit some knowledge in the demonstration example knowledge graph, and we insert [NA] tokens in the corresponding sentences that use these knowledge within the example answer."

This section describes the use of [NA] tokens to indicate missing knowledge in the demonstration example, which is part of the conscious incompetence setting. It confirms that [NA] is used when knowledge is absent from the retrieved knowledge graph.

## Turn 5 — document page 8 (rank 5 of 20)

## Figure 4: Precision, Recall, and F1-Score for [NA]
- Recall is stable at about 15 regardless of the number of absent knowledge.
- Precision and F1-Score exhibit a clear upward trend as the number of absent knowledge increases.
- This indicates that with more absent knowledge in the KG, [NA] enables generated outputs to locate absent knowledge more accurately.
- The “Conscious Incompetence” setting plays an increasingly crucial role when the coverage problem of the knowledge graph is more serious.

## Section 5.3: Retrieval Analysis
- An ablation study examines the impact of retrieval accuracy on model output.
- Retrieval accuracy is simulated from 100 to 20 at intervals of 20.
- Results show clear downward trends in all metrics as retrieval accuracy drops.
- The impact on recall (green) is much more significant than on precision (yellow).
- The reduction in recall was nearly linear as retrieval accuracy decreased.
- The greatest drop in recall occurred between ground truth (57.1) and 80 accuracy.

## Section 5.4: Human Evaluation
- Human evaluation verifies the correlation between automatic evaluation and human judgment.
- Human evaluation results are shown in Table 6.
- For all three baselines, automatic and human scores are close with a gap within 2.5.
- This indicates a strong correlation between automatic evaluation and human judgments.

## Table 6: Result of Human Evaluation on text-citation alignment
| Model          | Alignment | Human Avg. |
|----------------|-----------|------------|
| ChatGPT(0.5)   | 84.5      | 82.0       |
| LLaMA-7B       | 47.8      | 45.5       |
| Vicuna-13B     | 66.9      | 64.5       |

## Turn 6 — document page 7 (rank 6 of 20)

## Section 5.2: Conscious Incompetence

This section discusses the evaluation of citation quality when knowledge is removed from the provided knowledge graph. It states that the removal of required knowledge has a minimal impact on correctness but significantly affects citation precision and recall. The text further explains that with more knowledge absent from the provided knowledge graph, both precision and recall drop drastically, demonstrating that the coverage issue poses a considerable challenge to generating answers with high quality citations.

The section also mentions that the evaluation of [NA] precision and recall is next, but the specific results or definitions related to [NA] precision and recall are not provided on this page.
