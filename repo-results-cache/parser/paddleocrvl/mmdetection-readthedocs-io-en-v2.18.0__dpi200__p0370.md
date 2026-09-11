• anchor_generator (dict) – Config dict for anchor generator

• bbox_coder(dict) – Config of bounding box coder.

• reg_ decoded_bbox (bool) – If true, the regression loss would be applied directly on decoded bounding boxes, converting both the predicted boxes and regression targets to absolute coordinates format. Default False. It should be True when using IoULoss, GIoULoss, or DIoULoss in the bbox head.

• train_cfg(dict) – Training config of anchor head.

• test_cfg(dict) – Testing config of anchor head.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

cls_scores (list[Tensor]): Classification scores for all scale levels, each is a 4D-tensor, the channels number is num_anchors * num_classes.

bbox_pred(list[Tensor]): Box energies / deltas for all scale levels, each is a 4D-tensor, the channels number is num_anchors * 4.

## Return type tuple

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list [Tensor]) – each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single(cls_score, bbox_pred, anchor, labels, label_weights, bbox_targets, bbox_weights,

num\_total\_samples)

Compute loss of a single image.

## Parameters

• cls_score (Tensor) – Box scores for each image Has shape (num_total_anchors, num_classes).