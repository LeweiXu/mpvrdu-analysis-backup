conv1-> conv2->xxx->conv3->yyy->zzz1->zzz2

If stages is missing, the plugin would be applied to all stages.

## Parameters

• plugins (list[dict]) – List of plugins cfg to build. The postfix is required if multiple same type plugins are inserted.

• stage_idx(int) – Index of stage to build

Returns Plugins for current stage

Return type list[dict]

property norm1

the normalization layer named “norm1”

Type nn.Module

train(mode=True)

Convert the model into training mode while keeping normalization layer freezed.

##### class mmdet.models.backbones.ResNetV1d(**kwargs)

ResNetV1d variant described in Bag of Tricks.

Compared with default ResNet(ResNetV1b), ResNetV1d replaces the 7x7 conv in the input stem with three 3x3 convs. And in the downsampling block, a 2x2 avg_pool with stride 2 is added before conv, whose stride is changed to 1.

class mmdet.models.backbones.SSDVGG(depth, with_last_pool=False, ceil_mode=True, out_indices=(3, 4), out_feature_indices=(22, 34), pretrained=None, init_cfg=None, input_size=None, l2_norm_scale=None)

VGG Backbone network for single-shot-detection.

## Parameters

• depth (int) – Depth of vgg, from  $ \{11, 13, 16, 19\} $.

• with_last_pool (bool) – Whether to add a pooling layer at the last of the model

• ceil_mode (bool) – When True, will use ceil instead of floor to compute the output shape.

• out_indices (Sequence[int]) – Output from which stages.

• out_feature_indices (Sequence[int]) – Output from which feature map.

• pretrained (str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

• input_size (int, optional) – Deprecated argument. Width and height of input, from  $ \{300, 512\} $.

• l2_norm_scale (float, optional) – Deprecated argument. L2 normalization layer init scale.