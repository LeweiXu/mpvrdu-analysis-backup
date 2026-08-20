class mmdet.models.dense_heads.YOLOV3Head(num_classes, in_channels, out_channels=(1024, 512, 256),

anchor_generator='base_sizes': [[(116, 90), (156, 198), (373, 326)], [(30, 61), (62, 45), (59, 119)], [(10, 13), (16, 30), (33, 23)]],'strides': [32, 16, 8], 'type': 'YOLOAnchorGenerator'}, 'box_coder': ['type': 'YOLOBBoxCoder'], 'featmap_strides': [32, 16, 8], one_hot_smoother=0.0, conv_cfg=None, norm_cfg=['requires_grad': True, 'type': 'BN'], act_cfg=['negative_slope': 0.1, 'type': 'LeakyReLU'], loss_cls=['loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_conf=['loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_xy=['loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_wh=['loss_weight': 1.0, 'type': 'MSELoss'}, train_cfg=None, test_cfg=None, init_cfg=['override': {'name': 'convs_pred'},'std': 0.01, 'type': 'Normal'})

YOLOV3Head Paper link: https://arxiv.org/abs/1804.02767.

## Parameters

• num_classes (int) – The number of object classes (w/o background)

• in channels (List[int]) – Number of input channels per scale.

• out_channels (List[int]) – The number of output channels per scale before the final 1x1 layer. Default: (1024, 512, 256).

• anchor_generator (dict) – Config dict for anchor generator

• bbox_coder(dict) – Config of bounding box coder.

- featmap_strides (List[int]) – The stride of each scale. Should be in descending order. Default: (32, 16, 8).

• one_hot_smoother (float) – Set a non-zero value to enable label-smooth Default: 0.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Dictionary to construct and config norm layer. Default: dict(type='BN', requires_grad=True)

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='LeakyReLU', negative_slope=0.1).

• loss_cls (dict) – Config of classification loss.

• loss_conf(dict) – Config of confidence loss.

• loss_xy(dict) – Config of xy coordinate loss.

• loss_wh(dict) – Config of wh coordinate loss.

• train_cfg(dict) – Training config of YOLOv3 head. Default: None.

• test_cfg(dict) – Testing config of YOLOv3 head. Default: None.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## aug_test(feats, img_metas, rescale=False)

Test function with test time augmentation.

Parameters