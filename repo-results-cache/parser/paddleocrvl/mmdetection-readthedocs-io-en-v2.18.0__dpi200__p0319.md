Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

center predict heatmaps for all levels, the channels number is num\_classes.

wh_pred(List[Tensor]): wh predicts for all levels, the channels number is 2.

offset_preds (List[Tensor]): offset predicts for all levels, the channels number is 2.

Return type center_heatmap_preds (List[Tensor])

## forward_single(feat)

Forward feature of a single level.

Parameters feat (Tensor) – Feature of a single level.

## Returns

center predict heatmaps, the channels number is num\_classes.

wh_pred (Tensor): wh predicts, the channels number is 2. offset_pred (Tensor): offset predicts, the channels number is 2.

Return type center_heatmap_pred (Tensor)

get_bboxes(center_heatmap_preds, wh_preds, offset_preds, img_metas, rescale=True, with_nms=False)

Transform network output for a batch into bbox predictions.

## Parameters

- center_heatmap_preds (list[Tensor]) – Center predict heatmaps for all levels with shape (B, num_classes, H, W).

• wh_preds (list[Tensor]) – WH predicts for all levels with shape (B, 2, H, W).

• offset_preds (list [Tensor]) – Offset predicts for all levels with shape (B, 2, H, W).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If True, return boxes in original image space. Default: True.

• with_nms (bool) – If True, do nms before return boxes. Default: False.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where 5 represent  $ (tl\_x, tl\_y, br\_x, br\_y, score) $ and the score between 0 and 1. The shape of the second tensor in the tuple is  $ (n,) $, and each element represents the class label of the corresponding box.

Return type list[tuple[Tensor, Tensor]]

get_targets(gt_bboxes, gt_labels, feat_shape, img_shape)

Compute regression and classification targets in multiple images.

## Parameters

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box.

• feat_shape (list[int]) – feature map shape with value [B, _, H, W]

• img_shape (list[int]) – image shape in [h, w] format.