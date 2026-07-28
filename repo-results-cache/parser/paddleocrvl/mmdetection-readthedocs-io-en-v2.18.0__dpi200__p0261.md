static random_select(img_scales)

Randomly select an img_scale from given candidates.

Parameters img_scales (list[tuple]) – Images scales for selection.

Returns Returns a tuple (img_scale, scale_dix), where img_scale is the selected image scale and scale_idx is the selected index in the given candidates.

Return type (tuple, int)

class mmdet.datasets.pipelines.Rotate(level, scale=1, center=None, img_fill_val=128)

seg_ignore_label=255, prob=0.5, max_rotate_angle=30,

random\_negative\_prob=0.5

Apply Rotate Transformation to image (and its corresponding bbox, mask, segmentation).

## Parameters

• level (int / float) – The level should be in range (0, MAX_LEVEL].

• scale (int / float) – Isotropic scale factor. Same in mmcv.imrotate.

• center (int | float | tuple[float]) – Center point (w, h) of the rotation in the source image. If None, the center of the image will be used. Same in mmcv.imrotate.

• img_fill_val (int | float | tuple) – The fill value for image border. If float, the same value will be used for all the three channels of image. If tuple, the should be 3 elements (e.g. equals the number of channels for image).

- seg_ignore_label(int) – The fill value used for segmentation map. Note this value must equals ignore_label in semantic_head of the corresponding config. Default 255.

• prob (float) – The probability for perform transformation and should be in range 0 to 1.

• max_rotate_angle (int / float) – The maximum angles for rotate transformation.

• random_negative_prob (float) – The probability that turns the offset negative.

class mmdet.datasets.pipelines.SegRescale(scale_factor=1, backend='cv2')

Rescale semantic segmentation maps.

## Parameters

• scale factor (float) – The scale factor of the final output.

• backend (str) – Image rescale backend, choices are ‘cv2’ and ‘pillow’. These two backends generate slightly different results. Defaults to ‘cv2’.

class mmdet.datasets.pipelines.Shear(level, img_fill_val=128, seg_ignore_label=255, prob=0.5)

direction='horizontal', max_shear_magnitude=0.3,

random_negative_prob=0.5, interpolation='bilinear'

Apply Shear Transformation to image (and its corresponding bbox, mask, segmentation).

## Parameters

• level (int / float) – The level should be in range [0, MAX_LEVEL].

• img_fill_val (int | float | tuple) – The filled values for image border. If float, the same fill value will be used for all the three channels of image. If tuple, the should be 3 elements.

- seg_ignore_label(int) – The fill value used for segmentation map. Note this value must equals ignore_label in semantic_head of the corresponding config. Default 255.

• prob (float) – The probability for performing Shear and should be in range [0, 1].

• direction (str) – The direction for shear, either “horizontal” or “vertical”.