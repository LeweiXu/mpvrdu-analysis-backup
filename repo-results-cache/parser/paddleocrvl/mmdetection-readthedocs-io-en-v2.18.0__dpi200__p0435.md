• (obj (init_cfg) - mmcv.ConfigDict): The Config for initialization. Default: None.

forward(param_feature, input_feature)

Forward function for DynamicConv.

## Parameters

• param_feature (Tensor) – The feature can be used to generate the parameter, has shape (num_all_proposals, in_channels).

• input_feature (Tensor) – Feature that interact with parameters, has shape (num_all_proposals, in_channels, H, W).

Returns The output feature has shape (num_all_proposals, out_channels).

Return type Tensor

class mmdet.models.utils.InvertedResidual(in_channels, out_channels, mid_channels, kernel_size=3,

stride=1, se_cfg=None, with_expand_conv=True,

Inverted Residual Block.

## Parameters

• in channels (int) – The input channels of this Module.

• out channels (int) – The output channels of this Module.

• mid channels (int) – The input channels of the depthwise convolution.

• kernel_size (int) – The kernel size of the depthwise convolution. Default: 3.

• stride (int) – The stride of the depthwise convolution. Default: 1.

• se_cfg(dict) – Config dict for the layer. Default: None, which means no set layer.

• with_expand_conv (bool) – Use expand conv or not. If set False, mid_channels must be the same with in_channels. Default: True.

• conv_cfg(dict) – Config dict for convolution layer. Default: None, which means using conv2d.

• norm_cfg(dict) – Config dict for normalization layer. Default: dict(type='BN').

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='ReLU').

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed. Default: False.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

Returns The output tensor.

Return type Tensor

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.