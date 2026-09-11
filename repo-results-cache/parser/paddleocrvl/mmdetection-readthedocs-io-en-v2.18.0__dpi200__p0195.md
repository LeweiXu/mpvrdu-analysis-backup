• base_size (int / float) – Basic size of an anchor.

• scales (torch.Tensor) – Scales of the anchor.

• ratios (torch.Tensor) – The ratio between the height. and width of anchors in a single level.

• center (tuple[float], optional) – The center of the base anchor related to a single feature grid. Defaults to None.

Returns Anchors in a single-level feature map.

Return type torch.Tensor

###### class mmdet.core.anchor.MlvlPointGenerator(strides, offset=0.5)

Standard points generator for multi-level (MlvI) feature maps in 2D points-based detectors.

## Parameters

• strides (list[int] | list[tuple[int, int]]) – Strides of anchors in multiple feature levels in order (w, h).

• offset (float) – The offset of points, the value is normalized with corresponding stride. Defaults to 0.5.

grid_priors(featmap_sizes, dtype=torch.float32, device='cuda', with_stride=False)

Generate grid points of multiple feature levels.

## Parameters

- featmap_sizes (list[tuple]) – List of feature map sizes in multiple feature levels, each size arrange as (h, w).

• dtype (dtype) – Dtype of priors. Default: torch.float32.

• device (str) – The device where the anchors will be put on.

• with_stride (bool) – Whether to concatenate the stride to the last dimension of points.

Returns Points of multiple feature levels. The sizes of each tensor should be  $ (N, 2) $ when with stride is False, where  $ N = width * height $, width and height are the sizes of the corresponding feature level, and the last dimension 2 represent  $ (coord\_x, coord\_y) $, otherwise the shape should be  $ (N, 4) $, and the last dimension 4 represent  $ (coord\_x, coord\_y, stride\_w, stride\_h) $.

Return type list[torch.Tensor]

## property num_base_priors

The number of priors (points) at a point on the feature grid

Type list[int]

## property num_levels

number of feature levels that the generator will be applied

Type int

single_level_grid_priors(featmap_size, level_idx, dtype=torch.float32, device='cuda', with_stride=False)

Generate grid Points of a single level.

Note: This function is usually called by method self.grid_priors.

## Parameters