## Turn 1 — document page 7 (rank 1 of 16)

Table 1: The effect after adding parameter  \( \beta_{0}^{i} \). For AGNews, due to the length limit, we only use three demonstrations per class. Our Anchor Re-weighting method achieves the best performance overall tasks.
Table 2: Results of different compression methods on GPT2-XL and GPT-J (averaged over SST-2, TREC, AGNews, and EmoC). Acc. denotes accuracy. The best results are shown in bold. Our method achieves the best compression performance.
Table 3: Results of different compression methods on GPT2-XL and GPT-J (averaged over SST-2, TREC, AGNews, and EmoC). Acc. denotes accuracy. The best results are shown in bold. Our method achieves the best compression performance.
Text: The Textanchor method is included to demonstrate that the effectiveness of Hiddenanchor is attributed to the aggregation of information in label words, rather than the mere text of label words. If we find that Hiddenanchor surpasses Textanchor in performance, it solidifies the notion that the aggregated information within label words carries significant importance. The Hiddenrandom method is introduced to illustrate that anchor hidden states encapsulate most of the demonstration information among all hidden states.
Text: We assess all compression methods using the label loyalty and word loyalty introduced in § 2.2, in addition to classification accuracy.
Text: We can see from Table 2 that the proposed compression method Hiddenanchor achieves the best results among all three compression methods on all metrics and for both models. For example, with the GPT-J model, the compression method with anchor states only leads to a 1.5 accuracy drop compared to the uncompressed situation, indicating that the compression introduces negligible information loss. Further, we estimate the efficiency improvements over the original ICL. As shown in Table 3, the speed-up ratio ranges from  \( 1.1 \times \)  to  \( 2.9 \times \) , as the efficiency gain is influenced by the length of the demonstrations. We refer readers to Appendix I for
Text: Omitting formatting significantly reduces accuracy, as the model will favor common tokens like “the” over label words, indicating confusion about the expected output type.
Text: Here, “formatting” refers to elements like “Review:” and “Sentiment:” in Figure 2.

## Turn 2 — document page 6 (rank 2 of 16)

This page introduces the "Anchor-Only Context Compression" technique, which reduces the full demonstration to anchor hidden states to accelerate ICL inference. It explains the method and its motivation based on the observation that model output heavily relies on label words. However, this page does not contain any specific numerical results or speed-up ratios for GPT2-XL on AGNews. The speed-up ratio information is mentioned in the previous page (page 7) and is not repeated or contradicted here.

## Turn 3 — document page 5 (rank 3 of 16)

This page discusses experiments on GPT2-XL and GPT-J models, analyzing the correlation between attention distributions on label words and model predictions. It presents Figures 5a and 5b, which show that for GPT2-XL (48 layers), the AUC-ROC metric (AUCROC_l) for deep layers approaches 0.8, indicating a strong correlation. The cumulative contribution R_l increases significantly in middle and deep layers. The results are averaged over SST-2, TREC, AGNews, and Emoc datasets. The page introduces the concept of "Anchors" and proposes applications to boost ICL accuracy and inference speed, including context compression to speed up inference. However, this page does not contain any specific numerical speed-up ratios for GPT2-XL on AGNews.

## Turn 4 — document page 14 (rank 4 of 16)

Table 6: Acceleration ratios, \( L_{demo} \) and \( L_{x} \).
| | SST-2 | TREC | AGNews | EmoC |
|---|---|---|---|---|
| GPT2-XL | 1.1× | 1.5× | 2.5× | 1.4× |
| GPT-J | 1.5× | 2.2× | 2.9× | 1.9× |
| \( L_{demo} \) | 18 | 61 | 151 | 53 |
| \( L_x \) | 19 | 7 | 37 | 12 |

## Turn 5 — document page 8 (rank 5 of 16)

Table 3: Acceleration ratios of the Hidden_anchor method.
| Model | SST-2 | TREC | AGNews | EmoC |
|---|---|---|---|---|
| GPT2-XL | 1.1× | 1.5× | 2.5× | 1.4× |
| GPT-J | 1.5× | 2.2× | 2.9× | 1.9× |

## Turn 6 — document page 13 (rank 6 of 16)

This page contains Figure 9 and Figure 10, which show variations in label loyalty and word loyalty across different datasets (SST-2, TREC, AGNews, EmoC) and model configurations (GPT2-XL, GPT-J). Figure 9(c) specifically shows results for the AGNews dataset, but it does not contain any numerical speed-up ratios. Figure 10 shows the effect of different numbers of isolated layers on label and word loyalty for GPT2-XL and GPT-J, but again, no speed-up ratios are provided. The text discusses anchor re-weighting implementation but does not mention any speed-up values for GPT2-XL on AGNews.
