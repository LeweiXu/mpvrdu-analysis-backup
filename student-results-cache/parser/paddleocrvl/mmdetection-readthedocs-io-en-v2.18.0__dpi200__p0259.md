When random flip is enabled, flip_ratio/direction can either be a float/string or tuple of float/string. There are 3 flip modes:

• flip_ratio is float, direction is string: the image will be direction`ly flipped with probability of `flip_ratio. E.g., flip_ratio=0.5, direction='horizontal', then image will be horizontally flipped with probability of 0.5.

• flip_ratio is float, direction is list of string: the image will be direction[i]`ly flipped with probability of `flip_ratio/len(direction). E.g., flip_ratio=0.5, direction=['horizontal','vertical'], then image will be horizontally flipped with probability of 0.25, vertically with probability of 0.25.

• flip_ratio is list of float, direction is list of string: given len(flip_ratio) == len(direction), the image will be direction[i]'ly flipped with probability of `flip_ratio[i]`. E.g., flip_ratio=[0.3, 0.5], direction=['horizontal','vertical'], then image will be horizontally flipped with probability of 0.3, vertically with probability of 0.5.

## Parameters

• flip_ratio (float / list[float], optional) – The flipping probability. Default: None.

• direction (str / list[str], optional) – The flipping direction. Options are ‘horizontal’, ‘vertical’, ‘diagonal’. Default: ‘horizontal’. If input is a list, the length must equal flip_ratio. Each element in flip_ratio indicates the flip probability of corresponding direction.

## bbox_flip(bboxes, img_shape, direction)

Flip bboxes horizontally.

## Parameters

• bboxes (numpy.ndarray) – Bounding boxes, shape (…, 4*k)

• img_shape (tuple[int]) – Image shape (height, width)

• direction (str) – Flip direction. Options are ‘horizontal’, ‘vertical’.

Returns Flipped bounding boxes.

Return type numpy.ndarray

class mmdet.datasets.pipelines.RandomShift(shift_ratio=0.5, max_shift_px=32, filter_thr_px=1)

Shift the image and box given shift pixels and probability.

## Parameters

• shift_ratio (float) – Probability of shifts. Default 0.5.

• max_shift_px(int) – The max pixels for shifting. Default 32.

• filter_thr_px(int) – The width and height threshold for filtering. The bbox and the rest of the targets below the width and height threshold will be filtered. Default 1.

class mmdet.datasets.pipelines.Resize(img_scale=None, multiscale_mode='range', ratio_range=None, keep_ratio=True, bbox_clip_border=True, backend='cv2', override=False)

Resize images & bbox & mask.

This transform resizes the input image to some scale. Bboxes and masks are then resized with the same scale factor. If the input dict contains the key “scale”, then the scale in the input dict is used, otherwise the specified