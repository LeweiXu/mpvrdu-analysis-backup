- gt_masks (Tensor) – Ground truth masks for each image with the same shape of the input image.

• pos_assigned_gt_inds (Tensor) – GT indices of the corresponding positive samples.

## Returns

Instance segmentation targets with shape (num_instances, H, W).

Return type Tensor

loss(mask_pred, gt_masks, gt_bboxes, img_meta, sampling_results)

Compute loss of the head.

## Parameters

• mask_pred (list[Tensor]) – Predicted prototypes with shape (num_classes, H, W).

- gt_masks (list[Tensor]) – Ground truth masks for each image with the same shape of the input image.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• img_meta (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• sampling_results (List[:obj:SamplingResult]) – Sampler results for each image.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

## sanitize_coordinates(x1, x2, img_size, padding=0, cast=True)

Sanitizes the input coordinates so that  $ x_{1} < x_{2} $,  $ x_{1}!= x_{2} $,  $ x_{1} >= 0 $, and  $ x_{2} <= image\_size $. Also converts from relative to absolute coordinates and casts the results to long tensors.

Warning: this does things in-place behind the scenes so copy if necessary.

## Parameters

• x1 (Tensor) – shape (N, ).

• x2 (Tensor) – shape (N, ).

• img_size (int) – Size of the input image.

• padding (int) - x1 >= padding, x2 <= image_size - padding.

• cast (bool) – If cast is false, the result won’t be cast to longs.

Returns x1 (Tensor): Sanitized x1. x2 (Tensor): Sanitized x2.

## Return type tuple

simple_test(feats, det_bboxes, det_labels, det_coeffs, img_metas, rescale=False)

Test function without test-time augmentation.

## Parameters

• feats (tuple[torch.Tensor]) – Multi-level features from the upstream network, each is a 4D-tensor.

- det_bboxes (list [Tensor]) – BBox results of each image. each element is  $ (n, 5) $ tensor, where 5 represent  $ (tl\_x, tl\_y, br\_x, br\_y, score) $ and the score between 0 and 1.

• det_labels (list[Tensor]) – BBox results of each image. each element is (n, ) tensor, each element represents the class label of the corresponding box.