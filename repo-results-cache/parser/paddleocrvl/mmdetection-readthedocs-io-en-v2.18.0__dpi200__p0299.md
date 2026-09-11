init_weights()
Initialize the weights.

class mmdet.models.necks.ChannelMapper(in_channels, out_channels, kernel_size=3, conv_cfg=None, norm_cfg=None, act_cfg='type': 'ReLU'), num_outs=None, init_cfg='distribution': 'uniform', 'layer': 'Conv2d', 'type': 'Xavier')

Channel Mapper to reduce/increase channels of backbone features.

This is used to reduce/increase channels of backbone features.

## Parameters

• in channels (List[int]) – Number of input channels per scale.

• out channels (int) – Number of output channels (used at each scale).

- kernel_size (int, optional) – kernel_size for reducing channels (used at each scale). Default: 3.

• conv_cfg (dict, optional) – Config dict for convolution layer. Default: None.

• norm_cfg(dict, optional) – Config dict for normalization layer. Default: None.

• act_cfg (dict, optional) – Config dict for activation layer in ConvModule. Default: dict(type='ReLU').

- num_outs (int, optional) – Number of output feature maps. There would be extra_convs when num_outs larger than the length of in_channels.

• init_cfg (dict or list[dict], optional) – Initialization config dict.

## Example

>>> import torch

>>> in_channels = [2, 3, 5, 7]

>>> scales = [340, 170, 84, 43]

>>> inputs = [torch.rand(1, c, s, s)
... for c, s in zip(in_channels, scales)]

>>> self = ChannelMapper(in_channels, 11, 3).eval()

>>> outputs = self.forward(inputs)

>>> for i in range(len(outputs)):
...     print(f'outputs[{i}]'.shape = {outputs[i].shape}')

outputs[0].shape = torch.Size([1, 11, 340, 340])

outputs[1].shape = torch.Size([1, 11, 170, 170])

outputs[2].shape = torch.Size([1, 11, 84, 84])

outputs[3].shape = torch.Size([1, 11, 43, 43])
forward(inputs)
Forward function.

class mmdet.models.necks.DilatedEncoder(in_channels, out_channels, block_mid_channels,

Dilated Encoder for YOLOF <https://arxiv.org/abs/2103.09460>.

This module contains two types of components:

• the original FPN lateral convolution layer and fpn convolution layer, which are  $ 1 \times 1 $ conv +  $ 3 \times 3 $ conv