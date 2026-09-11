• across skip trans (dict) – Across-pathway skip connection.

• output_trans(dict) – Transition that trans the output of the last stage.

• start_level (int) – Index of the start input backbone level used to build the feature pyramid. Default: 0.

• end_level (int) – Index of the end input backbone level (exclusive) to build the feature pyramid. Default: -1, which means the last level.

• add_extra_convs (bool) – It decides whether to add conv layers on top of the original feature maps. Default to False. If True, its actual mode is specified by extra_convs_on_inputs.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(inputs)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.necks.FPN(in_channels, out_channels, num_outs, start_level=0, end_level=-1,

add_extra_convs=False, relu_before_extra_convs=False,

no_norm_on_lateral=False, conv_cfg=None, norm_cfg=None, act_cfg=None,

upsample_cfg='mode': 'nearest'}, init_cfg='distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier')

Feature Pyramid Network.

This is an implementation of paper Feature Pyramid Networks for Object Detection.

## Parameters

• in channels (List[int]) – Number of input channels per scale.

• out_channels (int) – Number of output channels (used at each scale)

• num_outs (int) – Number of output scales.

• start_level (int) – Index of the start input backbone level used to build the feature pyramid. Default: 0.

• end_level (int) – Index of the end input backbone level (exclusive) to build the feature pyramid. Default: -1, which means the last level.

• add_extra_convs (bool | str) – If bool, it decides whether to add conv layers on top of the original feature maps. Default to False. If True, it is equivalent to add_extra_convs='on_input'. If str, it specifies the source feature map of the extra convs. Only the following options are allowed

– 'on_input': Last feat map of neck inputs (i.e. backbone feature).

– 'on lateral': Last feature map after lateral convs.

– 'on_output': The last output feature map after fpn convs.

• relu_before_extra_convs (bool) – Whether to apply relu before the extra conv. Default: False.