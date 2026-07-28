## Parameters

• cls_scores (list[Tensor]) – Classification scores at all fpn levels. Each tensor is in shape (N, num_classes * num_anchors, H, W)

• labels_list (list[Tensor]) – The label that each anchor is assigned to. Shape (N * H * W * num_anchors,)

• pos_inds (list[Tensor]) – List of bool tensors indicating whether the anchor is assigned to a positive label. Shape (N * H * W * num_anchors,)

Returns A single float number indicating the positive recall.

Return type Tensor

collect_loss_level_single(cls_loss, reg_loss, assigned_gt_inds, labels_seq)

Get the average loss in each FPN level w.r.t. each gt label.

## Parameters

• cls_loss (Tensor) – Classification loss of each feature map pixel, shape (num_anchor, num_class)

• reg_loss (Tensor) – Regression loss of each feature map pixel, shape (num_anchor, 4)

- assigned_gt_inds (Tensor) – It indicates which gt the prior is assigned to (0-based, -1: no assignment). shape (num_anchor),

• labels_seq – The rank of labels. shape (num_gt)

Returns (num_gt), average loss of each gt in this level

Return type shape

## forward_single(x)

Forward feature map of a single scale level.

Parameters x (Tensor) – Feature map of a single scale level.

## Returns

cls_score (Tensor): Box scores for each scale level Has shape (N, num_points * num_classes, H, W).

bbox_pred (Tensor): Box energies / deltas for each scale level with shape  $ (N, $ num_points * 4, H, W).

Return type tuple (Tensor)

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_points * num_classes, H, W).

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_points * 4, H, W).

- gt_bboxes (list [Tensor]) – each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.