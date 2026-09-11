• base channels (int) – Base channels after stem layer.

• in channels (int) – Number of input image channels. Default: 3.

• dilations (Sequence $$ int $$ ) – Dilation of each stage.

• out_indices (Sequence[int]) – Output from which stages.

• style(str)− pytorch or caffe. If set to “pytorch”, the stride-two layer is the 3x3 conv layer, otherwise the stride-two layer is the first 1x1 conv layer.

• frozen_stages (int) – Stages to be frozen (all param fixed). -1 means not freezing any parameters.

• norm_cfg(dict) – dictionary to construct and configure norm layer.

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed.

• zero_init_residual (bool) – whether to use zero init for last norm layer in resblocks to let them behave as identity.

• pretrained(str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## Example

>>> from mmdet.models import RegNet

>>> import torch

>>> self = RegNet(
    arch=dict(
        w0=88,
        wa=26.31,
        wm=2.25,
        group_w=48,
        depth=25,
        bot_mul=1.0))

>>> self.eval()

>>> inputs = torch.rand(1, 3, 32, 32)

>>> level_outputs = self.forward(inputs)

>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))
(1, 96, 8, 8)
(1, 192, 4, 4)
(1, 432, 2, 2)
(1, 1008, 1, 1)

adjust_width_group(widths, bottleneck_ratio, groups)

Adjusts the compatibility of widths and groups.

## Parameters

• widths (list[int]) – Width of each stage.

• bottleneck_ratio (float) – Bottleneck ratio.