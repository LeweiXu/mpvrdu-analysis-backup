• box_prob (Tensor) – Box probability, in shape (num_img, num_anchors, num_classes).

Returns Negative bag loss in shape (num_img, num_anchors, num_classes).

## Return type Tensor

positive_bag_loss(matched_cls_prob, matched_box_prob)

Compute positive bag loss.

 $ -log(Mean - max(P_{ij}^{cls} * P_{ij}^{loc})) $.

 $ P_{ij}^{cls} $: matched_cls_prob, classification probability of matched samples.

 $ P_{ij}^{loc} $: matched_box_prob, box probability of matched samples.

Parameters

• matched_cls_prob (Tensor) – Classification probability of matched samples in shape (num_gt, pre_anchor_topk).

• matched_box_prob (Tensor) – BBox probability of matched samples, in shape (num_gt, pre_anchor_topk).

Returns Positive bag loss in shape (num_gt,).

Return type Tensor

class mmdet.models.dense_heads.GARPNHead(in_channels, init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'conv_loc','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs})

Guided-Anchor-based RPN head.

forward_single(x)

Forward feature of a single scale level.

loss(cls_scores, bbox_preds, shape_preds, loc_preds, gt_bboxes, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.GARetinaHead(num_classes, in_channels, stacked_convs=4, conv_cfg=None, norm_cfg=None, init_cfg=None, **kwargs)

Guided-Anchor-based RetinaNet head.