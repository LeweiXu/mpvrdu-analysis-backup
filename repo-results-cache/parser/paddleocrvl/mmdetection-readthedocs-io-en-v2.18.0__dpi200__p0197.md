##### class mmdet.core.anchor.YOLOAnchorGenerator(strides, base_sizes)

## Anchor generator for YOLO

## Parameters

• strides (list[int] | list[tuple[int, int]]) – Strides of anchors in multiple feature levels.

• base_sizes (list[list[tuple[int, int]]]) – The basic sizes of anchors in multiple levels.

## gen_base_anchors()

Generate base anchors.

Returns Base anchors of a feature grid in multiple feature levels.

Return type list(torch.Tensor)

gen_single_level_base_anchors(base_sizes_per_level, center=None)

Generate base anchors of a single level.

## Parameters

• base_sizes_per_level (list[tuple[int, int]]) – Basic sizes of anchors.

• center (tuple[float], optional) – The center of the base anchor related to a single feature grid. Defaults to None.

Returns Anchors in a single-level feature maps.

Return type torch.Tensor

## property num_levels

number of feature levels that the generator will be applied

Type int

responsible_flags(featmap_sizes, gt_bboxes, device='cuda')

Generate responsible anchor flags of grid cells in multiple scales.

## Parameters

• featmap sizes (list(tuple)) – List of feature map sizes in multiple feature levels.

• gt_bboxes (Tensor) – Ground truth boxes, shape (n, 4).

• device (str) – Device where the anchors will be put on.

Returns responsible flags of anchors in multiple level

Return type list(torch.Tensor)

single_level_responsible_flags(featmap_size, gt_bboxes, stride, num_base_anchors, device='cuda')

Generate the responsible flags of anchor in a single feature map.

## Parameters

• featmap_size (tuple[int]) – The size of feature maps.

• gt_bboxes (Tensor) – Ground truth boxes, shape (n, 4).

• stride (tuple(int)) – stride of current level

• num_base_anchors (int) – The number of base anchors.

• device (str, optional) – Device where the flags will be put on. Defaults to ‘cuda’.

Returns The valid flags of each anchor in a single level feature map.