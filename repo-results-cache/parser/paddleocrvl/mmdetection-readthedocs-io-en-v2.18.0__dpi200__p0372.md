forward(feats, offset_list=None)

Forward function.

forward_single(x, offset)

Forward function of single scale.

get_bboxes(anchor_list, cls_scores, bbox_preds, img_metas, cfg, rescale=False)

Get proposal predict.

## Parameters

• anchor_list (list[list]) – Multi level anchors of each image.

• cls_scores (list[Tensor]) – Classification scores for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * num_classes, H, W).

• bbox_preds (list[Tensor]) – Box energies / deltas for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * 4, H, W).

• img_metas (list[dict], Optional) – Image meta info. Default None.

•cfg (mmcv.Config, Optional) – Test / postprocessing configuration, if None, test_cfg would be used.

• rescale (bool) – If True, return boxes in original image space. Default: False.

## Returns

Labeled boxes in shape (n, 5), where the first 4 columns are bounding box positions (tl_x, tl_y, br_x, br_y) and the 5-th column is a score between 0 and 1.

## Return type Tensor

get_targets(anchor_list, valid_flag_list, gt_bboxes, img_metas, featmap_sizes, gt_bboxes_ignore=None, label_channels=1)

Compute regression and classification targets for anchors.

## Parameters

• anchor_list (list[list]) – Multi level anchors of each image.

• valid_flag_list (list[list]) – Multi level valid flags of each image.

• gt_bboxes (list[Tensor]) – Ground truth bboxes of each image.

• img_metas (list[dict]) – Meta info of each image.

• featmap sizes (list[Tensor]) – Feature map size each level

• gt_bboxes_ignore (list[Tensor]) – Ignore bboxes of each image

• label channels (int) – Channel of label.

## Returns cls_reg_targets (tuple)

loss(anchor_list, valid_flag_list, cls_scores, bbox_preds, gt_bboxes, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

## Parameters

• anchor_list (list[list]) – Multi level anchors of each image.

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)