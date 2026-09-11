## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.PatchEmbed(in_channels=3, embed_dim=768, conv_type='Conv2d',

kernel_size=16, stride=16, padding='corner', dilation=1, bias=True, norm_cfg=None, input_size=None, init_cfg=None)

Image to Patch Embedding.

We use a conv layer to implement PatchEmbed.

## Parameters

• in channels (int) – The num of input channels. Default: 3

• embed_dims(int) – The dimensions of embedding. Default: 768

• conv_type (str) – The config dict for embedding conv layer type selection. Default: "Conv2d.

• kernel_size (int) – The kernel_size of embedding conv. Default: 16.

• stride (int) – The slide stride of embedding conv. Default: None (Would be set as kernel_size).

• padding (int | tuple | string) – The padding length of embedding conv. When it is a string, it means the mode of adaptive padding, support “same” and “corner” now. Default: “corner”.

• dilation (int) – The dilation rate of embedding conv. Default: 1.

• bias (bool) – Bias of embed conv. Default: True.

• norm_cfg (dict, optional) – Config dict for normalization layer. Default: None.

• input_size (int / tuple / None) – The size of input, which will be used to calculate the out size. Only work when dynamic_size is False. Default: None.

• init_cfg (mmcv.ConfigDict, optional) – The Config for initialization. Default: None.

## forward(x)

Parameters x (Tensor) – Has shape (B, C, H, W). In most cases, C is 3.

## Returns

Contains merged results and its spatial shape.

• x (Tensor): Has shape (B, out_h * out_w, embed_dims)

• out_size (tuple[int]): Spatial shape of x, arrange as (out_h, out_w).

Return type tuple

class mmdet.models.utils.ResLayer(block, inplanes, planes, num_blocks, stride=1, avg_down=False,

ResLayer to build ResNet style backbone.