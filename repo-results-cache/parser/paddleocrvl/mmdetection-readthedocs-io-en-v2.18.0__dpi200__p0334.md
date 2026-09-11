• cls_scores (Tensor) – Box score logits from a single decoder layer for all images. Shape [bs, num_query, cls_out_channels].

• bbox_preds (Tensor) – Sigmoid outputs from a single decoder layer for all images, with normalized coordinate (cx, cy, w, h) and shape [bs, num_query, 4].

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

- gt_labels_list (list[Tensor]) – Ground truth class indices for each image with shape (num_gts, ).

• img_metas (list[dict]) – List of image meta information.

- gt_bboxes_ignore_list (list[Tensor], optional) – Bounding boxes which can be ignored for each image. Default None.

## Returns

A dictionary of loss components for outputs from a single decoder layer.

Return type dict[str, Tensor]

onnx_export(all_cls_scores_list, all_bbox_preds_list, img_metas)

Transform network outputs into bbox predictions, with ONNX exportation.

## Parameters

• all_cls_scores_list (list[Tensor]) – Classification outputs for each feature level. Each is a 4D-tensor with shape [nb_dec, bs, num_query, cls_out_channels].

• all_bbox_preds_list (list[Tensor]) – Sigmoid regression outputs for each feature level. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

• img_metas (list[dict]) – Meta information of each image.

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].

Return type tuple[Tensor, Tensor]

simple_test_bboxes(feats, img_metas, rescale=False)

Test det bboxes without test-time augmentation.

Parameters

• feats (tuple[torch.Tensor]) – Multi-level features from the upstream network, each is a 4D-tensor.

• img_metas (list[dict]) – List of image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

## Returns

Each item in result_list is 2-tuple. The first item is bboxes with shape  $ (n, 5) $, where 5 represent  $ (tl\_x, tl\_y, br\_x, br\_y, score) $. The shape of the second tensor in the tuple is labels with shape  $ (n,) $.

Return type list[tuple[Tensor, Tensor]]