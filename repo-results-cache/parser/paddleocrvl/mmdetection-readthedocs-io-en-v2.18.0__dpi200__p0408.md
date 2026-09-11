## Return type Tensor

get_roi_rel_points_test(mask_pred, pred_label, cfg)

Get num_points most uncertain points during test.

## Parameters

• mask_pred (Tensor) – A tensor of shape (num_rois, num_classes, mask_height, mask_width) for class-specific or class-agnostic prediction.

• pred_label (list) – The predication class for each instance.

• cfg(dict) – Testing config of point head.

## Returns

A tensor of shape (num_rois, num_points) that contains indices from [0, mask_height x mask_width) of the most uncertain points.

point_coords (Tensor): A tensor of shape (num_rois, num_points, 2) that contains  $ [0, 1] $ x  $ [0, 1] $ normalized coordinates of the most uncertain points from the [mask_height, mask_width] grid.

Return type point_indices (Tensor)

## get_roi_rel_points_train(mask_pred, labels, cfg)

Get num_points most uncertain points with random points during train.

Sample points in  $ [0, 1] $ x  $ [0, 1] $ coordinate space based on their uncertainty. The uncertainties are calculated for each point using ‘_get_uncertainty()’ function that takes point’s logit prediction as input.

## Parameters

• mask_pred (Tensor) – A tensor of shape (num_rois, num_classes, mask_height, mask_width) for class-specific or class-agnostic prediction.

• labels (list) – The ground truth class for each instance.

• cfg(dict) – Training config of point head.

## Returns

A tensor of shape (num_rois, num_points, 2) that contains the coordinates sampled points.

Return type point_coords (Tensor)

get_targets(rois, rel_roi_points, sampling_results, gt_masks, cfg)

Get training targets of MaskPointHead for all images.

## Parameters

• rois (Tensor) – Region of Interest, shape (num_rois, 5).

• rel_roi_points – Points coordinates relative to RoI, shape (num_rois, num_points, 2).

• sampling_results (SamplingResult) – Sampling result after sampling and assignment.

- gt_masks (Tensor) – Ground truth segmentation masks of corresponding boxes, shape (num_rois, height, width).

• cfg(dict) – Training cfg.

Returns Point target, shape (num_rois, num_points).

Return type Tensor