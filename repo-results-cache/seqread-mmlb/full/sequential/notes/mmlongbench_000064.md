## Turn 1 — document page 7 (rank 1 of 20)

Table 3: Citation Quality OpenAI models and LLaMA family models. The first five metrics are reported in Micro, and the last three metrics are reported in Macro. We also report text citation alignment.
The experimental results are the mean of three runs, and the standard deviation is reported in brackets.
In general, there is a room of improvement for all models since no model can achieve a micro F1 Score of higher than 40. The OpenAI models outperform the LLaMA family models in almost all metrics. The correctness is above 94 for OpenAI models, but around 70 for LLaMA based models. For ChatGPT, temperature does not play a significant role since it effect on F1 Score is at most 1.2. The GPT-4 model achieves the best performance across almost all metrics, except for recall, since GPT-4 models tend to generate shorter answers with fewer citations, resulting in higher precision. While LLaMA is better at Recall by generating long answers with many citations. The F1-Score of models from the same family are close to one another, showing that our automatic evaluation metric designed is reliable.
Text-Citation Alignment From Table 3, similar to citation quality, the OpenAI models also outperform the LLaMA based models on text-citation alignment. In addition, models with 7B, 13B, 175B (ChatGPT), and trillion level (GPT4) parameters have an alignment score of 40+, 60+, 80+, and 92 respectively. LLaMA-13B model has an improvement of 14.3 compared to LLaMA-7B model. This shows that parameter size may play an important role in generating sentences and citations with good alignment.
Text Quality Evaluation We present the evaluation of generated text quality in Table 4. From the results, we find that OpenAI models, in general, have better text quality in all metrics compared to LLaMA family models, which corresponds to the citation evaluation results. All models exhibit rather high consistency, indicating that the LLMs
Table 4: Evaluation on generated text quality.
Table 5: Citation quality evaluation for generated texts using a KG with N pieces of knowledge removed.
5.2 Conscious Incompetence
We first evaluate citation quality of the generated text with knowledge removed using method described in § 4.4. From Table 5, the removal of required knowledge has a minimal impact on correctness, but significantly affects citation precision and recall. With more knowledge absent from provided knowledge graph, both precision and recall drops drastically, demonstrating that the coverage issue poses a considerable challenge to generating answers with high quality citations.
Next, we evaluate [NA] precision and recall.

## Turn 2 — document page 8 (rank 2 of 20)

Table 6: Result of Human Evaluation on text-citation alignment
| | Alignment | Human Avg. |
|---|---|---|
| ChatGPT(0.5) | 84.5 | 82.0 |
| LLaMA-7B | 47.8 | 45.5 |
| Vicuna-13B | 66.9 | 64.5 |

## Turn 3 — document page 9 (rank 3 of 20)

Table 7: Comparison of evaluation results on General and Specific question setting
| Setting | Model | Align. | Corr. | Prec. | Rec. | F1. | Coh. | Con. | Flu. | Rel. |
|---|---|---|---|---|---|---|---|---|---|---|
| General | GPT-4 (0.5) | 90.9 | 97.6 | 30.8 | 42.1 | 35.6 | 4.38 | 4.77 | 4.48 | 4.48 |
| General | ChatGPT (0.5) | 82.7 | 94.5 | 25.2 | 47.4 | 32.9 | 4.64 | 4.89 | 4.45 | 4.70 |
| Specific | GPT-4 (0.5) | 92.0 | 97.6 | 36.0 | 43.6 | 39.4 | 4.48 | 4.89 | 4.64 | 4.72 |
| Specific | ChatGPT (0.5) | 84.5 | 94.8 | 29.9 | 49.0 | 37.2 | 4.57 | 4.94 | 4.71 | 4.81 |

## Turn 4 — document page 6 (rank 4 of 20)

This page discusses the evaluation metrics for citation quality, including the design of [NA] precision and recall, and the alignment score. It mentions that F1-Score is reported on both micro and macro scales in Table 3. However, this page does not contain any tables itself. It only references Table 3 and other tables (Table 4, Table 5, Table 6, Table 7) from previous pages.

## Turn 5 — document page 5 (rank 5 of 20)

This page defines the evaluation metrics for citation quality, including Correctness, Precision, Recall, and F1-Score. It explains how these metrics are calculated and how F1-Score is derived from Precision and Recall. The page also describes the evaluation of text-citation alignment and conscious incompetence, but does not contain any tables. The F1-Score is mentioned as being reported in both micro and macro scales in Table 3, which was referenced in previous pages.

## Turn 6 — document page 15 (rank 6 of 20)

Table 8: Instruction we provide to the human annotators.
This page contains Table 8, which describes the annotation method for human evaluators, but does not contain any table that includes "F1" as a metric.
