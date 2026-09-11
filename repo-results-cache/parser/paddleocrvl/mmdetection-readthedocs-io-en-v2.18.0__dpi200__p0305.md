## Parameters

• in channels (List[int]) – Number of input channels per scale.

• out_channels (int) – Number of output channels (used at each scale)

• num_outs (int) – Number of output scales.

• start_level (int) – Index of the start input backbone level used to build the feature pyramid. Default: 0.

• end_level (int) – Index of the end input backbone level (exclusive) to build the feature pyramid. Default: -1, which means the last level.

• add_extra_convs (bool / str) – If bool, it decides whether to add conv layers on top of the original feature maps. Default to False. If True, it is equivalent to add_extra_convs='on_input'. If str, it specifies the source feature map of the extra convs. Only the following options are allowed

– 'on_input': Last feat map of neck inputs (i.e. backbone feature).

– 'on lateral': Last feature map after lateral convs.

– 'on_output': The last output feature map after fpn convs.

• relu_before_extra_convs (bool) – Whether to apply relu before the extra conv. Default: False.

• no_norm_on_lateral (bool) – Whether to apply norm on lateral. Default: False.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• act_cfg(str) – Config dict for activation layer in ConvModule. Default: None.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

forward(inputs)

Forward function.

##### class mmdet.models.necks.RFP(Recursive Feature Pyramid)

This is an implementation of RFP in DetectoRS. Different from standard FPN, the input of RFP should be multi-level features along with origin input image of backbone.

## Parameters

• rfp_steps (int) – Number of unrolled steps of RFP.

• rfp_backbone (dict) – Configuration of the backbone for RFP.

• aspp_out_channels (int) – Number of output channels of ASPP module.

• aspp_dilations (tuple[int]) – Dilation rates of four branches. Default: (1, 3, 6, 1)

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

forward(inputs)

Forward function.

init_weights()

Initialize the weights.