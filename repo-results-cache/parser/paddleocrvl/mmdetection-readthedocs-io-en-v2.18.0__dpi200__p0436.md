class mmdet.models.utils.LearnedPositionalEncoding(num_feats, row_num_embed=50, col_num_embed=50, init_cfg='layer': 'Embedding', 'type': 'Uniform'))

Position embedding with learnable embedding weights.

## Parameters

- num_feats (int) – The feature dimension for each position along x-axis or y-axis. The final returned dimension for each position is 2 times of this value.

• row_num_embed (int, optional) – The dictionary size of row embeddings. Default 50.

• col_num_embed (int, optional) – The dictionary size of col embeddings. Default 50.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(mask)

Forward function for LearnedPositionalEncoding.

Parameters mask (Tensor) – ByteTensor mask. Non-zero values representing ignored positions, while zero values means valid positions for this image. Shape [bs, h, w].

## Returns

Returned position embedding with shape  $ [bs, num\_feats*2, h, w] $.

Return type pos (Tensor)

class mmdet.models.utils.NormedConv2d(*args, tempearture=20, power=1.0, eps=1e-06)

Normalized Conv2d Layer.

## Parameters

• temperature (float, optional) – Temperature term. Default to 20.

• power (int, optional) – Power term. Default to 1.0.

• eps(float, optional) – The minimal value of divisor to keep numerical stability. Default to 1e-6.

• norm_over_kernel (bool, optional) – Normalize over kernel. Default to False.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.utils.NormedLinear(*args, tempearture=20, power=1.0, eps=1e-06, **kwargs) Normalized Linear Layer.

## Parameters

• temperature (float, optional) – Temperature term. Default to 20.

• power (int, optional) – Power term. Default to 1.0.

• eps(float, optional)—The minimal value of divisor to keep numerical stability. Default to 1e-6.