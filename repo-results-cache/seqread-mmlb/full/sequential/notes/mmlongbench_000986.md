## Turn 1 — document page 16 (rank 1 of 16)

Figure 14 displays six predicted confusion matrices for different values of M (5, 10, 20, 50, 100, 200). Each matrix shows the confusion between six categories: Abbreviation, Entity, Description, Person, Location, and Number. The values in the matrices represent the degree of confusion (likely a correlation or similarity score) between categories, with 1.0 indicating perfect confusion and -0.4 indicating low confusion. The matrices are color-coded, with darker shades indicating higher confusion.

## Turn 2 — document page 8 (rank 2 of 16)

Figure 6: Predicted and real confusion matrix on TREC. We set undefined diagonals to 1 for better visualization. The heatmaps display similarity in confusing category pairs, particularly in lighter-colored blocks.

(a) Confusion matrix of Confusion \( _{ij}^{pred} \).
(b) Confusion matrix of Confusion \( _{ij} \).

In the confusion matrices, the categories are: Abbreviation, Entity, Description, Person, Location, and Number. The values represent the degree of confusion, with 1.0 indicating perfect confusion and lower values indicating less confusion. The most confusing pair is identified as Description-Entity. The text also states that the method performs reasonably well for highly confusing categories, specifically Entity-Abbreviation and Description-Abbreviation.

## Turn 3 — document page 11 (rank 3 of 16)

Table 4 lists the label words for the TREC task as: Abbreviation, Entity, Description, Person, Location, Number. This confirms the categories used in the confusion matrices discussed in earlier pages.

## Turn 4 — document page 3 (rank 4 of 16)

This page discusses attention mechanisms and quantitative metrics (S_wp, S_pq, S_ww) for analyzing information flow in models during In-Context Learning (ICL). It mentions that in the TREC dataset, the term 'label words' is approximately equal to 'label tokens', with the only deviation being 'Abbreviation', where the first subword is used. The page also lists datasets used in experiments, including TREC for question type classification. However, it does not contain any new information about the confusion between categories or the most confusing category of Abbreviation.

## Turn 5 — document page 15 (rank 5 of 16)

This page describes the calculation of the Confusion metric, which quantifies the degree of confusion between two categories i and k. It explains how to compute this metric using the Area Under the Receiver Operating Characteristic Curve (AUC-ROC) of a classifier that predicts the probabilities for the two categories. The page also mentions that the Confusion metric is bounded between 0 and 1, with values closer to 1 indicating less confusion. The page references Figure 14, which depicts the prediction confusion matrix for different values of M, and states that M=10 was chosen for computation. However, this page does not contain any information about which category is the most confusing for Abbreviation.

## Turn 6 — document page 7 (rank 6 of 16)

This page contains tables (Table 1 and Table 2) comparing different methods for In-Context Learning (ICL) on various datasets including TREC, SST-2, AGNews, and EmoC. It discusses methods like Vanilla ICL, Anchor Re-weighting, Text_anchor, Hidden_random, and Hidden_anchor. The tables show metrics such as accuracy, label loyalty, and word loyalty. The text mentions that omitting formatting information leads to the model favoring common tokens like “the” over label words, indicating confusion about the expected output type. However, this page does not contain any information about the confusion between categories or the most confusing category of Abbreviation.

## Turn 7 — document page 12 (rank 7 of 16)

This page contains Table 5, which shows results for a test sample with the label “World” from AGNews. It compares the output label words when using “First 5 layers” isolation versus “No isolation”. The table lists the top 5 predicted tokens sorted by probability. The page also includes Figure 8, which charts the effect of different numbers of isolated layers on GPT2-XL and GPT-J, showing variations in label loyalty and word loyalty. The text emphasizes the important role of information aggregation via label words in the shallow layers. The page discusses the calculation of AUCROC_l and presents additional experimental results (F.1 and F.2) for ICL with more demonstrations and semantically-unrelated labels. However, this page does not contain any information about the confusion between categories or the most confusing category of Abbreviation.
