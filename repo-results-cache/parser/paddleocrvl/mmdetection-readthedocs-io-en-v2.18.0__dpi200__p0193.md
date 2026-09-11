• device (str, optional) – The device the tensor will be put on. Defaults to ‘cuda’.

Returns Anchors in the overall feature maps.

Return type torch.Tensor

single_level_valid_flags(featmap_size, valid_size, num_base_anchors, device='cuda')

Generate the valid flags of anchor in a single feature map.

## Parameters

• featmap_size (tuple[int]) – The size of feature maps, arrange as (h, w).

• valid_size(tuple[int]) – The valid size of the feature maps.

• num_base_anchors (int) – The number of base anchors.

• device (str, optional) – Device where the flags will be put on. Defaults to ‘cuda’.

Returns The valid flags of each anchor in a single level feature map.

Return type torch.Tensor

sparse_priors(prior_idxs, featmap_size, level_idx, dtype=torch.float32, device='cuda')

Generate sparse anchors according to the prior_idxs.

## Parameters

• prior_idxs (Tensor) – The index of corresponding anchors in the feature map.

• featmap_size (tuple[int]) – feature map size arrange as (h, w).

• level_idx(int) – The level index of corresponding feature map.

• (obj (device) – torch.dtype): Date type of points.Defaults to torch.float32.

• (obj – torch.device): The device where the points is located.

## Returns

Anchor with shape  $ (N, 4) $, N should be equal to the length of prior_idxs.

Return type Tensor

valid_flags(featmap_sizes, pad_shape, device='cuda')

Generate valid flags of anchors in multiple feature levels.

## Parameters

• featmap sizes (list(tuple)) – List of feature map sizes in multiple feature levels.

• pad_shape (tuple) – The padded shape of the image.

• device (str) – Device where the anchors will be put on.

Returns Valid flags of anchors in multiple levels.

Return type list(torch.Tensor)

class mmdet.core.anchor.LegacyAnchorGenerator(strides, ratios, scales=None, base_sizes=None, scale_major=True, octave_base_scale=None, scales_per_octave=None, centers=None, center_offset=0.0)

Legacy anchor generator used in MMDetection V1.x.

Note: Difference to the V2.0 anchor generator: