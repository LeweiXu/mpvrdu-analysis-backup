- gt_masks (BitmapMask | PolygonMask) – Gt masks (the whole instance) of each image, with the same shape of the input image.

• mask pred (Tensor) – Predicted masks of each positive proposal, shape (num_pos, h, w).

• mask targets (Tensor) – Gt mask of each positive proposal, binary map of the shape (num_pos, h, w).

• rcnn_train_cfg(dict) – Training config for R-CNN part.

Returns mask iou target (length == num positive).

Return type Tensor

class mmdet.models.roi_heads.MaskPointHead(num_classes, num_fcs=3, in_channels=256)

(num_classes, num_fcs=3, in_channels=256, fc_channels=256, class_agnostic=False, coarse_pred_each_layer=True, conv_cfg='type': 'Conv1d'), norm_cfg=None, act_cfg='type': 'ReLU'), loss_point='loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_mask': True, init_cfg='override': {'name': 'fc_logits'},'std': 0.001, 'type': 'Normal'}

A mask point head use in PointRend.

MaskPointHead uses shared multi-layer perceptron (equivalent to nn.Conv1d) to predict the logit of input points. The fine-grained feature and coarse feature will be concatenated together for prediction.

## Parameters

• num_fcs (int) – Number of fc layers in the head. Default: 3.

• in channels (int) – Number of input channels. Default: 256.

• fc channels (int) – Number of fc channels. Default: 256.

• num_classes (int) – Number of classes for logits. Default: 80.

• class_agnostic (bool) – Whether use class agnostic classification. If so, the output channels of logits will be 1. Default: False.

• coarse_pred_each_layer (bool) – Whether concatenate coarse feature with the output of each fc layer. Default: True.

• conv_cfg (dict / None) – Dictionary to construct and config conv layer. Default: dict(type='Conv1d'))

• norm_cfg(dict / None) – Dictionary to construct and configure a config norm layer. Default: None.

• loss_point(dict) – Dictionary to construct and config loss layer of point head. Default: dict(type='CrossEntropyLoss', use_mask=True, loss_weight=1.0).

• init_cfg(dict or list[dict], optional) – Initialization config dict.

forward(fine_grained_feats, coarse_feats)

Classify each point base on fine grained and coarse feats.

## Parameters

- fine_grained_feats (Tensor) – Fine grained feature sampled from FPN, shape (num_rois, in_channels, num_points).

• coarse_feats (Tensor) – Coarse feature sampled from CoarseMaskHead, shape (num_rois, num_classes, num_points).

## Returns

Point classification results, shape (num_rois, num_class, num_points).