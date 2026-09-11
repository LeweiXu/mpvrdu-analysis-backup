• rng (None / int / numpy.random.RandomState) – seed or state.

• kwargs (keyword arguments) –

– num_pred: number of predicted boxes

– num_gts: number of true boxes

– p_ignore (float): probability of a predicted box assigned to an ignored truth.

– p_assigned (float): probability of a predicted box not being assigned.

- p_use_label (float | bool): with labels or not.

Returns Randomly generated sampling result.

Return type SamplingResult

## Example

>>> from mmdet.core.bbox.samplers.sampling_result import *  # NOQA
>>> self = SamplingResult.random()
>>> print(self.__dict__)

## to(device)

Change the device of the data inplace.

## Example

>>> self = SamplingResult.random()
>>> print(f'self = {self.to(None)}')
>>> # xdoctest: +REQUIREDs(--gpu)
>>> print(f'self = {self.to(0)}')

class mmdet.core.bbox.ScoreHLRSampler(num, pos_fraction, context, neg_pos_ub=-1,

 $ add\_gt\_as\_proposals=True $, k=0.5, bias=0,  $ score\_thr=0.05 $,  $ iou\_thr=0.5 $,  $ **kwargs $

Importance-based Sample Reweighting (ISR_N), described in Prime Sample Attention in Object Detection.

Score hierarchical local rank (HLR) differentiates with RandomSampler in negative part. It firstly computes Score-HLR in a two-step way, then linearly maps score hlr to the loss weights.

## Parameters

• num (int) – Total number of sampled RoIs.

• pos_fraction (float) – Fraction of positive samples.

• context (BaseRoIHead) – RoI head that the sampler belongs to.

• neg_pos_ub (int) – Upper bound of the ratio of num negative to num positive, -1 means no upper bound.

• add_gt_as_proposals (bool) – Whether to add ground truth as proposals.

• k (float) – Power of the non-linear mapping.

• bias (float) – Shift of the non-linear mapping.

• score_thr (float) – Minimum score that a negative sample is to be considered as valid bbox.