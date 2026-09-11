• conv_cfg (dict, optional) – Config dict for convolution layer. Default: None, which means using conv2d.

• norm_cfg(dict) – Config dict for normalization layer. Default: dict(type='BN')

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='Swish')

forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.ConvUpsample(in_channels, inner_channels, num_layers=1,

num_upsample=None, conv_cfg=None, norm_cfg=None,

init_cfg=None, **kwargs)

ConvUpsample performs 2x upsampling after Conv.

There are several ConvModule layers. In the first few layers, upsampling will be applied after each layer of convolution. The number of upsampling must be no more than the number of ConvModule layers.

## Parameters

• in channels (int) – Number of channels in the input feature map.

• inner channels (int) – Number of channels produced by the convolution.

• num_layers (int) – Number of convolution layers.

• num_upsample (int / optional) – Number of upsampling layers. Must be no more than num_layers. Upsampling will be applied after the first num_upsample layers of convolution. Default: num_layers.

• conv_cfg(dict) – Config dict for convolution layer. Default: None, which means using conv2d.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• init_cfg(dict) – Config dict for initialization. Default: None.

• kwargs (key word augments) – Other augments used in ConvModule.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.DetrTransformerDecoder(*args, post_norm_cfg = {'type': 'LN'},

return intermediate=False, **kwargs)

Implements the decoder in DETR transformer.

Parameters

• return intermediate (bool) – Whether to return intermediate outputs.