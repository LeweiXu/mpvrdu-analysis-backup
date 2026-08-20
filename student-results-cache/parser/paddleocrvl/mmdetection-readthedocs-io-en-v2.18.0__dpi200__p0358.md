conv_cfg=None, norm_cfg=None,

anchor_generator={'octave_base_scale': 4, 'ratios': [0.5, 1.0, 2.0],'scales_per_octave': 3,'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'},

init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name':'retina_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs)

• label_weight (Tensor): Classification loss weight of each anchor after paa assign, with shape (num_anchors).

• bbox_weight (Tensor): Bbox weight of each anchor with shape (num_anchors, 4).

• num_pos (int): The number of positive samples after paa assign.

## Return type tuple

score_voting(det_bboxes, det_labels, mlvl_bboxes, mlvl_nms_scores, score_thr)

Implementation of score voting method works on each remaining boxes after NMS procedure.

## Parameters

• det_bboxes (Tensor) – Remaining boxes after NMS procedure, with shape  $ (k, 5) $, each dimension means  $ (x_{1}, y_{1}, x_{2}, y_{2}, \text{score}) $.

• det_labels (Tensor) – The label of remaining boxes, with shape  $ (k, 1) $,Labels are 0-based.

- mlvI_bboxes (Tensor) – All boxes before the NMS procedure, with shape (num_anchors,4).

- mlvI_nms_scores (Tensor) – The scores of all boxes which is used in the NMS procedure, with shape (num_anchors, num_class)

• score_thr (float) – The score threshold of bboxes.

## Returns

Usually returns a tuple containing voting results.

• det_bboxes_voted (Tensor): Remaining boxes after score voting procedure, with shape  $ (k, 5) $, each dimension means  $ (x1, y1, x2, y2, \text{score}) $.

• det_labels_voted (Tensor): Label of remaining bboxes after voting, with shape (num_anchors,).

Return type tuple

class mmdet.models.dense_heads.PISARetinaHead(num_classes, in_channels, stacked_convs=4,

PISA Retinanet Head.

The head owns the same structure with Retinanet Head, but differs in two aspects: 1. Importance-based Sample Reweighting Positive (ISR-P) is applied to

change the positive loss weights.

2. Classification-aware regression loss is adopted as a third loss.

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)