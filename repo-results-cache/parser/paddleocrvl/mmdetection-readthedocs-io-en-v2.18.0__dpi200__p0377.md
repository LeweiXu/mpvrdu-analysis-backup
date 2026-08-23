- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

property num_anchors

Returns: int: Number of anchors on each point of feature map.

star_dcn_offset(bbox_pred, gradient_mul, stride)

Compute the star deformable conv offsets.

## Parameters

• bbox_pred (Tensor) – Predicted bbox distance offsets (l, r, t, b).

• gradient_mul (float) – Gradient multiplier.

• stride (int) – The corresponding stride for feature maps, used to project the bbox onto the feature map.

Returns The offsets for deformable convolution.

Return type dcn offsets (Tensor)

transform_bbox_targets( decoded_bboxes, mlvl_points, num_imgs)

Transform bbox_targets (x1, y1, x2, y2) into (l, t, r, b) format.

## Parameters

• decoded_bboxes (list[Tensor]) – Regression targets of each level, in the form of (x1, y1, x2, y2).

- mvl_points (list[Tensor]) – Points of each fpn level, each has shape (num_points, 2).

• num_imgs(int) – the number of images in a batch.

## Returns

Regression targets of each level in the form of  $ (l, t, r, b) $.

Return type bbox targets (list[Tensor])

class mmdet.models.dense_heads.YOLACTHead(num_classes, in_channels,

anchor_generator={'octave_base_scale': 3, 'ratios': [0.5, 1.0, 2.0],'scales_per_octave': 1,'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'}, loss_cls={'loss_weight': 1.0,'reduction': 'none', 'type': 'CrossEntropyLoss', 'use_sigmoid': False}, loss_bbox={'beta': 1.0, 'loss_weight': 1.5, 'type': 'SmoothL1Loss'}, num_head_convs=1, num_protos=32, use_ohem=True, conv_cfg=None, norm_cfg=None, init_cfg={'bias': 0, 'distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier'}, **kwargs)

YOLACT box head used in https://arxiv.org/abs/1904.02689.