class mmdet.models.dense_heads.FCOSHead(num_classes, in_channels, regress_ranges=((-1, 64), (64, 128),

(num_classes, in_channels, regress_ranges=((- 1, 64), (64, 128), (128, 256), (256, 512), (512, 100000000.0)), center_sampling=False, center_sample_radius=1.5, norm_on_bbox=False, centerness_on_reg=False, loss_cls=\{alpha': 0.25, gamma': 2.0, loss_weight': 1.0, type': 'FocalLoss', 'use_sigmoid': True}, loss_bbox=\{loss_weight': 1.0, type': 'IoULoss'}, loss_centerness=\{loss_weight': 1.0, type': 'CrossEntropyLoss', 'use_sigmoid': True}, norm_cfg=\{num_groups': 32,'requires_grad': True, type': 'GN'}, init_cfg=\{layer': 'Conv2d', 'override': {bias_prob': 0.01, name': 'conv_cls','std': 0.01, type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs)

Anchor-free head used in FCOS.

The FCOS head does not use anchor boxes. Instead bounding boxes are predicted at each pixel and a centerness measure is used to suppress low-quality predictions. Here norm_on_bbox, centerness_on_reg, dcn_on_last_conv are training tricks used in official repo, which will bring remarkable mAP gains of up to 4.9. Please see https://github.com/tianzhi0549/FCOS for more detail.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• strides (list[int] | list[tuple[int, int]]) – Strides of points in multiple feature levels. Default: (4, 8, 16, 32, 64).

• regress_ranges (tuple[tuple[int, int]]) – Regress range of multiple level points.

• center sampling (bool) – If true, use center sampling. Default: False.

• center_sample_radius (float) – Radius of center sampling. Default: 1.5.

• norm_on_bbox (bool) – If true, normalize the regression targets with FPN strides. Default: False.

• centerness_on_reg (bool) – If true, position centerness on the regress branch. Please refer to https://github.com/tianzhi0549/FCOS/issues/89#issuecomment-516877042. Default: False.

• conv_bias (bool / str) – If specified as auto, it will be decided by the norm_cfg. Bias of conv will be set as True if norm_cfg is None, otherwise False. Default: “auto”.

• loss_cls (dict) – Config of classification loss.

• loss_bbox(dict) – Config of localization loss.

• loss_centerness (dict) – Config of centerness loss.

• norm_cfg (dict) – dictionary to construct and config norm layer. Default: norm_cfg=dict(type='GN', num_groups=32, requires_grad=True).

• init_cfg(dict or list[dict], optional) – Initialization config dict.