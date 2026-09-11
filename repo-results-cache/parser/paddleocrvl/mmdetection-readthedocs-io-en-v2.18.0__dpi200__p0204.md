• (Sequence[int] or torch.Tensor or Sequence[(max_shape) - Sequence[int]],optional): Maximum bounds for boxes, specifies (H, W, C) or (H, W). If priors shape is (B, N, 4), then the max_shape should be a Sequence[Sequence[int]], and the length of max_shape should also be B. Default None.

Returns Boxes with shape  $ (N, 4) $ or  $ (B, N, 4) $

Return type Tensor

encode(points, gt_bboxes, max_dis=None, eps=0.1)

Encode bounding box to distances.

## Parameters

• points (Tensor) – Shape (N, 2), The format is [x, y].

• gt_bboxes (Tensor) – Shape (N, 4), The format is “xyxy”

• max_dis (float) – Upper bound of the distance. Default None.

• eps (float) – a small value to ensure target < max_dis, instead <=. Default 0.1.

Returns Box transformation deltas. The shape is  $ (N, 4) $.

Return type Tensor

class mmdet.core.bbox.InstanceBalancedPosSampler(num, pos_fraction, neg_pos_ub=-1, add_gt_as_proposals=True, **kwargs)

Instance balanced sampler that samples equal number of positive samples for each instance.

class mmdet.core.bbox.IoUBalancedNegSampler(num, pos_fraction, floor_thr=-1, floor_fraction=0,

num_bins=3, **kwargs)

IoU Balanced Sampling.

arXiv: https://arxiv.org/pdf/1904.02701.pdf (CVPR 2019)

Sampling proposals according to their IoU.  $ floor\_fraction $ of needed RoIs are sampled from proposals whose IoU are lower than  $ floor\_thr $ randomly. The others are sampled from proposals whose IoU are higher than  $ floor\_thr $. These proposals are sampled from some bins evenly, which are split by  $ num\_bins $ via IoU evenly.

## Parameters

• num (int) – number of proposals.

• pos_fraction (float) – fraction of positive proposals.

• floor_thr (float) – threshold (minimum) IoU for IoU balanced sampling, set to -1 if all using IoU balanced sampling.

• floor_fraction (float) – sampling fraction of proposals under floor_thr.

• num bins (int) – number of bins in IoU balanced sampling.

sample_via_interval(max_overlaps, full_set, num_expected)

Sample according to the iou interval.

Parameters

• max_overlaps (torch.Tensor) – IoU between bounding boxes and ground truth boxes.

• full_set (set(int)) – A full set of indices of boxes

• num_expected (int) – Number of expected samples

Returns Indices of samples

Return type np.ndarray