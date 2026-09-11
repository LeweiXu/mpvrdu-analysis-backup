• scores (Tensor): Classification scores, has shape (num_instance,).

• labels (Tensor): Has shape (num_instances,).

• masks (Tensor): Processed mask results, has shape (num_instances, h, w).

## Return type list[InstanceData]

loss(mlvl_mask_preds, mlvl_cls_preds, gt_labels, gt_masks, img_metas, gt_bboxes=None, **kwargs) Calculate the loss of total batch.

## Parameters

- mlvl_mask_preds (list[Tensor]) – Multi-level mask prediction. Each element in the list has shape (batch_size, num_grids**2, h, w).

- mlvl_cls_preds (list[Tensor]) – Multi-level scores. Each element in the list has shape (batch_size, num_classes, num_grids, num_grids).

• gt_labels (list [Tensor]) – Labels of multiple images.

- gt_masks (list[Tensor]) – Ground truth masks of multiple images. Each has shape (num_instances, h, w).

• img_metas (list[dict]) – Meta information of multiple images.

• gt_bboxes (list[Tensor]) – Ground truth bboxes of multiple images. Default: None.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

resize_feats(feats)

Downsample the first feat and upsample last feat in feats.

class mmdet.models.dense_heads.SSDHead(num_classes=80, in_channels=(512, 1024, 512, 256, 256, 256),

(num_classes=80, in_channels=(512, 1024, 512, 256, 256, 256), stacked_convs=0, feat_channels=256, use_depthwise=False, conv_cfg=None, norm_cfg=None, act_cfg=None, anchor_generator='basesize_ratio_range': (0.1, 0.9), 'input_size': 300, 'ratios': ([2], [2, 3], [2, 3], [2, 3], [2], [2]),'scale_major': False,'strides': [8, 16, 32, 64, 100, 300], 'type': 'SSDAnchorGenerator'}, 'bbox_coder={clip_border': True, 'target_means': [0.0, 0.0, 0.0, 0.0], 'target_stds': [1.0, 1.0, 1.0, 1.0], 'type': 'DeltaXYWHBBoxCoder'},'reg_ decoded_bbox=False, train_cfg=None, test_cfg=None, init_cfg={bias': 0, 'distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier'})

SSD head used in https://arxiv.org/abs/1512.02325.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• stacked_convs (int) – Number of conv layers in cls and reg tower. Default: 0.

• feat_channels (int) – Number of hidden channels when stacked_convs > 0. Default: 256.

• use_depthwise(bool) – Whether to use DepthwiseSeparableConv. Default: False.

• conv_cfg(dict) – Dictionary to construct and config conv layer. Default: None.

• norm_cfg(dict) – Dictionary to construct and configure a config norm layer. Default: None.

• act_cfg(dict) – Dictionary to construct and configure activation layer. Default: None.