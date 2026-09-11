• featmap_size (tuple[int]) – Size of the feature maps, arrange as (h, w).

• level_idx(int) – The index of corresponding feature map level.

• dtype (dtype) – Dtype of priors. Default: torch.float32.

• device (str, optional) – The device the tensor will be put on. Defaults to ‘cuda’.

• with_stride (bool) – Concatenate the stride to the last dimension of points.

Returns Points of single feature levels. The shape of tensor should be  $ (N, 2) $ when with stride is False, where  $ N = \text{width} * \text{height} $, width and height are the sizes of the corresponding feature level, and the last dimension 2 represent  $ (coord\_x, coord\_y) $, otherwise the shape should be  $ (N, 4) $, and the last dimension 4 represent  $ (coord\_x, coord\_y, stride\_w, stride\_h) $.

Return type Tensor

## single_level_valid_flags(featmap_size, valid_size, device='cuda')

Generate the valid flags of points of a single feature map.

## Parameters

• featmap_size (tuple[int]) – The size of feature maps, arrange as as (h, w).

- valid_size (tuple[int]) – The valid size of the feature maps. The size arrange as as (h, w).

• device (str, optional) – The device where the flags will be put on. Defaults to ‘cuda’.

Returns The valid flags of each point in a single level feature map.

### Return type torch.Tensor

sparse_priors(prior_idxs, featmap_size, level_idx, dtype=torch.float32, device='cuda')

Generate sparse points according to the prior_idxs.

## Parameters

• prior_idxs (Tensor) – The index of corresponding anchors in the feature map.

• featmap_size (tuple[int]) – feature map size arrange as (w, h).

• level_idx(int) – The level index of corresponding feature map.

• (obj (device) – torch.dtype): Date type of points. Defaults to torch.float32.

• (obj – torch.device): The device where the points is located.

Returns Anchor with shape  $ (N, 2) $, N should be equal to the length of prior_idxs. And last dimension 2 represent  $ (coord\_x, coord\_y) $.

## Return type Tensor

## valid_flags(featmap_sizes, pad_shape, device='cuda')

Generate valid flags of points of multiple feature levels.

## Parameters

- featmap_sizes (list(tuple)) – List of feature map sizes in multiple feature levels, each size arrange as (h, w).

• pad_shape(tuple(int)) – The padded shape of the image, arrange as (h, w).

• device (str) – The device where the anchors will be put on.

Returns Valid flags of points of multiple levels.

Return type list(torch.Tensor)