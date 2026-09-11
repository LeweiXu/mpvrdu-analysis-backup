- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single(cls_score, bbox_pred, anchors, labels, label_weights, bbox_targets, bbox_weights, num_total_samples)

Loss function on single scale.

refine_bboxes(anchor_list, bbox_preds, img_metas)

Refine bboxes through stages.

region_targets(anchor_list, valid_flag_list, gt_bboxes_list, img_metas, featmap_sizes, gt_bboxes_ignore_list=None, gt_labels_list=None, label_channels=1, unmap_outputs=True)

See StageCascadeRPNHead.get_targets().

class mmdet.models.dense_heads.VFNetHead(num_classes, in_channels, regress_ranges=((-1, 64), (64, 64), (-1, 6

(num_classes, in_channels, regress_ranges=((- 1, 64), (64, 128), (128, 256), (256, 512), (512, 100000000.0)), center_sampling=False, center_sample_radius=1.5, sync_num_pos=True, gradient_mul=0.1, bbox_norm_type='reg_denom', loss_cls_fl='alpha': 0.25, 'gamma': 2.0, 'loss_weight': 1.0, 'type': 'FocalLoss', 'use_sigmoid': True, use_vfl=True, loss_cls='alpha': 0.75, 'gamma': 2.0, 'iou_weighted': True, 'loss_weight': 1.0, 'type': 'VarifocalLoss', 'use_sigmoid': True, loss_bbox='loss_weight': 1.5, 'type': 'GIoULoss'}, loss_bbox_refine='loss_weight': 2.0, 'type': 'GIoULoss'}, norm_cfg='num_groups': 32,'requires_grad': True, 'type': 'GN'}, use_atss=True, reg_ decoded_bbox=True, anchor_generator='center_offset': 0.0, 'octave_base_scale': 8, 'ratios': [1.0],'scales_per_octave': 1,'strides': [8, 16, 32, 64, 128], 'type': 'AnchorGenerator'}, init_cfg='layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'vfnet_cls','std': 0.01, 'type': 'Normal'},'std': 0.01, 'type': 'Normal'}, **kwargs)

Head of  $ 'VarifocalNet $ (VFNet): An IoU-aware Dense Object Detector.<https://arxiv.org/abs/2008.13367>_.

The VFNet predicts IoU-aware classification scores which mix the object presence confidence and object localization accuracy as the detection score. It is built on the FCOS architecture and uses ATSS for defining positive/negative training examples. The VFNet is trained with Varifocal Loss and employs star-shaped deformable convolution to extract features for a bbox.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• regress_ranges (tuple[tuple[int, int]]) – Regress range of multiple level points.

• center sampling (bool) – If true, use center sampling. Default: False.