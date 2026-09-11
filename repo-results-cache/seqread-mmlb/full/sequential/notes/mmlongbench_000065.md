## Turn 1 — document page 7 (rank 1 of 20)

| Model        | Align. | Corr. | Micro Prec. | Micro Rec. | Micro F1. | Macro Prec. | Macro Rec. | Macro F1. |
|--------------|--------|-------|-------------|------------|-----------|-------------|------------|-----------|
| GPT-4 (0.5)  | 92.0_(1.5) | 97.6_(0.1) | 36.0_(0.6) | 43.6_(1.0) | 39.4      | 40.7_(1.1) | 43.9_(1.0) | 42.3      |
| ChatGPT (0.1)| 85.9_(2.5) | 96.1_(0.4) | 29.0_(0.0) | 50.8_(0.3) | 36.9      | 32.7_(0.4) | 51.2_(0.3) | 39.9      |
| ChatGPT (0.5)| 84.5_(1.1) | 94.8_(0.2) | 29.9_(0.2) | 49.0_(0.8) | 37.2      | 34.1_(0.5) | 49.4_(0.9) | 40.4      |
| ChatGPT (0.9)| 84.1_(0.5) | 94.2_(0.4) | 28.7_(0.2) | 49.0_(0.3) | 36.2      | 32.5_(0.2) | 49.4_(0.3) | 39.2      |
| Alpaca-7B    | 46.9_(0.9) | 78.9_(0.6) | 14.9_(1.4) | 19.4_(0.2) | 16.8      | 19.8_(0.4) | 19.9_(0.3) | 19.8      |
| LLaMA-7B     | 47.8_(0.8) | 70.2_(0.2) | 7.7_(2.4)  | 41.1_(0.7) | 13.0      | 11.0_(1.9) | 41.4_(0.7) | 17.4      |
| LLaMA-13B    | 62.1_(0.4) | 71.7_(1.9) | 10.5_(3.3) | 43.7_(1.0) | 16.9      | 13.8_(2.2) | 43.5_(1.0) | 20.9      |
| Vicuna-13B   | 66.9_(0.1) | 59.0_(0.6) | 14.9_(0.2) | 16.8_(0.0) | 15.8      | 15.1_(0.0) | 17.0_(0.0) | 16.0      |

Table 3: Citation Quality OpenAI models and LLaMA family models. The first five metrics are reported in Micro, and the last three metrics are reported in Macro. We also report text citation alignment.
The experimental results are the mean of three runs, and the standard deviation is reported in brackets.
In general, there is a room of improvement for all models since no model can achieve a micro F1 Score of higher than 40. The OpenAI models outperform the LLaMA family models in almost all metrics. The correctness is above 94 for OpenAI models, but around 70 for LLaMA based models. For ChatGPT, temperature does not play a significant role since it effect on F1 Score is at most 1.2. The GPT-4 model achieves the best performance across almost all metrics, except for recall, since GPT-4 models tend to generate shorter answers with fewer citations, resulting in higher precision. While LLaMA is better at Recall by generating long answers with many citations. The F1-Score of models from the same family are close to one another, showing that our automatic evaluation metric designed is reliable.

Text-Citation Alignment From Table 3, similar

## Turn 2 — document page 8 (rank 2 of 20)

Figure 4: Precision, Recall, and F1-Score for [NA]. The recall is stable at about 15 regardless of the number of absent knowledge. This indicates that the current LLMs have ability to identify absent knowledge to a limited extent. While precision and F1-Score exhibit a clear upward trend, which shows that with more absent knowledge in KG, [NA] enables generated outputs to locate absent knowledge more accurately. Therefore, the “Conscious Incompetence” setting plays an increasingly crucial role when the coverage problem of knowledge graph is more serious.

5.3 Retrieval Analysis
We conduct an ablation study to examine the impact of retrieval accuracy on the model's output. The experiment simulates retrieval accuracy from 100 to 20 at intervals of 20. We start with the ground truth knowledge graphs that we used for question construction. In each subsequent rounds, we randomly replace additional 20% knowledge graphs with irrelevant knowledge graphs to simulate retrieving wrong graphs. The results for citation quality are in Figure 5. Answers are generated using ChatGPT with a temperature of 0.5.

