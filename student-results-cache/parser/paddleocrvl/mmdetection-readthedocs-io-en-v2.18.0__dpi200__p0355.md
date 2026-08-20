–'spherical': each component has its own single variance

Default: 'diag'. From 'full' to'spherical', the gmm fitting process is faster yet the performance could be influenced. For most cases, 'diag' should be a good choice.

get_bboxes(cls_scores, bbox_preds, score_factors=None, img_metas=None, cfg=None, rescale=False, with_nms=True, **kwargs)

Transform network outputs of a batch into bbox results.

Note: When score_factors is not None, the cls_scores are usually multiplied by it then obtain the real score used in NMS, such as CenterNess in FCOS, IoU branch in ATSS.

## Parameters

• cls_scores (list[Tensor]) – Classification scores for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * num_classes, H, W).

• bbox_preds (list[Tensor]) – Box energies / deltas for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * 4, H, W).

- score_factors (list[Tensor], Optional) – Score factor for all scale level, each is a 4D-tensor, has shape (batch_size, num_priors * 1, H, W). Default None.

• img_metas (list[dict], Optional) – Image meta info. Default None.

•cfg (mmcv.Config, Optional) – Test / postprocessing configuration, if None, test_cfg would be used. Default None.

• rescale (bool) – If True, return boxes in original image space. Default False.

• with_nms (bool) – If True, do nms before return boxes. Default True.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

Return type list[list[Tensor, Tensor]]

get_pos_loss(anchors, cls_score, bbox_pred, label, label_weight, bbox_target, bbox_weight, pos_inds)

Calculate loss of all potential positive samples obtained from first match process.

## Parameters

• anchors (list[Tensor]) – Anchors of each scale.

• cls_score (Tensor) – Box scores of single image with shape (num_anchors, num_classes)

• bbox_pred (Tensor) – Box energies / deltas of single image with shape (num_anchors, 4)

• label (Tensor) – classification target of each anchor with shape (num_anchors,)

• label_weight (Tensor) – Classification loss weight of each anchor with shape (num_anchors).

• bbox_target(dict) – Regression target of each anchor with shape (num_anchors, 4).

• bbox_weight (Tensor) – Bbox weight of each anchor with shape (num_anchors, 4).

• pos_inds (Tensor) – Index of all positive samples got from first assign process.

Returns Losses of all positive samples in single image.