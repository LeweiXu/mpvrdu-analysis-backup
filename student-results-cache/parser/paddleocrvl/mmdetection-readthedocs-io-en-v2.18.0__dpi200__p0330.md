class mmdet.models.dense_heads.DETRHead(num_classes, in_channels, num_query=100, num_reg_fcs=2)

(num_classes, in_channels, num_query=100, num_reg_fcs=2, transformer=None, sync_cls_avg_factor=False, positional_encoding='normalize': True, 'num_feats': 128, 'type': 'SinePositionalEncoding'), loss_cls={'bg_cls_weight': 0.1, 'class_weight': 1.0, 'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': False}, loss_bbox={'loss_weight': 5.0, 'type': 'L1Loss'}, loss_iou={'loss_weight': 2.0, 'type': 'GIoULoss'}, train_cfg={'assigner': {'cls_cost': {'type': 'ClassificationCost', 'weight': 1.0}, 'iou_cost': {'iou_mode': 'giou', 'type': 'IoUCost', 'weight': 2.0},'reg_cost': {'type': 'BBoxL1Cost', 'weight': 5.0}, 'type': 'HungarianAssigner'}, test_cfg={'max_per_img': 100}, init_cfg=None, **kwargs)

Implements the DETR transformer head.

See paper: End-to-End Object Detection with Transformers for details.

## Parameters

• num_classes (int) – Number of categories excluding the background.

• in channels (int) – Number of channels in the input feature map.

• num_query (int) – Number of query in Transformer.

• num_reg_fcs (int, optional) – Number of fully-connected layers used in FFN, which is then used for the regression head. Default 2.

• (obj (test_cfg) - `mmcv.ConfigDict`|dict): Config for transformer. Default: None.

• sync_cls_avg_factor (bool) – Whether to sync the avg_factor of all ranks. Default to False.

• (obj – `mmcv.ConfigDict` | dict): Config for position encoding.

• (obj – mmcv.ConfigDict |dict): Config of the classification loss. Default `CrossEntropyLoss.

• (obj – mmcv.ConfigDict `|dict): Config of the regression loss. Default `L1Loss.

• (obj – mmcv.ConfigDict `|dict): Config of the regression iou loss. Default `GIoULoss.

• (obj – `mmcv.ConfigDict` | dict): Training config of transformer head.

• (obj – `mmcv.ConfigDict` | dict): Testing config of transformer head.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(feats, img_metas)

Forward function.

## Parameters

• feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

• img_metas (list[dict]) – List of image information.

## Returns

Outputs for all scale levels.

• all_cls_scores_list (list[Tensor]): Classification scores for each scale level. Each is a 4D-tensor with shape [nb_dec, bs, num_query, cls_out_channels]. Note  $ cls\_out\_channels $ should include background.