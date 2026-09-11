• target_stds (Sequence[float]) – Denormalizing standard deviation of target for delta coordinates

• clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

- add_ctr_clamp (bool) – Whether to add center clamp, when added, the predicted box is clamped is its center is too far away from the original anchor’s center. Only used by YOLOF. Default False.

• ctr_clamp (int) – the maximum pixel shift to clamp. Only used by YOLOF. Default 32.

decode(bboxes, pred_bboxes, max_shape=None, wh_ratio_clip=0.016)

Apply transformation  $ pred\_bboxes $ to boxes.

## Parameters

• bboxes (torch.Tensor) – Basic boxes. Shape (B, N, 4) or (N, 4)

• pred_bboxes (Tensor) – Encoded offsets with respect to each roi. Has shape (B, N, num_classes * 4) or (B, N, 4) or (N, num_classes * 4) or (N, 4). Note N = num_ర్చక * W * H when rois is a grid of anchors. Offset encoding follows $ ^{1} $.

• (Sequence[int] or torch.Tensor or Sequence[(max_shape) - Sequence[int]], optional): Maximum bounds for boxes, specifies (H, W, C) or (H, W). If bboxes shape is (B, N, 4), then the max_shape should be a Sequence[Sequence[int]] and the length of max_shape should also be B.

• wh_ratio_clip (float, optional) – The allowed ratio between width and height.

Returns Decoded boxes.

Return type torch.Tensor

## encode(bboxes, gt_bboxes)

Get box regression transformation deltas that can be used to transform the bboxes into the gt_bboxes.

## Parameters

• bboxes (torch.Tensor) – Source boxes, e.g., object proposals.

• gt_bboxes (torch.Tensor) – Target of the transformation, e.g., ground-truth boxes.

Returns Box transformation deltas

Return type torch.Tensor

##### class mmdet.core.bbox.DistancePointBBoxCoder(clip_border=True)

Distance Point BBox coder.

This coder encodes gt bboxes  $ (x_{1}, y_{1}, x_{2}, y_{2}) $ into (top, bottom, left, right) and decode it back to the original.

Parameters clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

decode(points, pred_bboxes, max_shape=None)

Decode distance prediction to bounding box.

## Parameters

• points (Tensor) – Shape (B, N, 2) or (N, 2).

• pred_bboxes (Tensor) – Distance from the given point to 4 boundaries (left, top, right, bottom). Shape (B, N, 4) or (N, 4)