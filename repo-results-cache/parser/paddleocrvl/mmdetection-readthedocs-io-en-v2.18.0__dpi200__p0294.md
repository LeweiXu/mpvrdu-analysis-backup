## Example

>>> from mmdet.models import ResNet
>>> import torch
>>> self = ResNet(depth=18)
>>> self.eval()
>>> inputs = torch.rand(1, 3, 32, 32)
>>> level_outputs = self.forward(inputs)
>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))
(1, 64, 8, 8)
(1, 128, 4, 4)
(1, 256, 2, 2)
(1, 512, 1, 1)

forward(x)
Forward function.

make_res_layer(**kwargs)
Pack all blocks in a stage into a ResLayer.

## make_stage_plugins(plugins, stage_idx)

Make plugins for ResNet stage_idx th stage.

Currently we support to insert context_block, empirical_attention_block, nonlocal_block into the backbone like ResNet/ResNeXt. They could be inserted after conv1/conv2/conv3 of Bottleneck.

An example of plugins format could be:

## Examples

>>> plugins=[
...     dict(cfg=dict(type='xxx', arg1='xxx'),
...     stages=(False, True, True, True),
...     position='after_conv2'),
...     dict(cfg=dict(type='yyy'),
...         stages=(True, True, True, True),
...         position='after_conv3'),
...     dict(cfg=dict(type='zzz', postfix='1'),
...         stages=(True, True, True, True),
...         position='after_conv3'),
...     dict(cfg=dict(type='zzz', postfix='2'),
...         stages=(True, True, True, True),
...         position='after_conv3')
... ]
>>> self = ResNet(depth=18)
>>> stage_plugins = self.make_stage_plugins(plugins, 0)
>>> assert len(stage_plugins) == 3

Suppose stage_idx=0, the structure of blocks in the stage would be:

conv1-> conv2->conv3->yyy->zzz1->zzz2

Suppose ‘stage_idx=1’, the structure of blocks in the stage would be: