• pos_inds_gmm (Tensor) – All the indexes of samples which are used to fit GMM model. The tensor is of shape (num_samples,)

## Returns

The indices of positive and ignored samples.

• pos_inds_temp (Tensor): Indices of positive samples.

• ignore_inds_temp (Tensor): Indices of ignore samples.

Return type tuple[Tensor]

loss(cls_scores, bbox_preds, iou_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

• iou_preds (list[Tensor]) – iou_preds for each scale level with shape (N, num_anchors * 1, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (list[Tensor] | None) – Specify which bounding boxes can be ignored when are computing the loss.

Returns A dictionary of loss gmm assignment.

Return type dict[str, Tensor]

paa_reassign(pos_losses, label, label_weight, bbox_weight, pos_inds, pos_gt_inds, anchors)

Fit loss to GMM distribution and separate positive, ignore, negative samples again with GMM model.

## Parameters

• pos_losses (Tensor) – Losses of all positive samples in single image.

• label (Tensor) – classification target of each anchor with shape (num_anchors,)

• label_weight (Tensor) – Classification loss weight of each anchor with shape (num_anchors).

• bbox_weight (Tensor) – Bbox weight of each anchor with shape (num_anchors, 4).

• pos_inds (Tensor) – Index of all positive samples got from first assign process.

• pos_gt_inds (Tensor) – Gt_index of all positive samples got from first assign process.

• anchors (list [Tensor]) – Anchors of each scale.

## Returns

Usually returns a tuple containing learning targets.

• label (Tensor): classification target of each anchor after paa assign, with shape (num_anchors,)