the normalization layer named “norm2”

>>> inputs = torch.rand(1, 1, 32, 32)
>>> level_outputs = self.forward(inputs)
>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))
(1, 32, 8, 8)
(1, 64, 4, 4)
(1, 128, 2, 2)
(1, 256, 1, 1)

(continued from previous page)

forward(x)
Forward function.

## property norm1

the normalization layer named “norm1”

Type nn.Module

## property norm2

Type nn.Module

train(mode=True)

Convert the model into training mode will keep the normalization layer freez.

HourglassNet backbone.

Stacked Hourglass Networks for Human Pose Estimation. More details can be found in the paper.

## Parameters

• downsample_times(int) – Downsample times in a HourglassModule.

- num_stacks (int) – Number of HourglassModule modules stacked, 1 for Hourglass-52, 2 for Hourglass-104.

• stage_channels (list[int]) – Feature channel of each sub-module in a HourglassModule.

• stage_blocks (list[int]) – Number of sub-modules stacked in a HourglassModule.

• feat channel (int) – Feature channel of conv after a HourglassModule.

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

• pretrained (str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None