Return type all_cls_scores (Tensor)

forward_train(x, img_metas, gt_bboxes, gt_labels=None, gt_bboxes_ignore=None, proposal_cfg=None, **kwargs)

Forward function for training mode.

## Parameters

• x (list[Tensor]) – Features from backbone.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• gt_bboxes (Tensor) – Ground truth bboxes of the image, shape (num_gts, 4).

• gt_labels (Tensor) – Ground truth labels of each box, shape (num_gts,).

- gt_bboxes_ignore (Tensor) – Ground truth bboxes to be ignored, shape (num_ignored_gts, 4).

• proposal_cfg (mmcv.Config) – Test / postprocessing configuration, if None, test_cfg would be used.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

get_bboxes(all_cls_scores_list, all_bbox_preds_list, img_metas, rescale=False)

Transform network outputs for a batch into bbox predictions.

## Parameters

• all_cls_scores_list (list[Tensor]) – Classification outputs for each feature level. Each is a 4D-tensor with shape [nb_dec, bs, num_query, cls_out_channels].

• all_bbox_preds_list (list[Tensor]) – Sigmoid regression outputs for each feature level. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

• img_metas (list[dict]) – Meta information of each image.

• rescale (bool, optional) – If True, return boxes in original image space. Default False.

Returns Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

Return type list[list[Tensor, Tensor]]

get_targets(cls_scores_list, bbox_preds_list, gt_bboxes_list, gt_labels_list, img_metas,

gt_bboxes_ignore_list=None)

“Compute regression and classification targets for a batch image.”

Outputs from a single decoder layer of a single feature level are used.

Parameters

• cls_scores_list (list[Tensor]) – Box score logits from a single decoder layer for each image with shape [num_query, cls_out_channels].

• bbox_preds_list (list[Tensor]) – Sigmoid outputs from a single decoder layer for each image, with normalized coordinate (cx, cy, w, h) and shape [num_query, 4].