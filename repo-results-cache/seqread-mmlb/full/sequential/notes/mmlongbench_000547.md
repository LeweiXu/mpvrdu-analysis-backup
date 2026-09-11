## Turn 1 — document page 13 (rank 1 of 20)

Table 4: Effect of loss components on AP. We train two models turning off  \( \ell_{1} \)  loss, and GIoU loss, and observe that  \( \ell_{1} \)  gives poor results on its own, but when combined with GIoU improves  \( AP_{M} \)  and  \( AP_{L} \) . Our baseline (last row) combines both losses.
| class | \( \ell_1 \) | GIoU | AP | \( \Delta \) | \( AP_{50} \) | \( \Delta \) | \( AP_S \) | \( AP_M \) | \( AP_L \) |
|---|---|---|---|---|---|---|---|---|---|
| √ | √ | √ | 40.6 | - | 61.6 | - | 19.9 | 44.3 | 60.2 |
| √ | √ |  | 39.9 | -0.7 | 61.6 | 0 | 19.9 | 43.2 | 57.9 |
| √ |  | √ | 35.8 | -4.8 | 57.3 | -4.4 | 13.7 | 39.8 | 57.9 |

## Turn 2 — document page 9 (rank 2 of 20)

Table 1 on page 9 shows results for DETR models on the COCO validation set. The row for "DETR" (baseline) shows an AP50 value of 62.4. The question asks for the AP50 value of DETR with L1 loss and without GIoU loss. The current page does not specify which DETR model corresponds to this configuration. However, the previous page (page 13) showed that when GIoU loss is removed, the AP50 remains 61.6, which is consistent with the baseline DETR model shown on page 9 (AP50=62.4) if we assume the baseline includes L1 loss. The current page does not contradict the previous answer.

## Turn 3 — document page 12 (rank 3 of 20)

Table 4 on page 13 (referenced in the text) shows the effect of loss components on AP. The row with L1 loss and without GIoU loss (second row) shows an AP50 value of 61.6. This page confirms the ablation study setup and references Table 4, but does not contain new data contradicting or correcting the AP50 value of 61.6 for the specified configuration.

## Turn 4 — document page 10 (rank 4 of 20)

Table 2 on page 10 shows the effect of encoder size on DETR model performance. The row with 6 encoder layers (and fixed 6 decoder layers) shows an AP50 value of 61.6. This configuration is described in the text as the model used for ablation studies (41.3M parameters, 6 encoder, 6 decoder layers, width 256). This matches the configuration described in previous pages (page 13, Table 4) as the one with L1 loss and without GIoU loss, which also had an AP50 of 61.6. The current page confirms this value for the same model configuration.

## Turn 5 — document page 23 (rank 5 of 20)

This page discusses training hyperparameters, including the use of L1 and GIoU losses with specific weights (λ_L1=5, λ_iou=2), and describes the baseline model which uses GIoU loss along with standard L1 loss. It also mentions that the baseline uses only GIoU loss with weights 20 and 1 for box and proposal regression tasks respectively. However, this page does not contain any table or direct measurement of AP50 values for the specific configuration of DETR with L1 loss and without GIoU loss. The page confirms the loss combination used in the baseline model but does not contradict or correct the previously recorded AP50 value of 61.6 for the specified configuration.

## Turn 6 — document page 16 (rank 6 of 20)

Table 5 on page 16 shows results for DETR models on the COCO validation set. The row for "DETR" (with R50 backbone) shows an AP value of 31.1. This is the mask AP (computed on the things classes) before any panoptic post-treatment. The table does not provide an AP50 value for this model. The previous answer of 61.6 was for a different metric (AP50) from a different configuration (L1 loss without GIoU loss) as shown in Table 4 on page 13. This page does not contradict or correct the previous answer for the specific question.
