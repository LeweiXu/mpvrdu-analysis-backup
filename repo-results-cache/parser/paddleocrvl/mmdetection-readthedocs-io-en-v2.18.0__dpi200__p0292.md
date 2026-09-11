• groups (int) – Number of groups of Bottleneck. Default: 1

• base_width(int) – Base width of Bottleneck. Default: 4

• radix (int) – Radix of SplitAttentionConv2d. Default: 2

• reduction_factor (int) – Reduction factor of inter_channels in SplitAttentionConv2d. Default: 4.

• avg_down_stride (bool) – Whether to use average pool for stride in Bottleneck. Default: True.

• kwargs (dict) – Keyword arguments for ResNet.

## make_res_layer(**kwargs)

Pack all blocks in a stage into a ResLayer.

class mmdet.models.backbones.ResNeXt(groups=1, base_width=4, **kwargs)

ResNeXt backbone.

## Parameters

• depth (int) – Depth of resnet, from  $ \{18, 34, 50, 101, 152\} $.

• in channels (int) – Number of input image channels. Default: 3.

• num_stages (int) – Resnet stages. Default: 4.

• groups (int) – Group of resnext.

• base_width(int) – Base width of resnext.

• strides (Sequence[int]) – Strides of the first block of each stage.

• dilations (Sequence $$ int $$ ) – Dilation of each stage.

• out_indices (Sequence[int]) – Output from which stages.

• style(str)− pytorch or caffe. If set to “pytorch”, the stride-two layer is the 3x3 conv layer, otherwise the stride-two layer is the first 1x1 conv layer.

• frozen_stages (int) – Stages to be frozen (all param fixed). -1 means not freezing any parameters.

• norm_cfg(dict) – dictionary to construct and configure norm layer.

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed.

• zero_init_residual (bool) – whether to use zero init for last norm layer in resblocks to let them behave as identity.

## make_res_layer(**kwargs)

Pack all blocks in a stage into a ResLayer