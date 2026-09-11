## Return type BaseInstanceMasks

abstract rescale(scale, interpolation='nearest')

Rescale masks as large as possible while keeping the aspect ratio. For details can refer to mmcv.imrescale.

## Parameters

• scale (tuple[int]) – The maximum size (h, w) of rescaled mask.

• interpolation (str) – Same as mmcv.imrescale().

Returns The rescaled masks.

Return type BaseInstanceMasks

abstract resize(out_shape, interpolation='nearest')

Resize masks to the given out_shape.

## Parameters

• out_shape – Target (h, w) of resized mask.

• interpolation (str) – See mmcv.imresize().

Returns The resized masks.

Return type BaseInstanceMasks

abstract rotate(out_shape, angle, center=None, scale=1.0, fill_val=0)

Rotate the masks.

## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• angle (int / float) – Rotation angle in degrees. Positive values mean counterclockwise rotation.

• center (tuple[float], optional) – Center point (w, h) of the rotation in source image. If not specified, the center of the image will be used.

• scale (int / float) – Isotropic scale factor.

• fill_val (int / float) – Border value. Default 0 for masks.

Returns Rotated masks.

shear(out_shape, magnitude, direction='horizontal', border_value=0, interpolation='bilinear') Shear the masks.

## Parameters

• out_shape (tuple[int]) – Shape for output mask, format (h, w).

• magnitude (int / float) – The magnitude used for shear.

• direction (str) – The shear direction, either “horizontal” or “vertical”.

• border_value (int / tuple[int]) – Value used in case of a constant border. Default 0.

• interpolation (str) – Same as in mmcv.imshear().

Returns Sheared masks.

Return type ndarray

abstract to_ndarray()

Convert masks to the format of ndarray.