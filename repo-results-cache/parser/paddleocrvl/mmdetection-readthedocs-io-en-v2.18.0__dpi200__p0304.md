• in channels (List[int]) – Number of input channels per scale.

• out_channels (int) – Number of output channels (used at each scale)

• num_outs (int) – Number of output scales.

• start_level (int) – Index of the start input backbone level used to build the feature pyramid. Default: 0.

• end_level (int) – Index of the end input backbone level (exclusive) to build the feature pyramid. Default: -1, which means the last level.

• add_extra_convs (bool) – It decides whether to add conv layers on top of the original feature maps. Default to False. If True, its actual mode is specified by extra_convs_on_inputs.

• conv_cfg(dict) – dictionary to construct and config conv layer.

• norm_cfg(dict) – dictionary to construct and configure norm layer.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(inputs)

Forward function.

## init_weights()

Initialize the weights of module.

class mmdet.models.necks.NASFPN(in_channels, out_channels, num_outs, stack_times, start_level=0, end_level=-1, add_extra_convs=False, norm_cfg=None, init_cfg='layer': 'Conv2d', 'type': 'Caffe2Xavier')

## NAS-FPN

Implementation of NAS-FPN: Learning Scalable Feature Pyramid Architecture for Object Detection

## Parameters

• in channels (List[int]) – Number of input channels per scale.

• out_channels (int) – Number of output channels (used at each scale)

• num_outs (int) – Number of output scales.

• stack_times (int) – The number of times the pyramid architecture will be stacked.

• start_level (int) – Index of the start input backbone level used to build the feature pyramid. Default: 0.

• end_level (int) – Index of the end input backbone level (exclusive) to build the feature pyramid. Default: -1, which means the last level.

• add_extra_convs (bool) – It decides whether to add conv layers on top of the original feature maps. Default to False. If True, its actual mode is specified by extra_convs_on_inputs.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(inputs)

Forward function.

class mmdet.models.necks.PAFPN(in_channels, out_channels, num_outs, start_level=0, end_level=-1, add_extra_convs=False, relu_before_extra_convs=False, no_norm_on_lateral=False, conv_cfg=None, norm_cfg=None, act_cfg=None, init_cfg='distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier')

Path Aggregation Network for Instance Segmentation.

This is an implementation of the PAFPN in Path Aggregation Network.