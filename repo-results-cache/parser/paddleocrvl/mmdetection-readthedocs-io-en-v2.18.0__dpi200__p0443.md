• mode(str) – Algorithm used for interpolation. The options are the same as those in F.interpolate(). Default: 'bilinear'.

• align corners (bool) – The same as the argument in F.interpolate().

Returns The interpolated source Tensor.

## Return type Tensor

mmdet.models.utils.make_divisible(value, divisor, min_value=None, min_ratio=0.9)

Make divisible function.

This function rounds the channel number to the nearest value that can be divisible by the divisor. It is taken from the original tf repo. It ensures that all layers have a channel number that is divisible by divisor. It can be seen here: https://github.com/tensorflow/models/blob/master/research/slim/nets/mobilenet/mobilenet.py #noqa

## Parameters

• value (int) – The original channel number.

• divisor (int) – The divisor to fully divide the channel number.

• min_value (int) – The minimum value of the output channel. Default: None, means that the minimum value equal to the divisor.

• min_ratio (float) – The minimum ratio of the rounded channel number to the original channel number. Default: 0.9.

Returns The modified output channel number.

## Return type int

mmdet.models.utils.nchw_to_nlc(x)

Flatten [N, C, H, W] shape tensor to [N, L, C] shape tensor.

Parameters x (Tensor) – The input tensor of shape [N, C, H, W] before conversion.

Returns The output tensor of shape [N, L, C] after conversion.

Return type Tensor

mmdet.models.utils.nlc_to_nchw(x, hw_shape)

Convert [N, L, C] shape tensor to [N, C, H, W] shape tensor.

## Parameters

• x (Tensor) – The input tensor of shape [N, L, C] before conversion.

• hw_shape (Sequence[int]) – The height and width of output feature map.

Returns The output tensor of shape [N, C, H, W] after conversion.

Return type Tensor