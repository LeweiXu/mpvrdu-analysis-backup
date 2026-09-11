MMDetection, Release 2.18.0
39.4 dense_heads
class mmdet.models.dense_heads.ATSSHead(num_classes, in_channels, stacked_convs=4, conv_cfg=None, norm_cfg={'num_groups': 32, 'requires_grad': True, 'type': 'GN'}, reg_decoded_bbox=True, loss_centerness={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'ats_cls', 'std': 0.01, 'type': 'Normal'}, 'std': 0.01, 'type': 'Normal'}, **kwargs)
Bridging the Gap Between Anchor-based and Anchor-free Detection via Adaptive Training Sample Selection.
ATSS head structure is similar with FCOS, however ATSS use anchor boxes and assign label by Adaptive Training Sample Selection instead max-iou.
https://arxiv.org/abs/1912.02424
forward(feats)
Forward features from the upstream network.
Parameters feats (tuple[Tensor]) - Features from the upstream network, each is a 4D-tensor.
Returns
Usually a tuple of classification scores and bbox prediction
cls_scores (list[Tensor]): Classification scores for all scale levels, each is a 4D-tensor, the channels number is num_anchors * num_classes.
bbox_preds (list[Tensor]): Box energies / deltas for all scale levels, each is a 4D-tensor, the channels number is num_anchors * 4.
Return type tuple
forward_single(x, scale)
Forward feature of a single scale level.
Parameters
- x (Tensor) – Features of a single scale level.
- ((scale) - obj: mmcv.cnn.Scale): Learnable scale module to resize the bbox prediction.
Returns
cls_score (Tensor): Cls scores for a single scale level the channels number is num_anchors * num_classes.
bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_anchors * 4.
centerness (Tensor): Centerness for a single scale level, the channel number is (N, num_anchors * 1, H, W).
Return type tuple
get_targets(anchor_list, valid_flag_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None, gt_labels_list=None, label_channels=1, unmap_outputs=True)
Get targets for ATSS head.
This method is almost the same as AnchorHead.get_targets(). Besides returning the targets as the parent method does, it also returns the anchors as the first element of the returned tuple.
39.4. dense_heads
301