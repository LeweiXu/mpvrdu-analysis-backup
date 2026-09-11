MMDetection, Release 2.18.0
- cls_score (Tensor) - Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W).
- bbox_pred (Tensor) - Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W).
- anchors (Tensor) – Box reference for each scale level with shape (N, num_total_anchors, 4).
- labels (Tensor) – Labels of each anchors with shape (N, num_total_anchors).
- label_weights (Tensor) - Label weights of each anchor with shape (N, num_total_anchors)
- bbox_targets (Tensor) – BBox regression targets of each anchor weight shape (N, num_total_anchors, 4).
- bbox_weights (Tensor) – BBox regression loss weights of each anchor with shape (N, num_total_anchors, 4).
- num_total_samples (int) – If sampling, num total samples equal to the number of total anchors; Otherwise, it is the number of positive anchors.
Returns A dictionary of loss components.
Return type dict[str, Tensor]
class mmdet.models.dense_heads.AutoAssignHead(*args, force_topk=False, topk=9,
pos_loss_weight=0.25, neg_loss_weight=0.75,
center_loss_weight=0.75, **kwargs)
AutoAssignHead head used in AutoAssign.
More details can be found in the paper.
Parameters
- force_topk (bool) – Used in center prior initialization to handle extremely small gt. Default is False.
- topk (int) – The number of points used to calculate the center prior when no point falls in gt_bbox. Only work when force_topk if True. Defaults to 9.
- pos_loss_weight (float) – The loss weight of positive loss and with default value 0.25.
- neg_loss_weight (float) – The loss weight of negative loss and with default value 0.75.
- center_loss_weight (float) – The loss weight of center prior loss and with default value 0.75.
forward_single(x, scale, stride)
Forward features of a single scale level.
Parameters
- x (Tensor) – FPN feature maps of the specified stride.
- ((scale) - obj: mmcv.cnn.Scale): Learnable scale module to resize the bbox prediction.
- stride (int) – The corresponding stride for feature maps, only used to normalize the bbox prediction when self.norm_on_bbox is True.
Returns scores for each class, bbox predictions and centerness predictions of input feature maps.
Return type tuple
308
Chapter 39. mmdet.models