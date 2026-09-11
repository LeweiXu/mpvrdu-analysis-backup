•  $ (scale\_refine) $ – obj: mmcv.cnn.Scale): Learnable scale module to resize the bbox prediction.

•  $ (-obj: mmcv.cnn.Scale) $: Learnable scale module to resize the refined bbox prediction.

• stride (int) – The corresponding stride for feature maps, used to normalize the bbox prediction when bbox_norm_type ='stride'.

• reg_denom (int) – The corresponding regression range for feature maps, only used to normalize the bbox prediction when bbox_norm_type ='reg_denom'.

## Returns

iou-aware cls scores for each box, bbox predictions and refined bbox predictions of input feature maps.

Return type tuple

get_anchors(featmap_sizes, img_metas, device='cuda')

Get anchors according to feature map sizes.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• img_metas (list[dict]) – Image meta info.

• device (torch.device / str) – Device for returned tensors

Returns anchor_list (list[Tensor]): Anchors of each image. valid_flag_list (list[Tensor]): Valid flags of each image.

Return type tuple

get_atss_targets(cls_scores, mlvl_points, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) A wrapper for computing ATSS targets for points in multiple images.

## Parameters

• cls_scores (list[Tensor]) – Box iou-aware scores for each scale level with shape (N, num_points * num_classes, H, W).

- mlvI_points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

• gt_labels (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / Tensor) – Ground truth bboxes to be ignored, shape (num_ignored_gts, 4). Default: None.

## Returns

labels_list (list[Tensor]): Labels of each level. label_weights (Tensor): Label weights of all levels. bbox_targets_list (list[Tensor]): Regression targets of each

level, (l, t, r, b).

bbox_weights (Tensor): Bbox weights of all levels.

Return type tuple