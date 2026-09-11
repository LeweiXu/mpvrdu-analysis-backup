1. The center offset of V1.x anchors are set to be 0.5 rather than 0.

2. The width/height are minused by 1 when calculating the anchors’ centers and corners to meet the V1.x coordinate system.

3. The anchors’ corners are quantized.

## Parameters

• strides (list[int] | list[tuple[int]]) – Strides of anchors in multiple feature levels.

• ratios (list[float]) – The list of ratios between the height and width of anchors in a single level.

- scales (list[int] / None) – Anchor scales for anchors in a single level. It cannot be set at the same time if octave_base_scale and scales_per_octave are set.

• base_sizes (list[int]) – The basic sizes of anchors in multiple levels. If None is given, strides will be used to generate base_sizes.

• scale_major (bool) – Whether to multiply scales first when generating base anchors. If true, the anchors in the same row will have the same scales. By default it is True in V2.0

• octave_base_scale(int) – The base scale of octave.

- scales_per_octave (int) – Number of scales for each octave. octave_base_scale and scales_per_octave are usually used in retinanet and the scales should be None when they are set.

- centers (list[tuple[float, float]] | None) – The centers of the anchor relative to the feature grid center in multiple feature levels. By default it is set to be None and not used. It a list of float is given, this list will be used to shift the centers of anchors.

• center_offset (float) – The offset of center in proportion to anchors’ width and height. By default it is 0.5 in V2.0 but it should be 0.5 in v1.x models.

## Examples

>>> from mmdet.core import LegacyAnchorGenerator
>>> self = LegacyAnchorGenerator(
>>> [16], [1.], [1.], [9], center_offset=0.5)
>>> all_anchors = self.grid_anchors(((2, 2),), device='cpu')
>>> print(all_anchors)
[tensor([[0., 0., 8., 8.],
[16., 0., 24., 8.],
[0., 16., 8., 24.],
[16., 16., 24., 24.]])]

gen_single_level_base_anchors(base_size, scales, ratios, center=None)

Generate base anchors of a single level.

Note: The width/height of anchors are minused by 1 when calculating the centers and corners to meet the V1.x coordinate system.

## Parameters