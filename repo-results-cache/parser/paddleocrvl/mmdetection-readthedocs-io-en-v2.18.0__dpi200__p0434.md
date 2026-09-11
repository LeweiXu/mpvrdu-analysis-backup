• post_norm_cfg(dict) – Config of last normalization layer. Default LN.

forward(query, *args, **kwargs)

Forward function for TransformerDecoder.

Parameters query (Tensor) – Input query with shape (num_query, bs, embed_dims).

Returns

Results with shape [1, num_query, bs, embed_dims] when return_intermediate is False, otherwise it has shape [num_layers, num_query, bs, embed_dims].

Return type Tensor

class mmdet.models.utils.DetrTransformerDecoderLayer(attn_cfg, feedforward_channels,

ffn_dropout=0.0, operation_order=None, act_cfg={'inplace': True, 'type': 'ReLU'}, norm_cfg={'type': 'LN'}, ffn_num_fcs=2, **kwargs)

Implements decoder layer in DETR transformer.

## Parameters

- attn_cfgs (list[mmcv.ConfigDict] | list[dict] | dict)) – Configs for self_attention or cross_attention, the order should be consistent with it in operation_order. If it is a dict, it would be expand to the number of attention in operation_order.

• feedforward channels (int) – The hidden dimension for FFNs.

• ffn_dropout (float) – Probability of an element to be zeroed in ffn. Default 0.0.

• operation_order (tuple[str]) – The execution order of operation in transformer. Such as ('self_attn', 'norm', 'ffn', 'norm'). DefaultNone

• act_cfg(dict) – The activation config for FFNs. Default: LN

• norm_cfg(dict) – Config dict for normalization layer. Default: LN.

• ffn_num_fcs (int) – The number of fully-connected layers in FFNs. Default2.

class mmdet.models.utils.DynamicConv(in_channels=256, feat_channels=64, out_channels=None,

 $$ \begin{array}{l}input\_{f}eat\_{s}hape=7,with\_{p}roj=True,act\_{c}fg=\{^{\prime}inplace^{\prime}:True,\\^{\prime}type^{\prime}:^{\prime}ReLU^{\prime}\},norm\_{c}fg=\{^{\prime}type^{\prime}:^{\prime}LN^{\prime}\},init\_{c}fg=None)\end{array} $$ 

Implements Dynamic Convolution.

This module generates parameters for each sample and uses bmm to implement  $ 1 \times 1 $ convolution. Code is modified from the official github repo.

## Parameters

• in channels (int) – The input feature channel. Defaults to 256.

• feat channels (int) – The inner feature channel. Defaults to 64.

• out_channels (int, optional) – The output feature channel. When not specified, it will be set to in_channels by default

• input_feat_shape(int) – The shape of input feature. Defaults to 7.

• with_proj (bool) – Project two-dimensional feature to one-dimensional feature. Default to True.

• act_cfg(dict) – The activation config for DynamicConv.

• norm_cfg(dict) – Config dict for normalization layer. Default layer normalization.