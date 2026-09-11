Returns Converted masks in the format of ndarray.

## Return type ndarray

abstract to_tensor(dtype, device)

Convert masks to the format of Tensor.

## Parameters

• dtype (str) – Dtype of converted mask.

• device (torch.device) – Device of converted masks.

Returns Converted masks in the format of Tensor.

Return type Tensor

abstract translate(out_shape, offset, direction='horizontal', fill_val=0, interpolation='bilinear')

Translate the masks.

## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• offset (int | float) – The offset for translate.

• direction (str) – The translate direction, either “horizontal” or “vertical”.

• fill_val (int / float) – Border value. Default 0.

• interpolation (str) – Same as mmcv.imtranslate().

Returns Translated masks.

class mmdet.core.mask.BitmapMasks(masks, height, width)

This class represents masks in the form of bitmaps.

## Parameters

• masks (ndarray) – ndarray of masks in shape (N, H, W), where N is the number of objects.

• height (int) – height of masks

• width (int) – width of masks

## Example

>>> from mmdet.core.mask.structures import *  # NOQA
>>> num_masks, H, W = 3, 32, 32
>>> rng = np.random.RandomState(0)
>>> masks = (rng.rand(num_masks, H, W) > 0.1).astype(np.int)
>>> self =BitmapMasks(masks, height=H, width=W)

>>> # demo crop_and_resize
>>> num_boxes = 5
>>> bboxes = np.array([[0, 0, 30, 10.0]] * num_boxes)
>>> out_shape = (14, 14)
>>> inds = torch.randint(0, len(self), size=(num_boxes,))
>>> device = 'cpu'
>>> interpolation = 'bilinear'
>>> new = self.crop_and_resize(
...     bboxes, out_shape, inds, device, interpolation)

(continues on next page)