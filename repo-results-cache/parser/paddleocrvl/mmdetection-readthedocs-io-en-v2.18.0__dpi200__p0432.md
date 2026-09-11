>>> import torch
>>> @weighted_loss
>>> def l1_loss(pred, target):
>>>     return (pred - target).abs()

>>> pred = torch.Tensor([0, 2, 3])
>>> target = torch.Tensor([1, 1, 1])
>>> weight = torch.Tensor([1, 0, 1])

>>> l1_loss(pred, target)

tensor(1.3333)

>>> l1_loss(pred, target, weight)

tensor(1.)

>>> l1_loss(pred, target, reduction='none')

tensor([1., 1., 2.])

>>> l1_loss(pred, target, weight, avg_factor=2)

tensor(1.5000)

### 39.7 utils

class mmdet.models.utils.AdaptiveAvgPool2d(output_size: Union[int, None, Tuple[Optional[int],...]])

Handle empty batch dimension to AdaptiveAvgPool2d.

## forward(x)

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.CSPLayer(in_channels, out_channels, expand_ratio=0.5, num_blocks=1,

Cross Stage Partial Layer.

## Parameters

• in channels (int) – The input channels of the CSP layer.

• out channels (int) – The output channels of the CSP layer.

• expand_ratio (float) – Ratio to adjust the number of channels of the hidden layer. Default: 0.5

• num blocks (int) – Number of blocks. Default: 1

• add_identity(bool) – Whether to add identity in blocks. Default: True

• use_depthwise(bool) – Whether to depthwise separable convolution in blocks. Default: False