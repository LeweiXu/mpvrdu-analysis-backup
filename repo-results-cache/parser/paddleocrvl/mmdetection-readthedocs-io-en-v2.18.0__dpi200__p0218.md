### 37.4 mask

class mmdet.core.mask.BaseInstanceMasks

Base class for instance masks.

abstract property areas

areas of each instance.

Type ndarray

abstract crop(bbox)

Crop each mask by the given box.

Parameters bbox (ndarray) – Bbox in format [x1, y1, x2, y2], shape (4, ).

Returns The cropped masks.

Return type BaseInstanceMasks

abstract crop_and_resize(bboxes, out_shape, inds, device, interpolation='bilinear', binarize=True)

Crop and resize masks by the given bboxes.

This function is mainly used in mask targets computation. It firstly align mask to bboxes by assigned_inds, then crop mask by the assigned bbox and resize to the size of (mask_h, mask_w)

## Parameters

• bboxes (Tensor) – Bboxes in format [x1, y1, x2, y2], shape (N, 4)

• out_shape (tuple[int]) – Target (h, w) of resized mask

• inds (ndarray) – Indexes to assign masks to each bbox, shape (N,) and values should be between [0, num_masks - 1].

• device (str) – Device of bboxes

• interpolation (str) – See mmcv.imresize

• binarize (bool) – if True fractional values are rounded to 0 or 1 after the resize operation. If False and unsupported an error will be raised. Defaults to True.

Returns the cropped and resized masks.

Return type BaseInstanceMasks

abstract expand(expanded_h, expanded_w, top, left) see Expand.

abstract flip(flip_direction='horizontal')

Flip masks alone the given direction.

Parameters flip_direction(str) – Either ‘horizontal’ or ‘vertical’.

Returns The flipped masks.

Return type BaseInstanceMasks

abstract pad(out_shape, pad_val)

Pad masks to the given size of  $ (h, w) $.

Parameters

• out_shape (tuple[int]) – Target (h, w) of padded mask.

• pad_val (int) – The padded value.

Returns The padded masks.