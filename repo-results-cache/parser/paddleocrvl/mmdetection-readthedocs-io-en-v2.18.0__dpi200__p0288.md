• attn_drop_rate (float) – The drop out rate for attention layer. Default 0.0.

• drop_path_rate (float) – stochastic depth rate. Default 0.1.

• use_abs_pos_embed (bool) – If True, add absolute position embedding to the patch embedding. Defaults: True.

• use conv ffn (bool) – If True, use Convolutional FFN to replace FFN. Default: False.

• act_cfg(dict) – The activation config for FFNs. Default: dict(type='GELU').

• norm_cfg(dict) – Config dict for normalization layer. Default: dict(type='LN').

• pretrained(str, optional) – model pretrained path. Default: None.

• convert_weights (bool) – The flag indicates whether the pre-trained model is from the original repo. We may need to convert some keys to make it compatible. Default: True.

• init_cfg (dict or list[dict], optional) – Initialization config dict. Default: None.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## init_weights()

Initialize the weights.

class mmdet.models.backbones.PyramidVisionTransformerV2(**kwargs)

Implementation of PVTv2: Improved Baselines with Pyramid Vision Transformer.

class mmdet.models.backbones.RegNet(arch, in_channels=3, stem_channels=32, base_channels=32)

(arch, in_channels=3, stem_channels=32, base_channels=32, strides=(2, 2, 2, 2), dilations=(1, 1, 1, 1), out_indices=(0, 1, 2, 3), style='pytorch', deep_stem=False, avg_down=False, frozen_stages=1, conv_cfg=None, norm_cfg={'requires_grad': True, 'type': 'BN'}, norm_eval=True, dcn=None, stage_with_dcn=(False, False, False, False), plugins=None, with_cp=False, zero_init_residual=True, pretrained=None, init_cfg=None)

RegNet backbone.

More details can be found in paper.

## Parameters

• arch (dict) – The parameter of RegNets.

- w0 (int): initial width

– wa (float): slope of width

– wm (float): quantization parameter to quantize the width

– depth (int): depth of the backbone

- group_w (int): width of group

– bot_mul (float): bottleneck ratio, i.e. expansion of bottleneck.

• strides (Sequence[int]) – Strides of the first block of each stage.