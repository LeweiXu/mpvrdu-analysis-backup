forward(x)
Forward function.

property norm1

normalization layer after the first convolution layer

Type nn.Module

property norm2

normalization layer after the second convolution layer

Type nn.Module

class mmdet.models.utils.SinePositionalEncoding(num_feats, temperature=10000, normalize=False, scale=6.283185307179586, eps=1e-06, offset=0.0, init_cfg=None)

Position encoding with sine and cosine functions.

See End-to-End Object Detection with Transformers for details.

## Parameters

- num_feats (int) – The feature dimension for each position along x-axis or y-axis. Note the final returned dimension for each position is 2 times of this value.

• temperature (int, optional) – The temperature used for scaling the position embedding. Defaults to 10000.

• normalize (bool, optional) – Whether to normalize the position embedding. Defaults to False.

- scale (float, optional) – A scale factor that scales the position embedding. The scale will be used only when normalize is True. Defaults to 2*pi.

• eps (float, optional) – A value added to the denominator for numerical stability. Defaults to 1e-6.

• offset (float) – offset add to embed when do the normalization. Defaults to 0.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward(mask)

Forward function for SinePositionalEncoding.

Parameters mask (Tensor) – ByteTensor mask. Non-zero values representing ignored positions, while zero values means valid positions for this image. Shape [bs, h, w].

## Returns

Returned position embedding with shape  $ [bs, num\_feats*2, h, w] $.

Return type pos (Tensor)

class mmdet.models.utils.Transformer(encoder=None, decoder=None, init_cfg=None)

Implements the DETR transformer.

Following the official DETR implementation, this module copy-paste from torch.nn.Transformer with modifications:

• positional encodings are passed in MultiheadAttention

• extra LN at the end of encoder is removed

• decoder returns a stack of activations from all decoding layers

See paper: End-to-End Object Detection with Transformers for details.