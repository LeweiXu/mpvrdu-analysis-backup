• groups (int) – number of groups in each stage

Returns The adjusted widths and groups of each stage.

Return type tuple(list)

forward(x)

Forward function.

generate_regnet(initial_width, width_slope, width_parameter, depth, divisor=8)

Generates per block width from RegNet parameters.

## Parameters

• initial_width ( $ [int] $) – Initial width of the backbone

• width_slope ( $ [float] $) – Slope of the quantized linear function

• width parameter ([int]) – Parameter used to quantize the width.

• depth ( $ [int] $) – Depth of the backbone.

• divisor (int, optional) – The divisor of channels. Defaults to 8.

Returns return a list of widths of each stage and the number of stages

Return type list, int

## get_stages_from_blocks(widths)

Gets widths/stage blocks of network at each stage.

Parameters widths (list[int]) – Width in each stage.

Returns width and depth of each stage

Return type tuple(list)

static quantize_float(number, divisor)

Converts a float to closest non-zero int divisible by divisor.

## Parameters

• number (int) – Original number to be quantized.

• divisor (int) – Divisor used to quantize the number.

Returns quantized number that is divisible by divisor.

Return type int

class mmdet.models.backbones.Res2Net(scales=4, base_width=26, style='pytorch', deep_stem=True, avg_down=True, pretrained=None, init_cfg=None, **kwargs=True)

## Res2Net backbone

## Parameters

• scales (int) – Scales used in Res2Net. Default: 4

• base_width (int) – Basic width of each scale. Default: 26

• depth (int) – Depth of res2net, from  $ \{50, 101, 152\} $.

• in channels (int) – Number of input image channels. Default: 3.

• num_stages (int) – Res2net stages. Default: 4.

• strides (Sequence[int]) – Strides of the first block of each stage.

• dilations (Sequence $$ int $$ ) – Dilation of each stage.