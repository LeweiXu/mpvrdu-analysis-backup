• bbox_preds (list[Tensor]) – Box energies / deltas for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * 4, H, W).

- score_factors (list[Tensor], Optional) – Score factor for all scale level, each is a 4D-tensor, has shape (batch_size, num_priors * 1, H, W). Default None.

• img_metas (list[dict], Optional) – Image meta info. Default None.

•cfg (mmcv.Config, Optional) – Test / postprocessing configuration, if None, test_cfg would be used. Default None.

• rescale (bool) – If True, return boxes in original image space. Default False.

• with_nms (bool) – If True, do nms before return boxes. Default True.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

Return type list[list[Tensor, Tensor]]

get_sampled_approxs(featmap_sizes, img_metas, device='cuda')

Get sampled approxs and inside flags according to feature map sizes.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• img_metas (list[dict]) – Image meta info.

• device (torch.device / str) – device for returned tensors

Returns approaches of each image, inside flags of each image

Return type tuple

loss(cls_scores, bbox_preds, shape_preds, loc_preds, gt_bboxes, gt_labels, img_metas,

gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list [Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None

Returns A dictionary of loss components.

Return type dict[str, Tensor]