Return type Tensor

## Example

>>> bboxes1 = torch.FloatTensor([
    [0, 0, 10, 10],
    [10, 10, 20, 20],
    [32, 32, 38, 42],
])

>>> bboxes2 = torch.FloatTensor([
    [0, 0, 10, 20],
    [0, 10, 10, 19],
    [10, 10, 20, 20],
])

>>> overlaps = bbox_overlaps(bboxes1, bboxes2)

>>> assert overlaps.shape == (3, 3)

>>> overlaps = bbox_overlaps(bboxes1, bboxes2, is_aligned=True)

>>> assert overlaps.shape == (3, )

## Example

>>> empty = torch.empty(0, 4)

>>> nonempty = torch.FloatTensor([[0, 0, 10, 9]])

>>> assert tuple(bbox_overlaps(empty, nonempty).shape) == (0, 1)

>>> assert tuple(bbox_overlaps(nonempty, empty).shape) == (1, 0)

>>> assert tuple(bbox_overlaps(empty, empty).shape) == (0, 0)

###### mmdet.core.bbox.bbox_rescale(bboxes, scale_factor=1.0)

Rescale bounding box w.r.t. scale factor.

## Parameters

• bboxes (Tensor) – Shape (n, 4) for bboxes or (n, 5) for rois

• scale factor (float) – rescale factor

Returns Rescaled bboxes.

Return type Tensor