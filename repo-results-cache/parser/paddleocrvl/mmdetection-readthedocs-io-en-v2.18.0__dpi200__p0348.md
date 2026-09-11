## Returns

Usually a tuple of classification scores and bbox prediction

cls_scores (list[Tensor]): Classification and quality (IoU) joint scores for all scale levels, each is a 4D-tensor, the channel number is num_classes.

bbox_pred(list[Tensor]): Box distribution logits for all scale levels, each is a 4D-tensor, the channel number is  $ 4*(n+1) $, n is max value of integral set.

Return type tuple

forward_single(x, scale)

Forward feature of a single scale level.

## Parameters

• x (Tensor) – Features of a single scale level.

•  $ (scale) - obj: mmcv.cnn.Scale $: Learnable scale module to resize the bbox prediction.

## Returns

cls_score (Tensor): Cls and quality joint scores for a single scale level the channel number is num_classes.

bbox_pred (Tensor): Box distribution logits for a single scale level, the channel number is  $ 4*(n+1) $, n is max value of integral set.

Return type tuple

get_targets(anchor_list, valid_flag_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None, gt_labels_list=None, label_channels=1, unmap_outputs=True)

Get targets for GFL head.

This method is almost the same as AnchorHead.get_targets(). Besides returning the targets as the parent method does, it also returns the anchors as the first element of the returned tuple.

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Cls and quality scores for each scale level has shape (N, num_classes, H, W).

• bbox_preds (list [Tensor]) – Box distribution logits for each scale level with shape (N, 4*(n+1), H, W), n is max value of integral set.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (list[Tensor] / None) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single(anchors, cls_score, bbox_pred, labels, label_weights, bbox_targets, stride, num_total_samples) Compute loss of a single scale level.