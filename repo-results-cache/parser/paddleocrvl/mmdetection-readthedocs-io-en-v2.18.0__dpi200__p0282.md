## Example

>>> from mmdet.models import Darknet
>>> import torch
>>> self = Darknet(depth=53)
>>> self.eval()
>>> inputs = torch.rand(1, 3, 416, 416)
>>> level_outputs = self.forward(inputs)
>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))
...
(1, 256, 52, 52)
(1, 512, 26, 26)
(1, 1024, 13, 13)

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

static make_conv_res_block(in_channels, out_channels, res_repeat, conv_cfg=None,

norm_cfg={'requires_grad': True, 'type': 'BN'}, act_cfg={'negative_slope': 0.1, 'type': 'LeakyReLU'})

In Darknet backbone, ConvLayer is usually followed by ResBlock. This function will make that. The Conv layers always have  $ 3 \times 3 $ filters with stride=2. The number of the filters in Conv layer is the same as the out channels of the ResBlock.

## Parameters

• in channels (int) – The number of input channels.

• out channels (int) – The number of output channels.

• res_repeat(int) – The number of ResBlocks.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg (dict) – Dictionary to construct and config norm layer. Default: dict(type='BN', requires_grad=True)

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='LeakyReLU', negative_slope=0.1).

## train(mode=True)

Sets the module in training mode.

This has any effect only on certain modules. See documentations of particular modules for details of their behaviors in training/evaluation mode, if they are affected, e.g. Dropout, BatchNorm, etc.

Parameters mode (bool) – whether to set training mode (True) or evaluation mode (False). Default: True.

Returns self

Return type Module