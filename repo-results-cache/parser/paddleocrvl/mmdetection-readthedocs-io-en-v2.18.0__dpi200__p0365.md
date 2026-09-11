class mmdet.models.dense_heads.SABLRetinaHead(num_classes, in_channels, stacked_convs=4,

feat_channels=256,

approx_anchor_generator={'octave_base_scale': 4,

'ratios': [0.5, 1.0, 2.0],'scales_per_octave': 3,'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'},

square_anchor_generator={'ratios': [1.0],'scales': [4],

'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'},

conv_cfg=None, norm_cfg=None,

bbox_coder={'num_ buckets': 14,'scale_factor': 3.0,

'type': 'BucketingBBoxCoder'},

reg_ decoded_bbox=False, train_cfg=None,

test_cfg=None, loss_cls={'alpha': 0.25, 'gamma': 2.0,

'loss_weight': 1.0, 'type': 'FocalLoss', 'use_sigmoid': True},

loss_bbox_cls={'loss_weight': 1.5, 'type': 'CrossEntropyLoss', 'use_sigmoid': True},

loss_bbox_reg={'beta': 0.111111111111111,

'loss_weight': 1.5, 'type': 'SmoothL1Loss'},

init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name':'retina_cls','std': 0.01, 'type': 'Normal'},

'std': 0.01, 'type': 'Normal'})

Side-Aware Boundary Localization (SABL) for RetinaNet.

The anchor generation, assigning and sampling in SABLRetinaHead are the same as GuidedAnchorHead for guided anchoring.

Please refer to https://arxiv.org/abs/1912.04260 for more details.

## Parameters

• num_classes (int) – Number of classes.

• in channels (int) – Number of channels in the input feature map.

• stacked_convs (int) – Number of Convs for classification and regression branches. Defaults to 4.

• feat channels (int) – Number of hidden channels. Defaults to 256.

• approx_anchor_generator (dict) – Config dict for approx generator.

• square_anchor_generator (dict) – Config dict for square generator.

• conv_cfg(dict) – Config dict for ConvModule. Defaults to None.

• norm_cfg(dict) – Config dict for Norm Layer. Defaults to None.

• bbox_coder(dict) – Config dict for bbox coder.

• reg_ decoded_bbox (bool) – If true, the regression loss would be applied directly on decoded bounding boxes, converting both the predicted boxes and regression targets to absolute coordinates format. Default False. It should be True when using IoULoss, GIoULoss, or DIoULoss in the bbox head.

• train_cfg(dict) – Training config of SABLRetinaHead.

• test_cfg(dict) – Testing config of SABLRetinaHead.

• loss_cls (dict) – Config of classification loss.

• loss_bbox_cls(dict) – Config of classification loss for bbox branch.

• loss_bbox_reg(dict) – Config of regression loss for bbox branch.