• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_points * 4, H, W).

- score_factors (list[Tensor]) – score_factors for each s cale level with shape (N, num_points * 1, H, W). Default: None.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc. Default: None.

• with_nms (bool) – Whether apply nms to the bboxes. Default: True.

Returns When with_nms is True, it is tuple[Tensor, Tensor], first tensor bboxes with shape [N, num_det, 5], 5 arrange as (x1, y1, x2, y2, score) and second element is class labels of shape [N, num_det]. When with_nms is False, first tensor is bboxes with shape [N, num_det, 4], second tensor is raw score has shape [N, num_det, num_classes].

Return type tuple[Tensor, Tensor] | list[tuple]

class mmdet.models.dense_heads.YOLOXHead(num_classes, in_channels, feat_channels=256,

stacked_convs=2, strides=[8, 16, 32], use_depthwise=False, dcn_on_last_conv=False, conv_bias='auto', conv_cfg=None, norm_cfg='{eps': 0.001,'momentum': 0.03, 'type': 'BN'}, act_cfg='{type': 'Swish'}, loss_cls='loss_weight': 1.0,'reduction':'sum', 'type': 'CrossEntropyLoss', 'use_sigmoid': True, loss_bbox='{eps': 1e-16, 'loss_weight': 5.0,'mode':'square','reduction':'sum', 'type': 'IoULoss'}, loss_obj='{loss_weight': 1.0,'reduction':'sum', 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_l1='{loss_weight': 1.0,'reduction':'sum', 'type': 'L1Loss'}, train_cfg=None, test_cfg=None, init_cfg='{a': 2.23606797749979, 'distribution': 'uniform', 'layer': 'Conv2d','mode': 'fan_in', 'nonlinearity': 'leaky_relu', 'type': 'Kaiming'})

YOLOXHead head used in YOLOX.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• feat channels (int) – Number of hidden channels in stacking convs. Default: 256

• stacked_convs (int) – Number of stacking convs of the head. Default: 2.

• strides (tuple) – Downsample factor of each feature map.

• use_depthwise(bool) – Whether to depthwise separable convolution in blocks. Default: False

• dcn_on_last_conv (bool) – If true, use dcn in the last layer of towers. Default: False.

• conv_bias (bool / str) – If specified as auto, it will be decided by the norm_cfg. Bias of conv will be set as True if norm_cfg is None, otherwise False. Default: “auto”.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• act_cfg(dict) – Config dict for activation layer. Default: None.

• loss_cls (dict) – Config of classification loss.

• loss_bbox(dict) – Config of localization loss.