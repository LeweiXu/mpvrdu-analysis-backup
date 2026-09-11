## get_fcos_targets(points, gt_bboxes_list, gt_labels_list)

Compute FCOS regression and classification targets for points in multiple images.

## Parameters

• points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

- gt_labels_list (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

Returns labels (list[Tensor]): Labels of each level. label_weights: None, to be compatible with ATSS targets. bbox_targets (list[Tensor]): BBox targets of each level. bbox_weights: None, to be compatible with ATSS targets.

## Return type tuple

## get_targets(cls_scores, mlvl_points, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore)

A wrapper for computing ATSS and FCOS targets for points in multiple images.

## Parameters

• cls_scores (list[Tensor]) – Box iou-aware scores for each scale level with shape (N, num_points * num_classes, H, W).

- mlvI_points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

• gt_labels (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / Tensor) – Ground truth bboxes to be ignored, shape (num_ignored_gts, 4).

## Returns

labels_list (list[Tensor]): Labels of each level. label_weights (Tensor/None): Label weights of all levels. bbox_targets_list (list[Tensor]): Regression targets of each

level, (l, t, r, b).

bbox_weights (Tensor/None): Bbox weights of all levels.

## Return type tuple

loss(cls_scores, bbox_preds, bbox_preds_refine, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box iou-aware scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box offsets for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

• bbox_preds_refine (list [Tensor]) – Refined Box offsets for each scale level, each is a 4D-tensor, the channel number is num_points * 4.