## Return type Tensor

get_targets(anchor_list, valid_flag_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None,

gt_labels_list=None, label_channels=1, unmap_outputs=True)

Get targets for PAA head.

This method is almost the same as AnchorHead.get_targets(). We direct return the results from _get_targets_single instead of map it to levels by images_to_levels function.

## Parameters

• anchor_list (list[list[Tensor]]) – Multi level anchors of each image. The outer list indicates images, and the inner list corresponds to feature levels of the image. Each element of the inner list is a tensor of shape (num_ర్చన, 4).

• valid_flag_list (list[list[Tensor]]) – Multi level valid flags of each image. The outer list indicates images, and the inner list corresponds to feature levels of the image. Each element of the inner list is a tensor of shape (num_anchors,)

• gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.

• img_metas (list[dict]) – Meta info of each image.

• gt_bboxes_ignore_list (list[Tensor]) – Ground truth bboxes to be ignored.

• gt_labels_list (list[Tensor]) – Ground truth labels of each box.

• label channels (int) – Channel of label.

• unmap outputs (bool) – Whether to map outputs back to the original set of anchors.

## Returns

Usually returns a tuple containing learning targets.

• labels (list[Tensor]): Labels of all anchors, each with shape (num_anchors,).

• label_weights (list[Tensor]): Label weights of all anchors. each with shape (num_anchors,).

• bbox_targets (list[Tensor]): BBox targets of all anchors. each with shape (num_anchors, 4).

• bbox_weights (list[Tensor]): BBox weights of all anchors. each with shape (num_anchors, 4).

• pos_inds (list[Tensor]): Contains all index of positive sample in all anchor.

• gt_inds (list[Tensor]): Contains all gt_index of positive sample in all anchor.

## Return type tuple

## gmm_separation_scheme(gmm_assignment, scores, pos_inds_gmm)

A general separation scheme for gmm model.

It separates a GMM distribution of candidate samples into three parts, 0 1 and uncertain areas, and you can implement other separation schemes by rewriting this function.

## Parameters

- gmm_assignment (Tensor) – The prediction of GMM which is of shape (num_samples,). The 0/1 value indicates the distribution that each sample comes from.

- scores (Tensor) – The probability of sample coming from the fit GMM distribution. The tensor is of shape (num_samples,).