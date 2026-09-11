## Example

>>> from mmdet.core.bbox.assigners.assign_result import *  # NOQA
>>> self = AssignResult.random()
>>> print(self.info)

set_extra_property(key, value)

Set user-defined new property.

##### class mmdet.core.bbox.BaseAssigner

Base assigner that assigns boxes to ground truth boxes.

abstract assign(bboxes, gt_bboxes, gt_bboxes_ignore=None, gt_labels=None)

Assign boxes to either a ground truth boxes or a negative boxes.

class mmdet.core.bbox.BaseBBoxCoder(**kwargs)

Base bounding box coder.

abstract decode(bboxes, bboxes_pred)

Decode the predicted bboxes according to prediction and base boxes.

abstract encode(bboxes, gt_bboxes)

Encode deltas between bboxes and ground truth boxes.

class mmdet.core.bbox.BaseSampler(num, pos_fraction, neg_pos_ub=-1, add_gt_as_proposals=True,

Base class of samplers.

sample(assign_result, bboxes, gt_bboxes, gt_labels=None, **kwargs)

Sample positive and negative bboxes.

This is a simple implementation of bbox sampling given candidates, assigning results and ground truth bboxes.

## Parameters

• assign_result (AssignResult) – Bbox assigning results.

• bboxes (Tensor) – Boxes to be sampled from.

• gt_bboxes (Tensor) – Ground truth bboxes.

• gt_labels (Tensor, optional) – Class labels of ground truth bboxes.

Returns Sampling result.

Return type SamplingResult

## Example

>>> from mmdet.core.bbox import RandomSampler
>>> from mmdet.core.bbox import AssignResult
>>> from mmdet.core.bbox.demodata import ensure_rng, random_boxes
>>> rng = ensure_rng(None)
>>> assign_result = AssignResult.random(rng=rng)
>>> bboxes = random_boxes(assign_result.num_preds, rng=rng)
>>> gt_bboxes = random_boxes(assign_result.num_gts, rng=rng)
>>> gt_labels = None
>>> self = RandomSampler(num=32, pos_fraction=0.5, neg_pos_ub=-1,

(continues on next page)