scale in the init method is used. If the input dict contains the key “scale_factor” (if MultiScaleFlipAug does not give img_scale but scale_factor), the actual scale will be computed by image shape and scale_factor.

img_scale can either be a tuple (single-scale) or a list of tuple (multi-scale). There are 3 multiscale modes:

• ratio_range is not None: randomly sample a ratio from the ratio range and multiply it with the image scale.

• ratio_range is None and multiscale_mode == "range": randomly sample a scale from the multiscale range.

• ratio_range is None and multiscale_mode == "value": randomly sample a scale from multiple scales.

## Parameters

• img_scale (tuple or list[tuple]) – Images scales for resizing.

• multiscale_mode(str) – Either “range” or “value”.

• ratio_range (tuple[float]) – (min_ratio, max_ratio)

• keep_ratio (bool) – Whether to keep the aspect ratio when resizing the image.

• bbox_clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

• backend (str) – Image resize backend, choices are ‘cv2’ and ‘pillow’. These two backends generate slightly different results. Defaults to ‘cv2’.

• override (bool, optional) – Whether to override scale and scale_factor so as to call resize twice. Default False. If True, after the first resizing, the existed scale and scale_factor will be ignored so the second resizing can be allowed. This option is a work-around for multiple times of resize in DETR. Defaults to False.

## static random_sample(img_scales)

Randomly sample an img_scale when multiscale_mode == 'range'.

Parameters img_scales (list[tuple]) – Images scale range for sampling. There must be two tuples in img_scales, which specify the lower and upper bound of image scales.

Returns Returns a tuple (img_scale, None), where img_scale is sampled scale and None is just a placeholder to be consistent with random_select().

Return type (tuple, None)

## static random_sample_ratio(img_scale, ratio_range)

Randomly sample an img_scale when ratio_range is specified.

A ratio will be randomly sampled from the range specified by ratio_range. Then it would be multiplied with img_scale to generate sampled scale.

## Parameters

• img_scale (tuple) – Images scale base to multiply with ratio.

• ratio_range (tuple[float]) – The minimum and maximum ratio to scale the img_scale.

Returns Returns a tuple (scale, None), where scale is sampled ratio multiplied with img_scale and None is just a placeholder to be consistent with random_select().

Return type (tuple, None)