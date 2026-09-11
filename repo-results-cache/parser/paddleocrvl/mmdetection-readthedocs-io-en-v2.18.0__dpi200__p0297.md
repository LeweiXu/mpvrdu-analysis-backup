- qkv_bias (bool, optional) – If True, add a learnable bias to query, key, value. Default: True

- qk_scale (float / None, optional) – Override default qk scale of head_dim ** -0.5 if set. Default: None.

- patch_norm (bool) – If add a norm layer for patch embed and patch merging. Default: True.

• drop_rate (float) – Dropout rate. Defaults: 0.

• attn_drop_rate (float) – Attention dropout rate. Default: 0.

• drop_path_rate (float) – Stochastic depth rate. Defaults: 0.1.

• use_abs_pos_embed (bool) – If True, add absolute position embedding to the patch embedding. Defaults: False.

• act_cfg(dict) – Config dict for activation layer. Default: dict(type='LN').

• norm_cfg(dict) – Config dict for normalization layer at output of backbone. Defaults: dict(type='LN').

• with_cp (bool, optional) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed. Default: False.

• pretrained (str, optional) – model pretrained path. Default: None.

• convert_weights (bool) – The flag indicates whether the pre-trained model is from the original repo. We may need to convert some keys to make it compatible. Default: False.

• frozen_stages (int) – Stages to be frozen (stop grad and set eval mode). -1 means not freezing any parameters.

• init_cfg(dict, optional) – The Config for initialization. Defaults to None.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## init_weights()

Initialize the weights.

train(mode=True)

Convert the model into training mode while keeping layers free of ___

class mmdet.models.backbones.TridentResNet(depth, num_branch, test_branch_idx, trident_dilations,

**kwargs)

The stem layer, stage 1 and stage 2 in Trident ResNet are identical to ResNet, while in stage 3, Trident BottleBlock is utilized to replace the normal BottleBlock to yield trident output. Different branch shares the convolution weight but uses different dilations to achieve multi-scale output.

/ stage3(b0) x - stem - stage1 - stage2 - stage3(b1) - output stage3(b2) /

Parameters

• depth (int) – Depth of resnet, from  $ \{50, 101, 152\} $.