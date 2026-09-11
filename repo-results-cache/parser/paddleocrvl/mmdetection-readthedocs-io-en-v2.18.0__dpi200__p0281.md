class mmdet.models.backbones.Darknet(depth=53, out_indices=(3, 4, 5), frozen_stages=-1, conv_cfg=None, norm_cfg='requires_grad': True, 'type': 'BN'), act_cfg='negative_slope': 0.1, 'type': 'LeakyReLU'), norm_eval=True, pretrained=None, init_cfg=None)

(1, 256, 52, 52)
(1, 512, 26, 26)
(1, 1024, 13, 13)

(continued from previous page)

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## train(mode=True)

Sets the module in training mode.

This has any effect only on certain modules. See documentations of particular modules for details of their behaviors in training/evaluation mode, if they are affected, e.g. Dropout, BatchNorm, etc.

Parameters mode (bool) – whether to set training mode (True) or evaluation mode (False). Default: True.

Returns self

Return type Module

Darknet backbone.

## Parameters

• depth (int) – Depth of Darknet. Currently only support 53.

• out_indices (Sequence[int]) – Output from which stages.

• frozen_stages (int) – Stages to be frozen (stop grad and set eval mode). -1 means not freezing any parameters. Default: -1.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Dictionary to construct and config norm layer. Default: dict(type='BN', requires_grad=True)

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='LeakyReLU', negative_slope=0.1).

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only.

• pretrained (str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None