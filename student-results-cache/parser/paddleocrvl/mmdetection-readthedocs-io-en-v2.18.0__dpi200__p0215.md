mmdet.core.bbox.distance2bbox(points, distance, max_shape=None)

Decode distance prediction to bounding box.

## Parameters

• points (Tensor) – Shape (B, N, 2) or (N, 2).

• distance (Tensor) – Distance from the given point to 4 boundaries (left, top, right, bottom). Shape (B, N, 4) or (N, 4)

• (Sequence[int] or torch.Tensor or Sequence[(max_shape) - Sequence[int]],optional): Maximum bounds for boxes, specifies (H, W, C) or (H, W). If priors shape is (B, N, 4), then the max_shape should be a Sequence[Sequence[int]] and the length of max_shape should also be B.

Returns Boxes with shape  $ (N, 4) $ or  $ (B, N, 4) $

Return type Tensor

mmdet.core.bbox.roi2bbox(rois)

Convert rois to bounding box format.

Parameters rois (torch.Tensor) – RoIs with the shape  $ (n, 5) $ where the first column indicates batch id of each RoI.

Returns Converted boxes of corresponding rois.

Return type list[torch.Tensor]

### 37.3 export

mmdet.core.export.add_dummy_nms_for_onnx(boxes, scores, max_output_boxes_per_class=1000, iou_threshold=0.5, score_threshold=0.05, pre_top_k=-1, after_top_k=-1, labels=None)

Create a dummy onnx::NonMaxSuppression op while exporting to ONNX.

This function helps exporting to onnx with batch and multiclass NMS op. It only supports class-agnostic detection results. That is, the scores is of shape  $ (N, num\_bboxes, num\_classes) $ and the boxes is of shape  $ (N, num\_boxes, 4) $.

## Parameters

• boxes (Tensor) – The bounding boxes of shape [N, num_boxes, 4]

• scores (Tensor) – The detection scores of shape [N, num_boxes, num_classes]

• max_output_boxes_per_class (int) – Maximum number of output boxes per class of nms. Defaults to 1000.

• iou_threshold (float) – IOU threshold of nms. Defaults to 0.5

• score_threshold (float) – score threshold of nms. Defaults to 0.05.

• pre_top_k (bool) – Number of top K boxes to keep before nms. Defaults to -1.

• after_top_k(int) – Number of top K boxes to keep after nms. Defaults to -1.

• labels (Tensor, optional) – It not None, explicit labels would be used. Otherwise, labels would be automatically generated using num_classed. Defaults to None.

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].