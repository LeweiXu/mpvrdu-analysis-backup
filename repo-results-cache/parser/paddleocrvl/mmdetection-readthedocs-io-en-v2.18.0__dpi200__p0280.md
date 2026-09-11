### 39.2 backbones

class mmdet.models.backbones.CSPDarknet(arch='P5', deepen_factor=1.0, widen_factor=1.0)

out_indices=(2, 3, 4), frozen_stages=-1, use_depthwise=False, arch_ovewrite=None, spp_kernal_sizes=(5, 9, 13), conv_cfg=None, norm_cfg='eps': 0.001,'momentum': 0.03, 'type': 'BN', act_cfg='type': 'Swish', norm_eval=False, init_cfg='a': 2.23606797749979, 'distribution': 'uniform', 'layer': 'Conv2d','mode': 'fan_in', 'nonlinearity': 'leaky_relu', 'type': 'Kaiming'

CSP-Darknet backbone used in YOLOv5 and YOLOX.

## Parameters

• arch (str) – Architecture of CSP-Darknet, from {P5, P6}. Default: P5.

• deepen_factor (float) – Depth multiplier, multiply number of channels in each layer by this amount. Default: 1.0.

• widen_factor (float) – Width multiplier, multiply number of blocks in CSP layer by this amount. Default: 1.0.

• out_indices (Sequence[int]) – Output from which stages. Default:  $ (2, 3, 4) $.

• frozen_stages (int) – Stages to be frozen (stop grad and set eval mode). -1 means not freezing any parameters. Default: -1.

• use_depthwise(bool) – Whether to use depthwise separable convolution. Default: False.

• arch_overwrite (list) – Overwrite default arch settings. Default: None.

- spp_kernal_sizes – (tuple[int]): Sequential of kernel sizes of SPP layers. Default: (5, 9, 13).

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Dictionary to construct and config norm layer. Default: dict(type='BN', requires_grad=True).

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='LeakyReLU', negative_slope=0.1).

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only.

• init_cfg (dict or list[dict], optional) – Initialization config dict. Default: None.

## Example

>>> from mmdet.models import CSPDarknet
>>> import torch
>>> self = CSPDarknet(depth=53)
>>> self.eval()
>>> inputs = torch.rand(1, 3, 416, 416)
>>> level_outputs = self.forward(inputs)
>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))

(continues on next page)