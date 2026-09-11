## Example

>>> self = FCOSHead(11, 7)
>>> feats = [torch.rand(1, 7, s, s) for s in [4, 8, 16, 32, 64]]
>>> cls_score, bbox_pred, centerness = self.forward(feats)
>>> assert len(cls_score) == len(self.scales)

## centerness_target(pos_bbox_targets)

Compute centerness targets.

Parameters pos_bbox_targets (Tensor) – BBox targets of positive bboxes in shape (num_pos, 4)

Returns Centerness target.

Return type Tensor

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

Returns cls_scores (list[Tensor]): Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes. bbox_pred (list[Tensor]): Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4. centernesses (list[Tensor]): centerness for each scale level, each is a 4D-tensor, the channel number is num_points * 1.

Return type tuple

forward_single(x, scale, stride)

Forward features of a single scale level.

## Parameters

• x (Tensor) – FPN feature maps of the specified stride.

•  $ (scale) - obj: mmcv.cnn.Scale $: Learnable scale module to resize the bbox prediction.

• stride (int) – The corresponding stride for feature maps, only used to normalize the bbox prediction when self.norm_on_bbox is True.

Returns scores for each class, bbox predictions and centerness predictions of input feature maps.

Return type tuple

get_targets(points, gt_bboxes_list, gt_labels_list)

Compute regression, classification and centerness targets for points in multiple images.

Parameters

• points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

- gt_labels_list (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

Returns concat_lvI_labels (list[Tensor]): Labels of each level. concat_lvI_bbox_targets (list[Tensor]): BBox targets of each level.

Return type tuple