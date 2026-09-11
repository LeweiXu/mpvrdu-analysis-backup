• bbox_preds (list [Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list[Tensor]) – Ground truth bboxes of each image with shape (num_obj, 4).

- gt_labels (list[Tensor]) – Ground truth labels of each image with shape (num_obj, 4).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• gt_bboxes_ignore (list [Tensor]) – Ignored gt bboxes of each image. Default: None.

## Returns

Loss dict, comprise classification loss, regression loss and carl loss.

Return type dict

class mmdet.models.dense_heads.PISASSDHead(num_classes=80, in_channels=(512, 1024, 512, 256

256), stacked_convs=0, feat_channels=256,

use_depthwise=False, conv_cfg=None, norm_cfg=None,

act_cfg=None, anchor_generator='basesize_ratio_range': (0.1, 0.9), 'input_size': 300, 'ratios': ([2], [2, 3], [2, 3], [2, 3], [2], [2]),'scale_major': False,'strides': [8, 16, 32, 64, 100, 300], 'type': 'SSDAnchorGenerator'},

bbox_coder='clip_border': True, 'target_means': [0.0, 0.0, 0.0, 0.0], 'target_stds': [1.0, 1.0, 1.0, 1.0], 'type': 'DeltaXYWHBBoxCoder'}, reg_ decoded_bbox=False,

train_cfg=None, test_cfg=None, init_cfg='bias': 0,

'distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier'}

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list [Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list[Tensor]) – Ground truth bboxes of each image with shape (num_obj, 4).

- gt_labels (list[Tensor]) – Ground truth labels of each image with shape (num_obj, 4).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• gt_bboxes_ignore (list[Tensor]) – Ignored gt bboxes of each image. Default: None.

## Returns

Loss dict, comprise classification loss regression loss and carl loss.

Return type dict