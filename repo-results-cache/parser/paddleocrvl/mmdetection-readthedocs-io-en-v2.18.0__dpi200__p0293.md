class mmdet.models.backbones.ResNet(depth, in_channels=3, stem_channels=None, base_channels=64)

num_stages=4, strides=(1, 2, 2, 2), dilations=(1, 1, 1, 1),

out_indices=(0, 1, 2, 3), style='pytorch', deep_stem=False,

avg_down=False, frozen_stages=-1, conv_cfg=None,

norm_cfg='requires_grad': True, 'type': 'BN', norm_eval=True,

dcn=None, stage_with_dcn=(False, False, False, False),

plugins=None, with_cp=False, zero_init_residual=True,

pretrained=None, init_cfg=None)

ResNet backbone.

## Parameters

• depth (int) – Depth of resnet, from  $ \{18, 34, 50, 101, 152\} $.

• stem_channels (int / None) – Number of stem channels. If not specified, it will be the same as base_channels. Default: None.

• base channels (int) – Number of base channels of res layer. Default: 64.

• in channels (int) – Number of input image channels. Default: 3.

• num_stages (int) – Resnet stages. Default: 4.

• strides (Sequence[int]) – Strides of the first block of each stage.

• dilations (Sequence[int]) – Dilation of each stage.

• out_indices (Sequence[int]) – Output from which stages.

• style(str) – pytorch or caffe. If set to “pytorch”, the stride-two layer is the 3x3 conv layer, otherwise the stride-two layer is the first 1x1 conv layer.

• deep_stem (bool) – Replace 7x7 conv in input stem with 3 3x3 conv

• avg_down (bool) – Use AvgPool instead of stride conv when downsampling in the bottleneck.

• frozen_stages (int) – Stages to be frozen (stop grad and set eval mode). -1 means not freezing any parameters.

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only.

• plugins (list[dict]) – List of plugins for stages, each dict contains:

–cfg (dict, required): Cfg dict to build plugin.

– position (str, required): Position inside block to insert plugin, options are ‘after_conv1’, ‘after_conv2’, ‘after_conv3’.

– stages (tuple[bool], optional): Stages to apply plugin, length should be same as 'num_stages'.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed.

• zero_init_residual (bool) – Whether to use zero init for last norm layer in resblocks to let them behave as identity.

• pretrained (str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None