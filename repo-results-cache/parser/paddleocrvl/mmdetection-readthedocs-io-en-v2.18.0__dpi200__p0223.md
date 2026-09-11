Polygons is a list of three levels. The first level of the list corresponds to objects, the second level to the polys that compose the object, the third level to the poly coordinates

## Parameters

• masks (list[list[ndarray]]) – The first level of the list corresponds to objects, the second level to the polys that compose the object, the third level to the poly coordinates

• height (int) – height of masks

• width(int) – width of masks

## Example

>>> from mmdet.core.mask.structures import *  # NOQA
>>> masks = [
>>>     [ np.array([0, 0, 10, 0, 10, 10., 0, 10, 0, 0]) ]
>>> ]
>>> height, width = 16, 16
>>> self = PolygonMasks(masks, height, width)

>>> # demo translate

>>> new = self.translate((16, 16), 4., direction='horizontal')
>>> assert np.all(new.masks[0][0][1::2] == masks[0][0][1::2])
>>> assert np.all(new.masks[0][0][0::2] == masks[0][0][0::2] + 4)

>>> # demo crop_and_resize
>>> num_boxes = 3
>>> bboxes = np.array([[0, 0, 30, 10.0]] * num_boxes)
>>> out_shape = (16, 16)
>>> inds = torch.randint(0, len(self), size=(num_boxes,))
>>> device = 'cpu'
>>> interpolation = 'bilinear'
>>> new = self.crop_and_resize(
...     bboxes, out_shape, inds, device, interpolation)
>>> assert len(new) == num_boxes
>>> assert new.height, new.width == out_shape

## property areas

This func is modified from detectron2. The function only works with Polygons using the shoelace formula.

Return type ndarray
crop(bbox)
see BaseInstanceMasks.crop()
crop_and_resize(bboxes, out_shape, inds, device='cpu', interpolation='bilinear', binarize=True)
see BaseInstanceMasks.crop_and_resize()
expand(*args, **kwargs)
TODO: Add expand for polygon
flip(flip_direction='horizontal')
see BaseInstanceMasks.flip()