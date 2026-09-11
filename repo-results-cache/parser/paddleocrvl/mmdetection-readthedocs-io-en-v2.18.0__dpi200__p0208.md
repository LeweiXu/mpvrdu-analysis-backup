## Parameters

• mlvI_anchors (list [Tensor]) – Multi level anchors.

• mvl_valid_flags (list[Tensor]) – Multi level valid flags.

• gt_bboxes (Tensor) – Ground truth bboxes of image

• img_meta(dict) – Meta info of image.

• featmap sizes (list[Tensor]) – Feature map size each level

• anchor_scale (int) – Scale of the anchor.

• anchor_strides (list[int]) – Stride of the anchor.

• gt_bboxes – Groundtruth boxes, shape (k, 4).

- gt_bboxes_ignore (Tensor, optional) – Ground truth bboxes that are labelled as ignored, e.g., crowd boxes in COCO.

• gt_labels (Tensor, optional) – Label of gt_bboxes, shape (k, ).

• allowed_border (int, optional) – The border to allow the valid anchor. Defaults to 0.

Returns The assign result.

Return type AssignResult

class mmdet.core.bbox.SamplingResult(pos_inds, neg_inds, bboxes, gt_bboxes, assign_result, gt_flags)

Bbox sampling result.

## Example

>>> # xdoctest: +IGNORE_WANT
>>> from mmdet.core.bbox.samplers.sampling_result import *  # NOQA
>>> self = SamplingResult.random(rng=10)
>>> print(f'self = {self}')
self = <SamplingResult({
    'neg_bboxes': torch.Size([12, 4]),
    'neg_inds': tensor([0, 1, 2, 4, 5, 6, 7, 8, 9, 10, 11, 12]),
    'num_gts': 4,
    'pos_assigned_gt_inds': tensor([], dtype=torch.int64),
    'pos_bboxes': torch.Size([0, 4]),
    'pos_inds': tensor([], dtype=torch.int64),
    'pos_is_gt': tensor([], dtype=torch.uint8)
})>
property bboxes
concatenated positive and negative boxes
Type torch.Tensor
property info
Returns a dictionary of info about the object.
classmethod random(rng=None, **kwargs)

## Parameters