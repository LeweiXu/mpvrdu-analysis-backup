## Parameters

• encoder (mmcv.ConfigDict | Dict) – Config of TransformerEncoder. Defaults to None.

• decoder ((mmcv.ConfigDict | Dict)) – Config of TransformerDecoder. Defaults to None

• (obj (init_cfg) - mmcv.ConfigDict): The Config for initialization. Defaults to None.

## forward(x, mask, query_embed, pos_embed)

Forward function for Transformer.

## Parameters

• x (Tensor) – Input query with shape [bs, c, h, w] where c = embed_dims.

• mask (Tensor) – The key_padding_mask used for encoder and decoder, with shape [bs, h, w].

• query_embed (Tensor) – The query embedding for decoder, with shape [num_query, c].

• pos_embed (Tensor) – The positional encoding for encoder and decoder, with the same shape as x.

## Returns

results of decoder containing the following tensor.

• out_dec: Output from decoder. If return_intermediate_dec is True output has shape [num_dec_layers, bs, num_query, embed_dims], else has shape [1, bs, num_query, embed_dims].

• memory: Output results from encoder, with shape [bs, embed_dims, h, w].

Return type tuple[Tensor]

init_weights()

Initialize the weights.

mmdet.models.utils.adaptive_avg_pool2d(input, output_size)

Handle empty batch dimension to adaptive_avg_pool2d.

## Parameters

• input (tensor) – 4D tensor.

• output_size (int, tuple[int, int]) – the target output size.

mmdet.models.utils.build_linear_layer(cfg, *args, **kwargs)

Build linear layer. :param cfg: The linear layer config, which should contain:

• type (str): Layer type.

• layer args: Args needed to instantiate an linear layer.

## Parameters

• args (argument list) – Arguments passed to the __init__ method of the corresponding linear layer.

• kwargs (keyword arguments) – Keyword arguments passed to the __init__ method of the corresponding linear layer.

Returns Created linear layer.

Return type nn.Module

##### mmdet.models.utils.build_transformer(cfg, default_args=None)

Builder for Transformer.