## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• magnitude (int / float) – The magnitude used for shear.

• direction (str) – The shear direction, either “horizontal” or “vertical”.

• border_value (int / tuple[int]) – Value used in case of a constant border.

• interpolation (str) – Same as in mmcv.imshear().

Returns The sheared masks.

Return type BitmapMasks

## to_ndarray()

See BaseInstanceMasks.to_ndarray().

## to_tensor(dtype, device)

See BaseInstanceMasks.to_tensor().

translate(out_shape, offset, direction='horizontal', fill_val=0, interpolation='bilinear')

Translate theBitmapMasks.

## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• offset (int | float) – The offset for translate.

• direction (str) – The translate direction, either “horizontal” or “vertical”.

• fill_val (int / float) – Border value. Default 0 for masks.

• interpolation (str) – Same as mmcv.imtranslate().

Returns TranslatedBitmapMasks.

Return typeBitmapMasks

## Example

>>> from mmdet.core.mask.structures importBitmapMasks

>>> self =BitmapMasks.random(dtype=np.uint8)

>>> out_shape = (32, 32)

>>> offset = 4

>>> direction = 'horizontal'

>>> fill_val = 0

>>> interpolation = 'bilinear'

>>> # Note, There seem to be issues when:

>>> # * out_shape is different than self's shape

>>> # * the mask dtype is not supported by cv2.AffineWarp

>>> new = self.translate(out_shape, offset, direction, fill_val,
                               interpolation)

>>> assert len(new) == len(self)

>>> assert new.height, new.width == out_shape

class mmdet.core.mask.PolygonMasks(masks, height, width)

This class represents masks in the form of polygons.