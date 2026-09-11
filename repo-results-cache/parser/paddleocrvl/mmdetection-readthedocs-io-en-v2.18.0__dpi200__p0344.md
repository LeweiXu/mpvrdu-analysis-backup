Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.dense_heads.FoveaHead(num_classes, in_channels, base_edge_list=(16, 32, 64, 128, 256), scale_ranges=((8, 32), (16, 64), (32, 128), (64, 256), (128, 512)), sigma=0.4, with_deform=False, deform_groups=4, init_cfg='layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'conv_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs)

FoveaBox: Beyond Anchor-based Object Detector https://arxiv.org/abs/1904.03797

## forward_single(x)

Forward features of a single scale level.

Parameters x (Tensor) – FPN feature maps of the specified stride.

## Returns

Scores for each class, bbox predictions, features after classification and regression conv layers, some models need these features like FCOS.

## Return type tuple

get_targets(gt_bbox_list, gt_label_list, featmap_sizes, points)

Compute regression, classification and centerness targets for points in multiple images.

## Parameters

• points (list [Tensor]) – Points of each fpn level, each has shape (num_points, 2).

- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

- gt_labels_list (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

loss(cls_scores, bbox_preds, gt_bbox_list, gt_label_list, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.