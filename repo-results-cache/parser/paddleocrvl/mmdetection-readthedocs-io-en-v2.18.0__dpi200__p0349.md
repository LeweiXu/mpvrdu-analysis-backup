## Parameters

• anchors (Tensor) – Box reference for each scale level with shape (N, num_total_anchors, 4).

• cls_score (Tensor) – Cls and quality joint scores for each scale level has shape (N, num_classes, H, W).

• bbox_pred (Tensor) – Box distribution logits for each scale level with shape  $ (N, 4*(n+1), H, W) $, n is max value of integral set.

• labels (Tensor) – Labels of each anchor with shape (N, num_total_anchors).

• label_weights (Tensor) – Label weights of each anchor with shape (N, num_total_anchors)

• bbox_targets (Tensor) – BBox regression targets of each anchor weight shape (N, num_total_anchors, 4).

• stride (tuple) – Stride in this scale level.

• num_total_samples (int) – Number of positive samples that is reduced over all GPUs.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.GuidedAnchorHead(num_classes, in_channels, feat_channels=256)

approx_anchor_generator='octave_base_scale': 8,

'ratios': [0.5, 1.0, 2.0],'scales_per_octave': 3,

'strides': [4, 8, 16, 32, 64], 'type': 'AnchorGenerator',

'square_anchor_generator':['ratios': [1.0],'scales': [8],'strides': [4, 8, 16, 32, 64], 'type': 'AnchorGenerator'},

'anchor_coder={target_means': [0.0, 0.0, 0.0, 0.0],

'type': 'DeltaXYWHBBoxCoder'},

'bbox_coder={target_means': [0.0, 0.0, 0.0, 0.0],

'target_stds': [1.0, 1.0, 1.0, 1.0],

'type': 'DeltaXYWHBBoxCoder'},

reg_ decoded_bbox=False,

'deform_groups=4, loc_filter_thr=0.01,

train_cfg=None, test_cfg=None, loss_loc={'alpha': 0.25, 'gamma': 2.0, 'loss_weight': 1.0, 'type': 'FocalLoss', 'use_sigmoid': True},

'loss_shape={'beta': 0.2, 'loss_weight': 1.0, 'type': 'BoundedIoULoss'},

'loss_cls={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True},

'loss_bbox={'beta': 1.0, 'loss_weight': 1.0, 'type': 'SmoothL1Loss'},

'init_cfg={'layer': 'Conv2d',

'override': {'bias_prob': 0.01, 'name': 'conv_loc',

'std': 0.01, 'type': 'Normal'},

'std': 0.01, 'type': 'Normal'}}

Guided-Anchor-based head (GA-RPN, GA-RetinaNet, etc.).

This GuidedAnchorHead will predict high-quality feature guided anchors and locations where anchors will be kept in inference. There are mainly 3 categories of bounding-boxes.

• Sampled 9 pairs for target assignment. (approxes)

• The square boxes where the predicted anchors are based on. (squares)

• Guided anchors.