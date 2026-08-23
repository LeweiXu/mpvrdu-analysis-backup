loss(cls_scores, bbox_preds, centernesses, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

• centernesses (list\[Tensor]) – centerness for each scale level, each is a 4D-tensor, the channel number is num_points * 1.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.FSAFHead(*args, score_threshold=None, init_cfg=None, **kwargs) Anchor-free head used in FSAF.

The head contains two subnetworks. The first classifies anchor boxes and the second regresses deltas for the anchors (num_anchors is 1 for anchor-free methods)

## Parameters

• *args – Same as its base class in RetinaHead

- score_threshold(float, optional) – The score_threshold to calculate positive recall. If given, prediction scores lower than this value is counted as incorrect prediction. Default to None.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

• **kwargs – Same as its base class in RetinaHead

## Example

>>> import torch

>>> self = FSAFHead(11, 7)

>>> x = torch.rand(1, 7, 32, 32)

>>> cls_score, bbox_pred = self.forward_single(x)

>>> # Each anchor predicts a score for each class except background
>>> cls_per_anchor = cls_score.shape[1] / self.num_anchors

>>> box_per_anchor = bbox_pred.shape[1] / self.num_anchors

>>> assert cls_per_anchor == self.num_classes

>>> assert box_per_anchor == 4

calculate_pos_recall(cls_scores, labels_list, pos_inds)

Calculate positive recall with score threshold.