forward_single(x)

Forward feature map of a single scale level.

class mmdet.models.dense_heads.GFLHead(num_classes, in_channels, stacked_convs=4, conv_cfg=None,

(num_classes, in_channels, stacked_convs=4, conv_cfg=None, norm_cfg='num_groups': 32,'requires_grad': True, 'type': 'GN'), loss_dfl='loss_weight': 0.25, 'type': 'DistributionFocalLoss'), bbox_coder='type': 'DistancePointBBoxCoder', reg_max=16, init_cfg='layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'gfl_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs): and Distributed Rounding Boxes for Dance Object Detection

Generalized Focal Loss: Learning Qualified and Distributed Bounding Boxes for Dense Object Detection.

GFL head structure is similar with ATSS, however GFL uses 1) joint representation for classification and localization quality, and 2) flexible General distribution for bounding box locations, which are supervised by Quality Focal Loss (QFL) and Distribution Focal Loss (DFL), respectively

https://arxiv.org/abs/2006.04388

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• stacked_convs (int) – Number of conv layers in cls and reg tower. Default: 4.

• conv_cfg(dict) – dictionary to construct and config conv layer. Default: None.

• norm_cfg(dict) – dictionary to construct and config norm layer. Default: dict(type='GN', num_groups=32, requires_grad=True).

• loss_qfl (dict) – Config of Quality Focal Loss (QFL).

• bbox_coder(dict) – Config of bbox coder. Defaults 'DistancePointBBoxCoder'.

• reg_max (int) – Max value of integral set :math:  $ \{0, \ldots, reg\_max\} $ in QFL setting. Default: 16.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## Example

>>> self = GFLHead(11, 7)
>>> feats = [torch.rand(1, 7, s, s) for s in [4, 8, 16, 32, 64]]
>>> cls_quality_score, bbox_pred = self.forward(feats)
>>> assert len(cls_quality_score) == len(self.scales)

## anchor center(anchors)

Get anchor centers from anchors.

Parameters anchors (Tensor) – Anchor list with shape (N, 4), “xyxy” format.

Returns Anchor centers with shape (N, 2), “xy” format.

Return type Tensor

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.