loss(cls_scores, bbox_preds, centernesses, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

• centernesses (list[Tensor]) – Centerness for each scale level with shape (N, num_anchors * 1, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (list[Tensor] / None) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single( anchors, cls_score, bbox_pred, centerness, labels, label_weights, bbox_targets,

num\_total\_samples)

Compute loss of a single scale level.

## Parameters

• cls_score (Tensor) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W).

• bbox_pred (Tensor) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W).

• anchors (Tensor) – Box reference for each scale level with shape (N, num_total_anchors, 4).

• labels (Tensor) – Labels of each anchor with shape (N, num_total_anchors).

• label_weights (Tensor) – Label weights of each anchor with shape (N, num_total_anchors)

• bbox_targets (Tensor) – BBox regression targets of each anchor weight shape (N, num_total_anchors, 4).

• num_total_samples (int) – Number of positive samples that is reduced over all GPUs.

Returns A dictionary of loss components.

Return type dict[str, Tensor]