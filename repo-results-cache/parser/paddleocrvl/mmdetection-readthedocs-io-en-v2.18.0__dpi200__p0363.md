loss(cls_scores, pts_preds_init, pts_preds_refine, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

## offset_to_pts(center_list, pred_list)

Change from point offset to point coordinate.

## points2bbox(pts, y_first=True)

Converting the points set into bounding box.

## Parameters

• pts – the input points sets (fields), each points set (fields) is represented as 2n scalar.

•  $ y_{first} $ – if  $ y_{first}=True $, the point set is represented as  $ [y_{1}, x_{1}, y_{2}, x_{2} \ldots y_{n}, x_{n}] $, otherwise the point set is represented as  $ [x_{1}, y_{1}, x_{2}, y_{2} \ldots x_{n}, y_{n}] $.

Returns each points set is converting to a bbox  $ [x_{1}, y_{1}, x_{2}, y_{2}] $.

(num_classes, in_channels, stacked_convs=4, conv_cfg=None, norm_cfg=None, anchor_generator={'octave_base_scale': 4, 'ratios': [0.5, 1.0, 2.0],'scales_per_octave': 3,'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'}, init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name':'retina_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs})

An anchor-based head used in RetinaNet.

The head contains two subnetworks. The first classifies anchor boxes and the second regresses deltas for the anchors.

## Example

>>> import torch

>>> self = RetinaHead(11, 7)

>>> x = torch.rand(1, 7, 32, 32)

>>> cls_score, bbox_pred = self.forward_single(x)

>>> # Each anchor predicts a score for each class except background
>>> cls_per_anchor = cls_score.shape[1] / self.num_anchors

>>> box_per_anchor = bbox_pred.shape[1] / self.num_anchors

>>> assert cls_per_anchor == (self.num_classes)

>>> assert box_per_anchor == 4