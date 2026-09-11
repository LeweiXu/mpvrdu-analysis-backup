• all_bbox_preds (Tensor) – Sigmoid regression outputs of all decode layers. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

- enc_cls_scores (Tensor) – Classification scores of points on encode feature map, has shape (N, h*w, num_classes). Only be passed when as_two_stage is True, otherwise is None.

- enc_bbox_preds (Tensor) – Regression results of each points on the encode feature map, has shape (N, h*w, 4). Only be passed when as_two_stage is True, otherwise is None.

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

- gt_labels_list (list[Tensor]) – Ground truth class indices for each image with shape (num_gts, ).

• img_metas (list[dict]) – List of image meta information.

- gt_bboxes_ignore (list[Tensor], optional) – Bounding boxes which can be ignored for each image. Default None.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.EmbeddingRPNHead(num_proposals=100, proposal_feature_channel=256, init_cfg=None, **kwargs)

RPNHead in the Sparse R-CNN.

Unlike traditional RPNHead, this module does not need FPN input, but just decode  $ init\_proposal\_bboxes $ and expand the first dimension of  $ init\_proposal\_bboxes $ and  $ init\_proposal\_features $ to the batch_size.

## Parameters

• num proposals (int) – Number of init proposals. Default 100.

• proposal_feature_channel (int) – Channel number of init_proposal_feature. Defaults to 256.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward_dummy(img, img_metas)

Dummy forward function.

Used in flops calculation.

forward_train(img, img_metas)

Forward function in training stage.

## init_weights()

Initialize the init_proposal_bboxes as normalized.

 $ [c_{x}, c_{y}, w, h] $, and we initialize it to the size of the entire image.

simple_test(img, img_metas)

Forward function in testing stage.

simple_test_rpn(img, img_metas)

Forward function in testing stage.