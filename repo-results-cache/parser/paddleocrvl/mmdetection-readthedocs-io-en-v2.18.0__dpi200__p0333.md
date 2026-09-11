- gt_bboxes_list (list[Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

- gt_labels_list (list[Tensor]) – Ground truth class indices for each image with shape (num_gts, ).

• img_metas (list[dict]) – List of image meta information.

- gt_bboxes_ignore_list (list[Tensor], optional) – Bounding boxes which can be ignored for each image. Default None.

## Returns

a tuple containing the following targets.

• labels_list (list[Tensor]): Labels for all images.

• label_weights_list (list[Tensor]): Label weights for all images.

• bbox targets list (list[Tensor]): BBox targets for all images.

• bbox_weights_list (list[Tensor]): BBox weights for all images.

• num_total_pos (int): Number of positive samples in all images.

• num_total_neg (int): Number of negative samples in all images.

Return type tuple

## init_weights()

Initialize weights of the transformer head.

loss(all_cls_scores_list, all_bbox_preds_list, gt_bboxes_list, gt_labels_list, img_metas,

gt_bboxes_ignore=None)

“Loss function.”

Only outputs from the last feature level are used for computing losses by default.

## Parameters

• all_cls_scores_list (list[Tensor]) – Classification outputs for each feature level. Each is a 4D-tensor with shape [nb_dec, bs, num_query, cls_out_channels].

• all_bbox_preds_list (list[Tensor]) – Sigmoid regression outputs for each feature level. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

- gt_labels_list (list[Tensor]) – Ground truth class indices for each image with shape (num_gts, ).

• img_metas (list[dict]) – List of image meta information.

- gt_bboxes_ignore (list[Tensor], optional) – Bounding boxes which can be ignored for each image. Default None.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single(cls_scores, bbox_preds, gt_bboxes_list, gt_labels_list, img_metas,

gt_bboxes_ignore_list=None)

“Loss function for outputs from a single decoder layer of a single feature level.”

## Parameters