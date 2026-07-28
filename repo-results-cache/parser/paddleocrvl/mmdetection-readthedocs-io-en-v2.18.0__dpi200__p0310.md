class mmdet.models.dense_heads.AnchorFreeHead(num_classes, in_channels, feat_channels=256)

stacked_convs=4, strides=(4, 8, 16, 32, 64),

dcn_on_last_conv=False, conv_bias='auto',

loss_cls='{alpha': 0.25, 'gamma': 2.0, 'loss_weight': 1.0, 'type': 'FocalLoss', 'use_sigmoid': True},

loss_bbox={'loss_weight': 1.0, 'type': 'IoULoss'},

bbox_coder={'type': 'DistancePointBBoxCoder'},

conv_cfg=None, norm_cfg=None, train_cfg=None,

test_cfg=None, init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'conv_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'})

Anchor-free head (FCOS, Fovea, RepPoints, etc.).

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• feat channels (int) – Number of hidden channels. Used in child classes.

• stacked_convs (int) – Number of stacking convs of the head.

• strides (tuple) – Downsample factor of each feature map.

• dcn_on_last_conv (bool) – If true, use dcn in the last layer of towers. Default: False.

• conv_bias (bool / str) – If specified as auto, it will be decided by the norm_cfg. Bias of conv will be set as True if norm_cfg is None, otherwise False. Default: “auto”.

• loss_cls (dict) – Config of classification loss.

• loss_bbox(dict) – Config of localization loss.

• bbox_coder(dict) – Config of bbox coder. Defaults 'DistancePointBBoxCoder'.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• train_cfg(dict) – Training config of anchor head.

• test_cfg(dict) – Testing config of anchor head.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## aug_test(feats, img_metas, rescale=False)

Test function with test time augmentation.

## Parameters

• feats (list [Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains features for all images in the batch.

• img_metas (list[list[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch. each dict has image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

Returns bbox results of each class

Return type list[ndarray]

## forward(feats)

Forward features from the upstream network.