get_neg_loss_single(cls_score, objectness, gt_labels, ious, inside_gt_bbox_mask)

Calculate the negative loss of all points in feature map.

## Parameters

• cls_score (Tensor) – All category scores for each point on the feature map. The shape is (num_points, num_class).

• objectness (Tensor) – Foreground probability of all points and is shape of (num_points, 1).

• gt_labels (Tensor) – The zeros based label of all gt with shape of (num_gt).

- ious (Tensor) – Float tensor with shape of (num_points, num_gt). Each value represents the iou of pred_bbox and gt_bboxes.

• inside_gt_bbox_mask (Tensor) – Tensor of bool type, with shape of (num_points, num_gt), each value is used to mark whether this point falls within a certain gt.

## Returns

• neg_loss (Tensor): The negative loss of all points in the feature map.

## Return type tuple[Tensor]

get_pos_loss_single(cls_score, objectness, reg_loss, gt_labels, center_prior_weights)

Calculate the positive loss of all points in gt\_bboxes.

## Parameters

• cls_score (Tensor) – All category scores for each point on the feature map. The shape is (num_points, num_class).

• objectness (Tensor) – Foreground probability of all points, has shape (num_points, 1).

• reg_loss (Tensor) – The regression loss of each gt_bbox and each prediction box, has shape of (num_points, num_gt).

• gt_labels (Tensor) – The zeros based gt_labels of all gt with shape of (num_gt,).

• center_prior_weights (Tensor) – Float tensor with shape of (num_points, num_gt). Each value represents the center weighting coefficient.

## Returns

• pos_loss (Tensor): The positive loss of all points in the gt_bboxes.

Return type tuple[Tensor]

## get_targets(points, gt_bboxes_list)

Compute regression targets and each point inside or outside gt_bbox in multiple images.

## Parameters

• points (list[Tensor]) – Points of all fpn level, each has shape (num_points, 2).

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

## Returns

• inside_gt_bbox_mask_list (list[Tensor]): Each Tensor is with bool type and shape of (num_points, num_gt), each value is used to mark whether this point falls within a certain gt.

• concat_lvI_bbox_targets (list[Tensor]): BBox targets of each level. Each tensor has shape (num_points, num_gt, 4).