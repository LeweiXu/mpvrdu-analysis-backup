# MMDET.CORE

### 37.1 anchor

class mmdet.core.anchor.AnchorGenerator(strides, ratios, scales=None, base_sizes=None,

 $$ scales\_{p}er\_{o}ctave=None,centers=None,center\_{o}f fset=0.0) $$ 

Standard anchor generator for 2D anchor-based detectors.

## Parameters

• strides (list[int] | list[tuple[int, int]]) – Strides of anchors in multiple feature levels in order (w, h).

• ratios (list[float]) – The list of ratios between the height and width of anchors in a single level.

- scales (list[int] / None) – Anchor scales for anchors in a single level. It cannot be set at the same time if octave_base_scale and scales_per_octave are set.

• base_sizes (list[int] / None) – The basic sizes of anchors in multiple levels. If None is given, strides will be used as base_sizes. (If strides are non square, the shortest stride is taken.)

• scale_major (bool) – Whether to multiply scales first when generating base anchors. If true, the anchors in the same row will have the same scales. By default it is True in V2.0

• octave_base_scale(int) – The base scale of octave.

- scales_per_octave (int) – Number of scales for each octave. octave_base_scale and scales_per_octave are usually used in retinanet and the scales should be None when they are set.

- centers (list[tuple[float, float]] | None) – The centers of the anchor relative to the feature grid center in multiple feature levels. By default it is set to be None and not used. If a list of tuple of float is given, they will be used to shift the centers of anchors.

• center_offset (float) – The offset of center in proportion to anchors’ width and height. By default it is 0 in V2.0.