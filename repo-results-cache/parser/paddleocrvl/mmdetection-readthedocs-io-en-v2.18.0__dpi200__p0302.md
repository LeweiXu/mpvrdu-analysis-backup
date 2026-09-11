• no_norm_on_lateral (bool) – Whether to apply norm on lateral. Default: False.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Config dict for normalization layer. Default: None.

• act_cfg(str) – Config dict for activation layer in ConvModule. Default: None.

• upsample_cfg(dict) – Config dict for interpolate layer. Default: dict(mode='nearest')

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## Example

>>> import torch

>>> in_channels = [2, 3, 5, 7]

>>> scales = [340, 170, 84, 43]

>>> inputs = [torch.rand(1, c, s, s)
... for c, s in zip(in_channels, scales)]

>>> self = FPN(in_channels, 11, len(in_channels)).eval()

>>> outputs = self.forward(inputs)

>>> for i in range(len(outputs)):
...     print(f'outputs[{i}]'.shape = {outputs[i].shape}')

outputs[0].shape = torch.Size([1, 11, 340, 340])

outputs[1].shape = torch.Size([1, 11, 170, 170])

outputs[2].shape = torch.Size([1, 11, 84, 84])

outputs[3].shape = torch.Size([1, 11, 43, 43])

forward(inputs)
Forward function.

class mmdet.models.necks.FPN_CARAFE(in_channels, out_channels, num_outs, start_level=0, end_level=1,

norm_cfg=None, act_cfg=None, order=('conv', 'norm', 'act'),
upsample_cfg={'encoder_dilation': 1, 'encoder_kernel': 3, 'type': 'carafe', 'up_group': 1, 'up_kernel': 5}, init_cfg=None)

FPN_CARAFE is a more flexible implementation of FPN. It allows more choice for upsample methods during the top-down pathway.

It can reproduce the performance of ICCV 2019 paper CARAFE: Content-Aware ReAssembly of FEatures Please refer to https://arxiv.org/abs/1905.02188 for more details.

## Parameters

• in channels (list[int]) – Number of channels for each input feature map.

• out_channels (int) – Output channels of feature pyramids.

• num_outs (int) – Number of output stages.

• start_level (int) – Start level of feature pyramids. (Default: 0)

• end_level (int) – End level of feature pyramids. (Default: -1 indicates the last level).

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

• activate(str) – Type of activation function in ConvModule (Default: None indicates w/o activation).

• order (dict) – Order of components in ConvModule.

• upsample (str) – Type of upsample layer.