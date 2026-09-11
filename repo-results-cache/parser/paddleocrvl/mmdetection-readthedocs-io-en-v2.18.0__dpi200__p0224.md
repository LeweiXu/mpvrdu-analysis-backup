Generate random polygon masks for demo / testing purposes.

Adapted from Page 196, 1

References

Example

>>> from mmdet.core.mask.structures import PolygonMasks
>>> self = PolygonMasks.random()
>>> print('self = {}'.format(self))

rescale(scale, interpolation=None)
see BaseInstanceMasks.rescale()

resize(out_shape, interpolation=None)
see BaseInstanceMasks.resize()

rotate(out_shape, angle, center=None, scale=1.0, fill_val=0)
See BaseInstanceMasks.rotate().

shear(out_shape, magnitude, direction='horizontal', border_value=0, interpolation='bilinear')
See BaseInstanceMasks.shear().

to_ bitmap()
convert polygon masks to bitmap masks.

to_ndarray()
Convert masks to the format of ndarray.

to_tensor(dtype, device)
See BaseInstanceMasks.to_tensor().

translate(out_shape, offset, direction='horizontal', fill_val=None, interpolation=None)
Translate the PolygonMasks.

Example

>>> self = PolygonMasks.random(dtype=np.int)
>>> out_shape = (self.height, self.width)
>>> new = self.translate(out_shape, 4., direction='horizontal')
>>> assert np.all(new.masks[0][0][1::2] == self.masks[0][0][1::2])
>>> assert np.all(new.masks[0][0][0::2] == self.masks[0][0][0::2] + 4)  # noqa:
↔ E501

mmdet.core.mask.encode_mask_results(mask_results)

Encode bitmap mask to RLE code.

Parameters mask_results(list / tuple[list]) – bitmap mask results. In mask scoring rcnn, mask_results is a tuple of (segm_results, segm_cls_score).

Returns RLE encoded mask.