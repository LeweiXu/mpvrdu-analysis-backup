## static random_choice(gallery, num)

Randomly select some elements from the gallery.

If gallery is a Tensor, the returned indices will be a Tensor; If gallery is a ndarray or list, the returned indices will be a ndarray.

## Parameters

• gallery (Tensor / ndarray / list) – indices pool.

• num (int) – expected sample num.

Returns sampled indices.

Return type Tensor or ndarray

sample(assign_result, bboxes, gt_bboxes, gt_labels=None, img_meta=None, **kwargs)

Sample positive and negative bboxes.

This is a simple implementation of bbox sampling given candidates, assigning results and ground truth bboxes.

## Parameters

• assign_result (AssignResult) – Bbox assigning results.

• bboxes (Tensor) – Boxes to be sampled from.

• gt_bboxes (Tensor) – Ground truth bboxes.

• gt_labels (Tensor, optional) – Class labels of ground truth bboxes.

## Returns

Sampling result and negative label weights.

Return type tuple $$ SamplingResult, Tensor $$ 

class mmdet.core.bbox.TBLRBBoxCoder(normalizer=4.0, clip_border=True)

TBLR BBox coder.

Following the practice in FSAF, this coder encodes gt bboxes  $ (x_{1}, y_{1}, x_{2}, y_{2}) $ into (top, bottom, left, right) and decode it back to the original.

## Parameters

• normalizer (list / float) – Normalization factor to be divided with when coding the coordinates. If it is a list, it should have length of 4 indicating normalization factor in tblr dims. Otherwise it is a unified float factor for all dims. Default: 4.0

• clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

decode(bboxes, pred_bboxes, max_shape=None)

Apply transformation  $ pred\_bboxes $ to boxes.

## Parameters

• bboxes (torch.Tensor) – Basic boxes.Shape (B, N, 4) or (N, 4)

• pred_bboxes (torch.Tensor) – Encoded boxes with shape (B, N, 4) or (N, 4)

• (Sequence[int] or torch.Tensor or Sequence[(max_shape) - Sequence[int]], optional): Maximum bounds for boxes, specifies (H, W, C) or (H, W). If bboxes shape is (B, N, 4), then the max_shape should be a Sequence[Sequence[int]] and the length of max_shape should also be B.