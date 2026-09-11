Returns Decoded boxes.

### Return type torch.Tensor

encode(bboxes, gt_bboxes)

Get box regression transformation deltas that can be used to transform the bboxes into the gt_bboxes in the (top, left, bottom, right) order.

Parameters

• bboxes (torch.Tensor) – source boxes, e.g., object proposals.

• gt_bboxes (torch.Tensor) – target of the transformation, e.g., ground truth boxes.

Returns Box transformation deltas

Return type torch.Tensor

mmdet.core.bbox.bbox2distance(points, bbox, max_dis=None, eps=0.1)

Decode bounding box based on distances.

## Parameters

• points (Tensor) – Shape (n, 2), [x, y].

• bbox (Tensor) – Shape (n, 4), “xyxy” format

• max_dis (float) – Upper bound of the distance.

• eps (float) – a small value to ensure target < max_dis, instead <=

Returns Decoded distances.

Return type Tensor

mmdet.core.bbox.bbox2result(bboxes, labels, num_classes)

Convert detection results to a list of numpy arrays.

## Parameters

• bboxes (torch.Tensor / np.ndarray) – shape (n, 5)

• labels (torch.Tensor / np.ndarray) – shape (n,)

• num_classes (int) – class number, including background class

Returns bbox results of each class

Return type list(ndarray)

mmdet.core.bbox.bbox2roi(bbox_list)

Convert a list of bboxes to roi format.

Parameters bbox_list (list[Tensor]) – a list of bboxes corresponding to a batch of images.

Returns shape (n, 5), [batch_ind, x1, y1, x2, y2]

Return type Tensor

mmdet.core.bbox.bbox_cxcywh_to_xyxy(bbox)

Convert bbox coordinates from (cx, cy, w, h) to (x1, y1, x2, y2).

Parameters bbox (Tensor) – Shape (n, 4) for bboxes.

Returns Converted bboxes.

Return type Tensor