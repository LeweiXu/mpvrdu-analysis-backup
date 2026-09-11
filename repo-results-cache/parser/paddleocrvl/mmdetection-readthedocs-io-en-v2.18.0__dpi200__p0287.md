• num blocks (int) – number of blocks.

• stride (int) – stride of the first block. Default: 1

• expand_ratio (int) – Expand the number of channels of the hidden layer in InvertedResidual by this ratio. Default: 6.

train(mode=True)

Convert the model into training mode while keeping normalization layer frozen.

class mmdet.models.backbones.PyramidVisionTransformer(pretrain_img_size=224, in_channels=3,

(pretrain_img_size=224, in_channels=3,
embed_dim=64, num_stages=4,
num_layers=[3, 4, 6, 3], num_heads=[1, 2, 5, 8],
patch_sizes=[4, 2, 2, 2], strides=[4, 2, 2, 2],
paddings=[0, 0, 0, 0], sr_ratios=[8, 4, 2, 1],
out_indices=(0, 1, 2, 3), mlp_ratios=[8, 8, 4, 4],
qkv_bias=True, drop_rate=0.0,
attn_drop_rate=0.0, drop_path_rate=0.1,
use_abs_pos_embed=True,
norm_after_stage=False,
use_conv_ffn=False, act_cfg='type':
'GELU', norm_cfg='eps': 1e-06, 'type': 'LN',
pretrained=None,
convert_weights=True, init_cfg=None)

Pyramid Vision Transformer (PVT)

Implementation of Pyramid Vision Transformer: A Versatile Backbone for Dense Prediction without Convolutions.

## Parameters

• pretrain_img_size (int | tuple[int]) – The size of input image when pretrain. Defaults: 224.

• in channels (int) – Number of input channels. Default: 3.

• embed_dims(int) – Embedding dimension. Default: 64.

• num_stags (int) – The num of stages. Default: 4.

- num_layers (Sequence[int]) – The layer number of each transformer encode layer. Default: [3, 4, 6, 3].

- num_heads (Sequence[int]) – The attention heads of each transformer encode layer. Default: [1, 2, 5, 8].

• patch_sizes (Sequence[int]) – The patch_size of each patch embedding. Default: [4, 2, 2, 2].

• strides (Sequence[int]) – The stride of each patch embedding. Default: [4, 2, 2, 2].

• paddings (Sequence[int]) – The padding of each patch embedding. Default: [0, 0, 0, 0].

• sr_ratios (Sequence[int]) – The spatial reduction rate of each transformer encode layer. Default: [8, 4, 2, 1].

• out_indices (Sequence[int] / int) – Output from which stages. Default: (0, 1, 2, 3).

• mlp_ratios (Sequence[int]) – The ratio of the mlp hidden dim to the embedding dim of each transformer encode layer. Default: [8, 8, 4, 4].

• qkv_bias (bool) – Enable bias for qkv if True. Default: True.

• drop_rate (float) – Probability of an element to be zeroed. Default 0.0.