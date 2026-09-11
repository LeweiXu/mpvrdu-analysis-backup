• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(feats)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.necks.YOLOXPAFPN(in_channels, out_channels, num_csp_blocks=3,

use_depthwise=False, upsample_cfg='mode': 'nearest',
'scale_factor': 2, conv_cfg=None, norm_cfg='eps': 0.001,
'momentum': 0.03, 'type': 'BN', act_cfg='type': 'Swish'},
init_cfg='{a': 2.23606797749979, 'distribution': 'uniform', 'layer': 'Conv2d','mode': 'fan_in', 'nonlinearity': 'leaky_relu', 'type': 'Kaiming'})

Path Aggregation Network used in YOLOX.

## Parameters

• in channels (List[int]) – Number of input channels per scale.

• out_channels (int) – Number of output channels (used at each scale)

• num_csp_blocks (int) – Number of bottlenecks in CSPLayer. Default: 3

• use_depthwise(bool) – Whether to depthwise separable convolution in blocks. Default: False

• upsample_cfg(dict) – Config dict for interpolate layer. Default: dict(scale_factor=2, mode='nearest')

• conv_cfg (dict, optional) – Config dict for convolution layer. Default: None, which means using conv2d.

• norm_cfg(dict) – Config dict for normalization layer. Default: dict(type='BN')

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='Swish')

• init_cfg (dict or list[dict], optional) – Initialization config dict. Default: None.

## forward(inputs)

Parameters inputs (tuple[Tensor]) – input features.

Returns YOLOXPAFPN features.

Return type tuple[Tensor]