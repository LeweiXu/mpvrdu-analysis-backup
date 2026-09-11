## Turn 1 — document page 6 (rank 1 of 16)

none

## Turn 2 — document page 7 (rank 2 of 16)

| Method | SST-2 | TREC | AGNews | EmoC | Average |
|---|---|---|---|---|---|
| Vanilla In-Context Learning (1-shot per class) | 61.28 | 57.56 | 73.32 | 15.44 | 51.90 |
| Vanilla In-Context Learning (5-shot per class) | 64.75 | 60.40 | 52.52 | 9.80 | 46.87 |
| Anchor Re-weighting (1-shot per class) | 90.07 | 60.92 | 81.94 | 41.64 | 68.64 |

Table 1: The effect after adding parameter  β₀ⁱ. For AGNews, due to the length limit, we only use three demonstrations per class. Our Anchor Re-weighting method achieves the best performance overall tasks.

## Turn 3 — document page 2 (rank 3 of 16)

The text on this page states: "An anchor re-weighting method is introduced, which employs a learnable vector to adjust the significance of different label words in demonstrations, leading to a 16.7% average accuracy boost compared to standard ICL baselines."

## Turn 4 — document page 5 (rank 4 of 16)

none

## Turn 5 — document page 1 (rank 5 of 16)

none

## Turn 6 — document page 9 (rank 6 of 16)

This page contains the conclusion and limitations sections of the paper. It reiterates that an anchor re-weighting method is proposed to improve ICL accuracy and that experimental results support the hypothesis that label words serve as anchors. However, it does not provide any new quantitative data or specific performance metrics for the anchor re-weighting method beyond what was already presented in earlier pages.

## Turn 7 — document page 8 (rank 7 of 16)

Table 3 shows acceleration ratios for the Hidden_anchor method on SST-2, TREC, AGNews, and EmoC datasets for GPT2-XL and GPT-J models. The table does not contain any information about the Anchor Re-weighting method or its performance improvement over vanilla ICL. The text discusses error diagnosis using anchor distances and confusion matrices, but does not provide new quantitative data on the performance improvement of the Anchor Re-weighting method.
