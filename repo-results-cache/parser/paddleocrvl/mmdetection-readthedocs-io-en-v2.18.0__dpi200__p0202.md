## Example

>>> self = CenterRegionAssigner(0.2, 0.2)

>>> bboxes = torch.Tensor([[0, 0, 10, 10], [10, 10, 20, 20]])

>>> gt_bboxes = torch.Tensor([[0, 0, 10, 10]])

>>> assign_result = self.assign(bboxes, gt_bboxes)

>>> expected_gt_inds = torch.LongTensor([1, 0])

>>> assert torch.all(assign_result.gt_inds == expected_gt_inds)

assign_one_hot_gt_indices(is_bbox_in_gt_core, is_bbox_in_gt_shadow, gt_priority=None)

Assign only one gt index to each prior box.

Gts with large gt_priority are more likely to be assigned.

## Parameters

• is_bbox_in_gt_core (Tensor) – Bool tensor indicating the bbox center is in the core area of a gt (e.g. 0-0.2). Shape: (num_prior, num_gt).

• is_bbox_in_gt_shadow(Tensor) – Bool tensor indicating the bbox center is in the shadowed area of a gt (e.g. 0.2-0.5). Shape: (num_prior, num_gt).

- gt_priority (Tensor) – Priorities of gts. The gt with a higher priority is more likely to be assigned to the bbox when the bbox match with multiple gts. Shape: (num_gt, ).

## Returns

Returns (assigned_gt_inds, shadowed_gt_inds).

- assigned_gt_inds: The assigned gt index of each prior bbox (i.e. index from 1 to num_gts). Shape: (num_prior, ).

• shadowed_gt_inds: shadowed gt indices. It is a tensor of shape (num_ignore, 2) with first column being the shadowed prior bbox indices and the second column the shadowed gt indices (1-based).

## Return type tuple

## get_gt_priorities(gt_bboxes)

Get gt priorities according to their areas.

Smaller gt has higher priority.

Parameters gt_bboxes (Tensor) – Ground truth boxes, shape (k, 4).

Returns The priority of gts so that gts with larger priority is more likely to be assigned. Shape  $ (k,) $

Return type Tensor

class mmdet.core.bbox.CombinedSampler(pos_sampler, neg_sampler, **kwargs)

A sampler that combines positive sampler and negative sampler.

class mmdet.core.bbox.DeltaXYWHBBoxCoder(target_means=(0.0, 0.0, 0.0, 0.0), target_stds=(1.0, 1.0, 1.0, 1.0), clip_border=True, add_ctr_clamp=False, ctr_clamp=32)

Delta XYWH BBox coder.

Following the practice in R-CNN, this coder encodes bbox  $ (x_{1}, y_{1}, x_{2}, y_{2}) $ into delta  $ (dx, dy, dw, dh) $ and decodes delta  $ (dx, dy, dw, dh) $ back to original bbox  $ (x_{1}, y_{1}, x_{2}, y_{2}) $.

Parameters

• target_means (Sequence $$ float $$ ) – Denormalizing means of target for delta coordinates