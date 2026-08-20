## Usually returns a tuple containing learning targets

• target_map_list (list[Tensor]): Target map of each level.

• neg_map_list (list[Tensor]): Negative map of each level.

## Return type tuple

## init_weights()

Initialize the weights.

loss(pred_maps, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute loss of the head.

## Parameters

• pred_maps (list[Tensor]) – Prediction map for each scale level, shape (N, num_anchors * num_attrib, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single(pred_map, target_map, neg_map)

Compute loss of a single image from a batch.

## Parameters

• pred_map (Tensor) – Raw predictions for a single level.

• target_map (Tensor) – The Ground-Truth target for a single level.

• neg_map (Tensor) – The negative masks for a single level.

Returns loss_cls (Tensor): Classification loss. loss_conf (Tensor): Confidence loss. loss_xy (Tensor): Regression loss of x, y coordinate. loss_wh (Tensor): Regression loss of w, h coordinate.

## Return type tuple

## property num_anchors

Returns: int: Number of anchors on each point of feature map.

## property num_attrib

number of attributes in pred_map, bboxes (4) + objectness (1) + num_classes

Type int

onnx_export(pred_maps, img_metas, with_nms=True)

Transform network output for a batch into bbox predictions.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level with shape (N, num_points * num_classes, H, W).