## Example

>>> self = SSDVGG(input_size=300, depth=11)
>>> self.eval()
>>> inputs = torch.rand(1, 3, 300, 300)
>>> level_outputs = self.forward(inputs)
>>> for level_out in level_outputs:
...     print(tuple(level_out.shape))
(1, 1024, 19, 19)
(1, 512, 10, 10)
(1, 256, 5, 5)
(1, 256, 3, 3)
(1, 256, 1, 1)

forward(x)

Forward function.

init_weights(pretrained=None)

Initialize the weights.

(pretrain_img_size=224, in_channels=3, embed_dims=96, patch_size=4, window_size=7, mlp_ratio=4, depths=(2, 2, 6, 2), num_heads=(3, 6, 12, 24), strides=(4, 2, 2, 2), out_indices=(0, 1, 2, 3), qkv_bias=True, qk_scale=None, patch_norm=True, drop_rate=0.0, attn_drop_rate=0.0, drop_path_rate=0.1, use_abs_pos_embed=False, act_cfg='type': 'GELU', norm_cfg='type': 'LN', with_cp=False, pretrained=None, convert_weights=False, frozen_stages=-1, init_cfg=None)

Swin Transformer A PyTorch implement of : Swin Transformer: Hierarchical Vision Transformer using Shifted Windows -

https://arxiv.org/abs/2103.14030

Inspiration from https://github.com/microsoft/Swin-Transformer

## Parameters

• pretrain_img_size (int | tuple[int]) – The size of input image when pretrain. Defaults: 224.

• in channels (int) – The num of input channels. Defaults: 3.

• embed_dims (int) – The feature dimension. Default: 96.

• patch_size (int / tuple[int]) – Patch size. Default: 4.

• window_size (int) – Window size. Default: 7.

• mlp_ratio(int) – Ratio of mlp hidden dim to embedding dim. Default: 4.

• depths (tuple[int]) – Depths of each Swin Transformer stage. Default:  $ (2, 2, 6, 2) $.

- num_heads (tuple[int]) – Parallel attention heads of each Swin Transformer stage. Default:  $ (3, 6, 12, 24) $.

• strides (tuple[int]) – The patch merging or patch embedding stride of each Swin Transformer stage. (In swin, we set kernel size equal to stride.) Default: (4, 2, 2, 2).

• out_indices (tuple[int]) – Output from which stages. Default:  $ (0, 1, 2, 3) $.