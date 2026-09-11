## Parameters

• block (nn.Module) – block used to build ResLayer.

• inplanes (int) – inplanes of block.

• planes (int) – planes of block.

• num blocks (int) – number of blocks.

• stride (int) – stride of the first block. Default: 1

• avg_down (bool) – Use AvgPool instead of stride conv when downsampling in the bottleneck. Default: False

• conv_cfg(dict) – dictionary to construct and config conv layer. Default: None

• norm_cfg(dict) – dictionary to construct and configure norm layer. Default: dict(type='BN')

• downsample_first (bool) – Downsample at the first block or last block. False for Hourglass, True for ResNet. Default: True

class mmdet.models.utils.SELayer(channels, ratio=16, conv_cfg=None, act_cfg=('type': 'ReLU'), ('type': 'Sigmoid'), init_cfg=None)

Squeeze-and-Excitation Module.

## Parameters

• channels (int) – The input (and output) channels of the SE layer.

• ratio (int) – Squeeze ratio in SELayer, the intermediate channel will be int(channels/ratio). Default: 16.

• conv_cfg (None or dict) – Config dict for convolution layer. Default: None, which means using conv2d.

• act_cfg (dict or Sequence[dict]) – Config dict for activation layer. If act_cfg is a dict, two activation layers will be configured by this dict. If act_cfg is a sequence of dicts, the first activation layer will be configured by the first dict and the second activation layer will be configured by the second dict. Default: (dict(type='ReLU'), dict(type='Sigmoid'))

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.SimplifiedBasicBlock(inplanes, planes, stride=1, dilation=1, downsample=None, style='pytorch', with_cp=False, conv_cfg=None, norm_cfg='type': 'BN'), dcn=None, plugins=None, init_fg=None)

Simplified version of original basic residual block. This is used in SCNet.

• Norm layer is now optional

• Last ReLU in forward function is removed