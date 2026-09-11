## Examples

>>> from mmdet.core import AnchorGenerator

>>> self = AnchorGenerator([16], [1.], [1.], [9])

>>> all_anchors = self.grid_priors([(2, 2)], device='cpu')

>>> print(all_anchors)

[tensor([[−4.5000, −4.5000, 4.5000, 4.5000],
                [11.5000, −4.5000, 20.5000, 4.5000],
                [-4.5000, 11.5000, 4.5000, 20.5000],
                [11.5000, 11.5000, 20.5000, 20.5000]])]

>>> self = AnchorGenerator([16, 32], [1.], [1.], [9, 18])

>>> all_anchors = self.grid_priors([(2, 2), (1, 1)], device='cpu')

>>> print(all_anchors)

[tensor([[−4.5000, −4.5000, 4.5000, 4.5000],
                [11.5000, −4.5000, 20.5000, 4.5000],
                [-4.5000, 11.5000, 4.5000, 20.5000],
                [11.5000, 11.5000, 20.5000, 20.5000]])],
                tensor([[−9., −9., 9., 9.
→]])]

gen_base_anchors()

Generate base anchors.

Returns Base anchors of a feature grid in multiple feature levels.

Return type list(torch.Tensor)

gen_single_level_base_anchors(base_size, scales, ratios, center=None)

Generate base anchors of a single level.

## Parameters

• base_size (int / float) – Basic size of an anchor.

• scales (torch.Tensor) – Scales of the anchor.

• ratios (torch.Tensor) – The ratio between the height and width of anchors in a single level.

• center (tuple[float], optional) – The center of the base anchor related to a single feature grid. Defaults to None.

Returns Anchors in a single-level feature maps.

Return type torch.Tensor

grid_anchors(featmap_sizes, device='cuda')

Generate grid anchors in multiple feature levels.

Parameters

• featmap sizes (list [tuple]) – List of feature map sizes in multiple feature levels.

• device (str) – Device where the anchors will be put on.

Returns Anchors in multiple feature levels. The sizes of each tensor should be [N, 4], where N = width * height * num_base_anchors, width and height are the sizes of the corresponding feature level, num_base_anchors is the number of anchors for that level.

Return type list[torch.Tensor]

grid_priors(featmap_sizes, dtype=torch.float32, device='cuda')

Generate grid anchors in multiple feature levels.