• gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.

• img_metas (list[dict]) – Meta info of each image.

• gt_bboxes_ignore_list (list[Tensor]) – Ground truth bboxes to be ignored.

• gt_labels_list (list[Tensor]) – Ground truth labels of each box.

• label channels (int) – Channel of label.

• unmap outputs (bool) – Whether to map outputs back to the original set of anchors.

## Returns

Usually returns a tuple containing learning targets.

• batch_labels (Tensor): Label of all images. Each element of is a tensor of shape (batch, h * w * num_anchors)

• batch_label_weights (Tensor): Label weights of all images of is a tensor of shape (batch, h * w * num_anchors)

• num_total_pos (int): Number of positive samples in all images.

• num_total_neg (int): Number of negative samples in all images.

## additional returns: This function enables user-defined returns from

self._get_targets_single. These returns are currently refined to properties at each feature map (i.e. having HxW dimension). The results will be concatenated after the end

Return type tuple

## init_weights()

Initialize the weights.

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (batch, num_anchors * num_classes, h, w)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (batch, num_anchors * 4, h, w)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None

Returns A dictionary of loss components.

Return type dict[str, Tensor]