get_target(approx_list, inside_flag_list, square_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None, gt_labels_list=None, label_channels=None, sampling=True, unmap_outputs=True)

Compute bucketing targets. :param approx_list: Multi level approx of each image. :type approx_list: list[list] :param inside_flag_list: Multi level inside flags of each

image.

## Parameters

• square_list (list[list]) – Multi level squares of each image.

• gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.

• img_metas (list[dict]) – Meta info of each image.

• gt_bboxes_ignore_list (list[Tensor]) – ignore list of gt bboxes.

• gt_bboxes_list – Gt bboxes of each image.

• label channels (int) – Channel of label.

• sampling (bool) – Sample Anchors or not.

• unmap outputs (bool) – unmap outputs or not.

## Returns

Returns a tuple containing learning targets.

• labels_list (list[Tensor]): Labels of each level.

• label_weights_list (list[Tensor]): Label weights of each level.

• bbox_cls_targets_list (list[Tensor]): BBox cls targets of each level.

• bbox_cls_weights_list (list[Tensor]): BBox cls weights of each level.

• bbox_reg_targets_list (list[Tensor]): BBox reg targets of each level.

• bbox_reg_weights_list (list[Tensor]): BBox reg weights of each level.

• num_total_pos (int): Number of positive samples in all images.

• num_total_neg (int): Number of negative samples in all images.

Return type tuple

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

class mmdet.models.dense_heads.SOLOHead(num_classes, in_channels, feat_channels=256,

stacked_convs=4, strides=(4, 8, 16, 32, 64), scale_ranges=((8, 32), (16, 64), (32, 128), (64, 256), (128, 512)), pos_scale=0.2, num_grids=[40, 36, 24, 16, 12], cls_down_index=0, loss_mask=None, loss_cls=None, norm_cfg='num_groups': 32,'requires_grad': True, 'type': 'GN', train_cfg=None, test_cfg=None, init_cfg=[['type': 'Normal', 'layer': 'Conv2d','std': 0.01}, {'type': 'Normal','std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_mask_list'}}, {'type': 'Normal','std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_cls'}]])

SOLO mask head used in `SOLO: Segmenting Objects` by Locations.

<https://arxiv.org/abs/1912.04488>