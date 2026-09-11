class mmdet.models.backbones.MobileNetV2(widen_factor=1.0, out_indices=(1, 2, 4, 7), frozen_stages=-1, conv_cfg=None, norm_cfg='type': 'BN'), act_cfg='type': 'ReLU6'), norm_eval=False, with_cp=False, pretrained=None, init_cfg=None)

## Example

>>> from mmdet.models import HourglassNet
>>> import torch
>>> self = HourglassNet()
>>> self.eval()
>>> inputs = torch.rand(1, 3, 511, 511)
>>> level_outputs = self.forward(inputs)
>>> for level_output in level_outputs:
...     print(tuple(level_output.shape))
(1, 256, 128, 128)
(1, 256, 128, 128)

forward(x)
Forward function.
init_weights()
Init module weights.

MobileNetV2 backbone.

## Parameters

• widen_factor (float) – Width multiplier, multiply number of channels in each layer by this amount. Default: 1.0.

• out_indices (Sequence[int], optional) – Output from which stages. Default: (1, 2, 4, 7).

• frozen_stages (int) – Stages to be frozen (all param fixed). Default: -1, which means not freezing any parameters.

• conv_cfg (dict, optional) – Config dict for convolution layer. Default: None, which means using conv2d.

• norm_cfg(dict) – Config dict for normalization layer. Default: dict(type='BN').

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='ReLU6').

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only. Default: False.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed. Default: False.

• pretrained(str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(x)

Forward function.

make_layer(out_channels, num_blocks, stride, expand_ratio)

Stack InvertedResidual blocks to build a layer for MobileNetV2.

## Parameters

• out channels (int) – out channels of block.