The results show clear downward trends in all metrics as expected when retrieval accuracy dropped. Among precision and recall, the impact of poor retrieval quality on recall (green) is much more significant than on precision (yellow). This indicates that the model has the ability to filter out incorrect knowledge to a certain extent, resulting in less noticeable impact on precision compared to recall. The reduction in recall was nearly linear as retrieval accuracy decreased, which is understandable since a knowledge cannot be cited if it is not provided. The greatest drop in recall occurred between the ground truth (57.1) and 80 accuracy (42.5), demonstrating the potential of the model to generate high-quality citations under perfect retrieval conditions. In practice, a retrieval accuracy of 80 is closest to the actual scenario of our experiment (our retrieval accuracy is 75.9). Therefore, when retrieval accuracy is reasonably high, the correctness of citations is not the most significant concern compared to recall.

Figure 5: Citation evaluation (Micro) of generated texts using knowledge graphs with retrieval accuracy 100 (gold), 80, 60,40, and 20.

Table 6: Result of Human Evaluation on text-citation alignment
| Model        | Alignment | Human Avg. |
|--------------|-----------|------------|
| ChatGPT(0.5) | 84.5      | 82.0       |
| LLaMA-7B     | 47.8      | 45.5       |
| Vicuna-13B   | 66.9      | 64.5       |

5.4 Human Evaluation
We conduct human evaluation to verify the correlation between automatic evaluation and human judgment. We randomly sample 100 sentence-citation pairs from each of the three baselines: ChatGPT (temperature 0.5), LLaMA-7B, and Vicuna-13B. We request two proficient English annotators for each baseline to determine if the citation aligns to the sentence and provides support for it. The reason we choose metric alignment here is in appendix C, with instruction to annotators and IAA.

The comparison between automatically calculated Alignment and human evaluation results is shown in Table 6. For all three baselines, the automatic and human scores are close with a gap within 2.5, despite the significant differences among the baselines. This indicates a strong correlation between the automatically calculated alignment and human judgments. The experiment results demonstrate that the automatic evaluation serves as a reli-

## Turn 3 — document page 6 (rank 3 of 20)

none

## Turn 4 — document page 9 (rank 4 of 20)

Table 7: Comparison of evaluation results on General and Specific question setting
| Setting | Model | Align. | Corr. | Prec. | Rec. | F1. | Coh. | Con. | Flu. | Rel. |
|---------|-------|--------|-------|-------|------|-----|------|------|------|------|
| General | GPT-4 (0.5) | 90.9 | 97.6 | 30.8 | 42.1 | 35.6 | 4.38 | 4.77 | 4.48 | 4.48 |
| General | ChatGPT (0.5) | 82.7 | 94.5 | 25.2 | 47.4 | 32.9 | 4.64 | 4.89 | 4.45 | 4.70 |
| Specific | GPT-4 (0.5) | 92.0 | 97.6 | 36.0 | 43.6 | 39.4 | 4.48 | 4.89 | 4.64 | 4.72 |
| Specific | ChatGPT (0.5) | 84.5 | 94.8 | 29.9 | 49.0 | 37.2 | 4.57 | 4.94 | 4.71 | 4.81 |

## Turn 5 — document page 14 (rank 5 of 20)

none

## Turn 6 — document page 13 (rank 6 of 20)

none

## Turn 7 — document page 23 (rank 7 of 20)

Table 19 shows an example of an attributed answer generated by ChatGPT with a temperature of 0.5. The retrieved knowledge includes Stephen Crane's notable works ("The Red Badge of Courage"), his atheistic views on religion, his attendance at Syracuse University, and his membership in the Syracuse Orange baseball team. The generated output incorporates this information, stating that his experiences at Syracuse University influenced his writing and that he wrote "The Eighty-Yard Run" based on his football experiences there.

## Turn 8 — document page 4 (rank 8 of 20)

none

## Turn 9 — document page 10 (rank 9 of 20)

none
