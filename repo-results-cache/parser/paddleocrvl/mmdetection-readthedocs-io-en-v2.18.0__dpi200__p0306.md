class mmdet.models.necks.SSDNeck(in_channels, out_channels, level_strides, level_paddings,

 $ l2\_norm\_scale=20.0 $, last\_kernel\_size=3, use\_depthwise=False,

conv_cfg=None, norm_cfg=None, act_cfg=\{type': 'ReLU'\},

init_cfg=[\{type': 'Xavier', 'distribution': 'uniform', 'layer': 'Conv2d'\},

{'type': 'Constant', 'val': 1, 'layer': 'BatchNorm2d'}

Extra layers of SSD backbone to generate multi-scale feature maps.

## Parameters

• in_channels (Sequence[int]) – Number of input channels per scale.

• out channels (Sequence[int]) – Number of output channels per scale.

• level_strides (Sequence[int]) – Stride of 3x3 conv per level.

• level_paddings (Sequence[int]) – Padding size of 3x3 conv per level.

• l2_norm_scale (float/None) – L2 normalization layer init scale. If None, not use L2 normalization on the first input feature.

• last_kernel_size (int) – Kernel size of the last conv layer. Default: 3.

• use_depthwise(bool) – Whether to use DepthwiseSeparableConv. Default: False.

• conv_cfg(dict) – Config dict for convolution layer. Default: None.

• norm_cfg(dict) – Dictionary to construct and config norm layer. Default: None.

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='ReLU').

• init_cfg(dict or list[dict], optional) – Initialization config dict.

forward(inputs)

Forward function.

class mmdet.models.necks.YOLOV3Neck(num_scales, in_channels, out_channels, conv_cfg=None,

norm_cfg={'requires_grad': True, 'type': 'BN'},

act_cfg={'negative_slope': 0.1, 'type': 'LeakyReLU'}, init_cfg=None)

The neck of YOLOV3.

It can be treated as a simplified version of FPN. It will take the result from Darknet backbone and do some upsampling and concatenation. It will finally output the detection result.

## Note:

The input feats should be from top to bottom. i.e., from high-lv1 to low-lv1.

But YOLOv3Neck will process them in reversed order. i.e., from bottom (high-lv) to top (low-lv)

## Parameters

• num_scales (int) – The number of scales / stages.

• in channels (List[int]) – The number of input channels per scale.

• out_channels (List[int]) – The number of output channels per scale.

• conv_cfg (dict, optional) – Config dict for convolution layer. Default: None.

• norm_cfg (dict, optional) – Dictionary to construct and config norm layer. Default: dict(type='BN', requires_grad=True)

• act_cfg (dict, optional) – Config dict for activation layer. Default: dict(type='LeakyReLU', negative_slope=0.1).