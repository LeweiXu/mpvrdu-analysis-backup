## Parameters

• featmap sizes (list [tuple]) – List of feature map sizes in multiple feature levels.

• dtype (torch.dtype) – Dtype of priors. Default: torch.float32.

• device (str) – The device where the anchors will be put on.

Returns Anchors in multiple feature levels. The sizes of each tensor should be [N, 4], where N = width * height * num_base_anchors, width and height are the sizes of the corresponding feature level, num_base_anchors is the number of anchors for that level.

Return type list[torch.Tensor]

property num_base_anchors
    total number of base anchors in a feature grid
    Type list[int]

property num_base_priors
    The number of priors (anchors) at a point on the feature grid
    Type list[int]

property num_levels
    number of feature levels that the generator will be applied
    Type int

single_level_grid_anchors(base_anchors, featmap_size, stride=(16, 16), device='cuda')
    Generate grid anchors of a single level.

Note: This function is usually called by method self.grid_anchors.

## Parameters

• base_anchors (torch.Tensor) – The base anchors of a feature grid.

• featmap_size (tuple[int]) – Size of the feature maps.

• stride (tuple[int], optional) – Stride of the feature map in order (w, h). Defaults to (16, 16).

• device (str, optional) – Device the tensor will be put on. Defaults to ‘cuda’.

Returns Anchors in the overall feature maps.

Return type torch.Tensor

single_level_grid_priors(featmap_size, level_idx, dtype=torch.float32, device='cuda')

Generate grid anchors of a single level.

Note: This function is usually called by method self.grid_priors.

## Parameters

• featmap_size (tuple[int]) – Size of the feature maps.

• level_idx(int) – The index of corresponding feature map level.

• (obj (dtype) – torch.dtype): Date type of points.Defaults to torch.float32.