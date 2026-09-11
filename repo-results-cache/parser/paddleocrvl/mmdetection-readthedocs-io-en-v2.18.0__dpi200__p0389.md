• loss_obj (dict) – Config of objectness loss.

• loss_l1(dict) – Config of L1 loss.

• train_cfg(dict) – Training config of anchor head.

• test_cfg(dict) – Testing config of anchor head.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

A tuple of multi-level predication map, each is a 4D-tensor of shape  $ (batch\_size, 5+num\_classes, height, width) $.

Return type tuple[Tensor]

forward_single(x, cls_convs, reg_convs, conv_cls, conv_reg, conv_obj)

Forward feature of a single scale level.

get_bboxes(cls_scores, bbox_preds, objectnesses, img_metas=None, cfg=None, rescale=False,

with_nms=True)

Transform network outputs of a batch into bbox results. :param cls_scores: Classification scores for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * num_classes, H, W).

## Parameters

• bbox_preds (list[Tensor]) – Box energies / deltas for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * 4, H, W).

• objectnesses (list[Tensor], Optional) – Score factor for all scale level, each is a 4D-tensor, has shape (batch_size, 1, H, W).

• img_metas (list[dict], Optional) – Image meta info. Default None.

•cfg (mmcv.Config, Optional) – Test / postprocessing configuration, if None, test_cfg would be used. Default None.

• rescale (bool) – If True, return boxes in original image space. Default False.

• with_nms (bool) – If True, do nms before return boxes. Default True.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

Return type list[list[Tensor, Tensor]]

## init_weights()

Initialize the weights.

loss(cls_scores, bbox_preds, objectnesses, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head. :param cls_scores: Box scores for each scale level,

each is a 4D-tensor, the channel number is num_priors * num_classes.