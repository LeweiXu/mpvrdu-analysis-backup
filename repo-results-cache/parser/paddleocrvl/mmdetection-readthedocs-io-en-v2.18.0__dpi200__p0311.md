Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

Usually contain classification scores and bbox predictions.

cls_scores (list[Tensor]): Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

bbox_pred(list[Tensor]): Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

## Return type tuple

## forward_single(x)

Forward features of a single scale level.

Parameters x (Tensor) – FPN feature maps of the specified stride.

## Returns

Scores for each class, bbox predictions, features after classification and regression conv layers, some models need these features like FCOS.

## Return type tuple

## get_points(featmap_sizes, dtype, device, flatten=False)

Get points according to feature map sizes.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• dtype (torch.dtype) – Type of points.

• device (torch.device) – Device of points.

Returns points of each image.

Return type tuple

abstract get_targets(points, gt_bboxes_list, gt_labels_list)

Compute regression, classification and centerness targets for points in multiple images.

## Parameters

• points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

- gt_labels_list (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

abstract loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.