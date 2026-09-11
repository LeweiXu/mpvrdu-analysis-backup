>>> assert len(new) == num_boxes
>>> assert new.height, new.width == out_shape

(continued from previous page)

property areas
See BaseInstanceMasks.areas.

crop(bbox)
See BaseInstanceMasks.crop().

crop_and_resize(bboxes, out_shape, inds, device='cpu', interpolation='bilinear', binarize=True)
See BaseInstanceMasks.crop_and_resize().

expand(expanded_h, expanded_w, top, left)
See BaseInstanceMasks.expand().

flip(flip_direction='horizontal')
See BaseInstanceMasks.flip().

pad(out_shape, pad_val=0)
See BaseInstanceMasks.pad().

classmethod random(num_masks=3, height=32, width=32, dtype=<class 'numpy.uint8'>, rng=None)
Generate random bitmap masks for demo / testing purposes.

## Example

>>> from mmdet.core.mask.structures importBitmapMasks
>>> self =BitmapMasks.random()
>>> print('self = {}'.format(self))
self =BitmapMasks(num_masks=3, height=32, width=32)
rescale(scale, interpolation='nearest')
See BaseInstanceMasks.rescale().

resize(out_shape, interpolation='nearest')
See BaseInstanceMasks.resize().

rotate(out_shape, angle, center=None, scale=1.0, fill_val=0)
Rotate theBitmapMasks.

## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• angle (int / float) – Rotation angle in degrees. Positive values mean counterclockwise rotation.

• center (tuple[float], optional) – Center point (w, h) of the rotation in source image. If not specified, the center of the image will be used.

• scale (int / float) – Isotropic scale factor.

• fill_val (int / float) – Border value. Default 0 for masks.

Returns RotatedBitmapMasks.

Return typeBitmapMasks

shear(out_shape, magnitude, direction='horizontal', border_value=0, interpolation='bilinear')

Shear theBitmapMasks.