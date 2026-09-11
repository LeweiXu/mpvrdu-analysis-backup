Parameters conv_to_res (bool, optional) – if True, change the conv layers to SimplifiedBasicBlock.

class mmdet.models.roi_heads.Shared2FCBBoxHead(fc_out_channels=1024, *args, **kwargs)

class mmdet.models.roi_heads.Shared4Conv1FCBBoxHead(fc_out_channels=1024, *args, **kwargs)

class mmdet.models.roi_heads.SingleRoIExtractor(roi_layer, out_channels, featmap_strides,

Extract RoI features from a single level feature map.

If there are multiple input feature levels, each RoI is mapped to a level according to its scale. The mapping rule is proposed in FPN.

## Parameters

• roi_layer(dict) – Specify RoI layer type and arguments.

• out channels (int) – Output channels of RoI layers.

• featmap_strides (List[int]) – Strides of input feature maps.

• finest_scale (int) – Scale threshold of mapping to level 0. Default: 56.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(feats, rois, roi_scale_factor=None)

Forward function.

## map_roi_levels(rois, num_levels)

Map rois to corresponding feature levels by scales.

• scale < finest_scale * 2: level 0

• finest_scale * 2 <= scale < finest_scale * 4: level 1

• finest_scale * 4 <= scale < finest_scale * 8: level 2

• scale >= finest_scale * 8: level 3

## Parameters

• rois (Tensor) – Input RoIs, shape (k, 5).

• num levels (int) – Total level number.

Returns Level index (0-based) of each RoI, shape (k, )

Return type Tensor

class mmdet.models.roi_heads.SparseRoIHead(num_stages=6, stage_loss_weights=(1, 1, 1, 1, 1),

(num_stages=6, stage_loss_weights=(1, 1, 1, 1, 1), proposal_feature_channel=256,

'out_channels': 256, 'roi_layer': {'output_size': 7,'sampling_ratio': 2, 'type': 'RoIAlign'}, 'type': 'SingleRoIExtractor'}, mask_roi_extractor=None, 'fbbox_head={dropout': 0.0, 'feedforward_channels': 2048, 'ffn_act_cfg': {'inplace': True, 'type': 'ReLU'}, 'hidden_channels': 256, 'num_classes': 80, 'num_cls_fcs': 1, 'num_fcs': 2, 'num_heads': 8, 'num_reg_fcs': 3, 'roi_feat_size': 7, 'type': 'DIIHead'}, mask_head=None, 'train_cfg=None', 'test_cfg=None', 'pretrained=None', 'init_cfg=None)

The RoIHead for Sparse R-CNN: End-to-End Object Detection with Learnable Proposals and Instances as