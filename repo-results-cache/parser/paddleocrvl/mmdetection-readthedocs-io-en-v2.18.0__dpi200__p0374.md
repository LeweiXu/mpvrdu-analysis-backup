• center_sample_radius (float) – Radius of center sampling. Default: 1.5.

- sync_num_pos (bool) – If true, synchronize the number of positive examples across GPUs.

Default: True

• gradient_mul(float) – The multiplier to gradients from bbox refinement and recognition. Default: 0.1.

• bbox_norm_type (str) – The bbox normalization type, ‘reg_denom’ or ‘stride’. Default: reg_denom

• loss_cls_fl (dict) – Config of focal loss.

• use_vfl (bool) – If true, use varifocal loss for training. Default: True.

• loss_cls (dict) – Config of varifocal loss.

• loss_bbox(dict) – Config of localization loss, GIoU Loss.

• loss_bbox – Config of localization refinement loss, GIoU Loss.

• norm_cfg (dict) – dictionary to construct and config norm layer. Default: norm_cfg=dict(type='GN', num_groups=32, requires_grad=True).

• use_atss (bool) – If true, use ATSS to define positive/negative examples. Default: True.

• anchor_generator (dict) – Config of anchor generator for ATSS.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## Example

>>> self = VFNetHead(11, 7)
>>> feats = [torch.rand(1, 7, s, s) for s in [4, 8, 16, 32, 64]]
>>> cls_score, bbox_pred, bbox_pred_refine = self.forward(feats)
>>> assert len(cls_score) == len(self.scales)

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

cls_scores (list[Tensor]): Box iou-aware scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

bbox_pred(list[Tensor]): Box offsets for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

bbox_pred_refine (list[Tensor]): Refined Box offsets for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

Return type tuple

forward_single(x, scale, scale_refine, stride, reg_denom)

Forward features of a single scale level.

## Parameters

• x (Tensor) – FPN feature maps of the specified stride.