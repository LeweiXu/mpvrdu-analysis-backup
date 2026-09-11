## Turn 1 — document page 4 (rank 1 of 16)

Figure 4: The impact of isolating label words versus randomly isolating non-label words within the first or last 5 layers. Isolating label words within the first 5 layers exerts the most substantial impact, highlighting the importance of shallow-layer information aggregation via label words.

Results and Analysis: Figure 4 illustrates a notable influence on the model's behavior when label words are isolated within the first 5 layers. Yet, this influence becomes inconsequential within the last 5 layers, or when random non-label words are used. This observation underlines the fundamental importance of shallow-layer information aggregation via label words in ICL. It also emphasizes the superiority of label words over non-label words. Further tests with variable numbers of layers reaffirm these findings (Appendix D). Moreover, similar results were obtained when testing ICL with semantically unrelated labels (refer to Appendix F.2).

## Turn 2 — document page 14 (rank 2 of 16)

Figure 12: The impact of isolating label words versus randomly isolating non-label words within the first or last 5 layers. Isolating label words within the first 5 layers exerts a more pronounced effect, highlighting the importance of shallow-layer information aggregation via label words.

## Turn 3 — document page 12 (rank 3 of 16)

Table 5 shows results for a test sample with label “World” from AGNews, comparing “First 5 layers” isolation with “No isolation”. Under “First 5 layers”, the top 5 words in V5 are “\n”, “The”, “Google”, “\endoftext\>”, “A” — mostly non-label words. Under “No isolation”, the top 5 are “World”, “Technology”, “Politics”, “Israel”, “Human” — including the label word “World” and semantically related words. This suggests that isolating non-label words in the first 5 layers leads to a different output distribution than no isolation, implying a measurable impact.

Figure 8 (a) and (b) show label loyalty and word loyalty for GPT2-XL and GPT-J. The chart indicates that isolating label words in shallow layers has a strong effect, while isolating non-label words (light-colored lines) has a much smaller effect compared to label word isolation. The text below Figure 8 states: “Remarkably, isolating label words in the shallow layers significantly influences the outcome, regardless of whether this is compared to isolation in deep layers or to non-label word isolation.” This implies that isolating non-label words has a much smaller impact than isolating label words, but does not state it is “almost no impact”.

The text in section F.2 states: “Figure 12 shows the more pronounced impact of isolating labels in the shallow layers compared to their isolation in the deep layers or the isolation of non-label tokens.” This confirms that isolating non-label tokens has less impact than isolating label tokens, but does not explicitly state it is “almost no impact”.

## Turn 4 — document page 11 (rank 4 of 16)

Table 4 shows demonstration templates and label words for four tasks (SST-2, TREC, AGNews, EmoC). The appendix section D states: "It can be found that isolating shallow layers cause a significant impact, isolating deep layers has a negligible impact on the model, even when the number of isolation layers increases." This refers to isolating layers in general, not specifically non-label words. The text does not explicitly state that isolating non-label words in the last 5 layers has "almost no impact," only that isolating deep layers has negligible impact. Previous pages (Turn 1, Turn 3) indicate that isolating non-label words has a much smaller impact than isolating label words, but do not confirm it is "almost no impact."

## Turn 5 — document page 13 (rank 5 of 16)

Figure 10 (a) and (b) show the effect of different numbers of isolated layers on GPT2-XL and GPT-J, respectively. The plots display "Label Loyalty (First)", "Label Loyalty (Last)", "Word Loyalty (First)", and "Word Loyalty (Last)". In both figures, the "Word Loyalty (Last)" line (red dashed) remains very close to 0.0 across all isolation layer numbers, indicating that isolating non-label words in the last 5 layers has minimal impact on word loyalty. The "Label Loyalty (Last)" line (blue dashed) also remains relatively low, but the "Word Loyalty (Last)" line is consistently near zero, suggesting almost no impact.

## Turn 6 — document page 2 (rank 6 of 16)

Figure 2: Illustration of the hypothesis that in shallow layers, label words gather information from demonstrations to form semantic representations for deeper processing, while deep layers extract and utilize this information from label words to formulate the final prediction.

The text describes a hypothesis about information flow in ICL: label words aggregate information in shallow layers and are used for final prediction in deep layers. It mentions experiments to validate this, including blocking the information aggregation path to label words, which significantly impairs performance in shallow layers. However, this page does not contain any information about the impact of randomly isolating non-label words within the last 5 layers.
