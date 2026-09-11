class mmdet.models.roi_heads.FusedSemanticHead(num_ins, fusion_level, num_convs=4,

(num_ins, fusion_level, num_convs=4,
in_channels=256, conv_out_channels=256,
num_classes=183, conv_cfg=None, norm_cfg=None,
ignore_label=None, loss_weight=None,
loss_seg='ignore_index': 255, 'loss_weight': 0.2,
'type': 'CrossEntropyLoss', init_cfg='override':
{'name': 'conv_logits'}, 'type': 'Kaiming'}

Multi-level fused semantic segmentation head.

in_1 -> 1x1 conv ---
in_2 -> 1x1 conv -- |
in_3 -> 1x1 conv - ||
in_4 -> 1x1 conv -----> 3x3 convs (*4)
in_5 -> 1x1 conv ---

## forward(feats)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.roi_heads.GenericRoIExtractor(aggregation='sum', pre_cfg=None, post_cfg=None, **kwargs)

Extract RoI features from all level feature maps levels.

This is the implementation of A novel Region of Interest Extraction Layer for Instance Segmentation.

## Parameters

• aggregation (str) – The method to aggregate multiple feature maps. Options are ‘sum’, ‘concat’. Default: ‘sum’.

• pre_cfg (dict / None) – Specify pre-processing modules. Default: None.

• post_cfg(dict / None) – Specify post-processing modules. Default: None.

• kwargs (keyword arguments) – Arguments that are the same as BaseRoIExtractor.

forward(feats, rois, roi_scale_factor=None)

Forward function.

class mmdet.models.roi_heads.GlobalContextHead(num_convs=4, in_channels=256,

conv_out_channels=256, num_classes=80,
loss_weight=1.0, conv_cfg=None, norm_cfg=None,
conv_to_res=False, init_cfg='override': {'name': 'fc'},
'std': 0.01, 'type': 'Normal'}

Global context head used in SCNet.

Parameters

• num_convs (int, optional) – number of convolutional layer in GlbCtxHead. Default: 4.