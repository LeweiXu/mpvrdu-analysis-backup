• feats (list [Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains features for all images in the batch.

• img_metas (list[list[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch. each dict has image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

Returns bbox results of each class

Return type list[ndarray]

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

A tuple of multi-level predication map, each is a 4D-tensor of shape  $ (batch\_size, 5+num\_classes, height, width) $.

Return type tuple[Tensor]

get_bboxes(pred_maps, img_metas, cfg=None, rescale=False, with_nms=True)

Transform network output for a batch into bbox predictions. It has been accelerated since PR #5991.

## Parameters

• pred_maps (list[Tensor]) – Raw predictions for a batch of images.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

•cfg (mmcv.Config / None) – Test / postprocessing configuration, if None, test_cfg would be used. Default: None.

• rescale (bool) – If True, return boxes in original image space. Default: False.

• with_nms (bool) – If True, do nms before return boxes. Default: True.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where 5 represent  $ (tl\_x, tl\_y, br\_x, br\_y, score) $ and the score between 0 and 1. The shape of the second tensor in the tuple is  $ (n,) $, and each element represents the class label of the corresponding box.

Return type list[tuple[Tensor, Tensor]]

get_targets(anchor_list, responsible_flag_list, gt_bboxes_list, gt_labels_list)

Compute target maps for anchors in multiple images.

## Parameters

• anchor_list (list[list[Tensor]]) – Multi level anchors of each image. The outer list indicates images, and the inner list corresponds to feature levels of the image. Each element of the inner list is a tensor of shape (num_total_anchors, 4).

• responsible_flag_list (list[list[Tensor]]) – Multi level responsible flags of each image. Each element is a tensor of shape (num_total_anchors,)

• gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.

• gt_labels_list (list[Tensor]) – Ground truth labels of each box.

## Returns