Returns The assign result.

Return type AssignResult

## Example

>>> self = MaxIoUAssigner(0.5, 0.5)

>>> bboxes = torch.Tensor([[0, 0, 10, 10], [10, 10, 20, 20]])

>>> gt_bboxes = torch.Tensor([[0, 0, 10, 9]])

>>> assign_result = self.assign(bboxes, gt_bboxes)

>>> expected_gt_inds = torch.LongTensor([1, 0])

>>> assert torch.all(assign_result.gt_inds == expected_gt_inds)

## assign_wrt_overlaps(overlaps, gt_labels=None)

Assign w.r.t. the overlaps of bboxes with gts.

## Parameters

• overlaps (Tensor) – Overlaps between k gt_bboxes and n bboxes, shape(k, n).

• gt_labels (Tensor, optional) – Labels of k gt_bboxes, shape (k, ).

Returns The assign result.

Return type AssignResult

##### class mmdet.core.bbox.OHEMSampler(num, pos_fraction, context, neg_pos_ub=-1,

 $$ a d d\_{g} t\_{a} s\_{p} r o p o s a l s=T r u e,\^{**}k w a r g s) $$ 

Online Hard Example Mining Sampler described in Training Region-based Object Detectors with Online Hard Example Mining.

##### class mmdet.core.bbox.PseudoBBoxCoder(**kwargs)

Pseudo bounding box coder.

decode(bboxes, pred_bboxes)

encode(bboxes, gt_bboxes)

##### class mmdet.core.bbox.PseudoSampler(**kwargs)

A pseudo sampler that does not do sampling actually.

sample(assign_result, bboxes, gt_bboxes, **kwargs)

Directly returns the positive and negative indices of samples.

## Parameters

• assign_result (AssignResult) – Assigned results

• bboxes (torch.Tensor) – Bounding boxes

• gt_bboxes (torch.Tensor) – Ground truth boxes

Returns sampler results

Return type SamplingResult

class mmdet.core.bbox.RandomSampler(num, pos_fraction, neg_pos_ub=-1, add_gt_as_proposals=True,

Random sampler.

Parameters