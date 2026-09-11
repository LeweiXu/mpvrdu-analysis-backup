forward(mlvl_feats, img_metas)

Forward function.

## Parameters

- mlvl_feats (tuple [Tensor]) – Features from the upstream network, each is a 4D-tensor with shape (N, C, H, W).

• img_metas (list[dict]) – List of image information.

Returns Outputs from the classification head, shape [nb_dec, bs, num_query, cls_out_channels]. Note cls_out_channels should include background. all_bbox_preds (Tensor): Sigmoid outputs from the regression head with normalized coordinate format (cx, cy, w, h). Shape [nb_dec, bs, num_query, 4]. enc_outputs_class (Tensor): The score of each point on encode feature map, has shape (N, h*w, num_class). Only when as_two_stage is True it would be returned, otherwise None would be returned. enc_outputs_coord (Tensor): The proposal generate from the encode feature map, has shape (N, h*w, 4). Only when as_two_stage is True it would be returned, otherwise None would be returned.

Return type all_cls_scores (Tensor)

get_bboxes(all_cls_scores, all_bbox_preds, enc_cls_scores, enc_bbox_preds, img_metas, rescale=False)

Transform network outputs for a batch into bbox predictions.

## Parameters

• all_cls_scores (Tensor) – Classification score of all decoder layers, has shape [nb_dec, bs, num_query, cls_out_channels].

• all_bbox_preds (Tensor) – Sigmoid regression outputs of all decode layers. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

- enc_cls_scores (Tensor) – Classification scores of points on encode feature map, has shape (N, h*w, num_classes). Only be passed when as_two_stage is True, otherwise is None.

- enc_bbox_preds (Tensor) – Regression results of each points on the encode feature map, has shape  $ (N, h*w, 4) $. Only be passed when as_two_stage is True, otherwise is None.

• img_metas (list[dict]) – Meta information of each image.

• rescale (bool, optional) – If True, return boxes in original image space. Default False.

Returns Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

## Return type list[list[Tensor, Tensor]]

## init_weights()

Initialize weights of the DeformDETR head.

loss(all_cls_scores, all_bbox_preds, enc_cls_scores, enc_bbox_preds, gt_bboxes_list, gt_labels_list, img_metas, gt_bboxes_ignore=None)

“Loss function.”

## Parameters

- all_cls_scores (Tensor) – Classification score of all decoder layers, has shape [nb_dec, bs, num_query, cls_out_channels].