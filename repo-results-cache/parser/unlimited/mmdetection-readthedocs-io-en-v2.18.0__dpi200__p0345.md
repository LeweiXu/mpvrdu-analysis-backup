MMDetection, Release 2.18.0
class mmdet.models.dense_heads.FreeAnchorRetinaHead(num_classes, in_channels, stacked_convs=4,
conv_cfg=None, norm_cfg=None,
pre_anchor_topk=50, bbox_thr=0.6,
gamma=2.0, alpha=0.5, **kwargs)
FreeAnchor RetinaHead used in https://arxiv.org/abs/1909.02466.
Parameters
- num_classes (int) – Number of categories excluding the background category.
- in_channels (int) – Number of channels in the input feature map.
- stacked_convs (int) – Number of conv layers in cls and reg tower. Default: 4.
- conv_cfg (dict) – dictionary to construct and config conv layer. Default: None.
- norm_cfg (dict) – dictionary to construct and config norm layer. Default: norm_cfg=dict(type='GN', num_groups=32, requires_grad=True).
- pre_anchor_topk (int) – Number of boxes that be token in each bag.
- bbox_thr (float) – The threshold of the saturated linear function. It is usually the same with the IoU threshold used in NMS.
- gamma (float) – Gamma parameter in focal loss.
- alpha (float) – Alpha parameter in focal loss.
loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)
Compute losses of the head.
Parameters
- cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)
- bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)
- gt_bboxes (list[Tensor]) – each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.
- gt_labels (list[Tensor]) – class indices corresponding to each box
- img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.
- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.
Returns A dictionary of loss components.
Return type dict[str, Tensor]
negative_bag_loss(cls_prob, box_prob)
Compute negative bag loss.
\[
F L ((1 - P _ {a _ {j} \in A _ {+}}) * (1 - P _ {j} ^ {b g})).
\]
\(P_{a_j \in A_+}\): Box_probability of matched samples.
\(P_{j}^{bg}\): Classification probability of negative samples.
Parameters
- cls_prob (Tensor) – Classification probability, in shape (num_img, num_anchors, num_classes).
338
Chapter 39. mmdet.models