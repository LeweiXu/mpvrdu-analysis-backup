• std (sequence) – Std values of 3 channels.

• to_rgb (bool) – Whether to convert the image from BGR to RGB.

• test_mode (bool) – whether involve random variables in transform. In train mode, crop_size is fixed, center coords and ratio is random selected from predefined lists. In test mode, crop_size is image's original shape, center coords and ratio is fixed.

• test_pad_mode (tuple) – padding method and padding shape value, only available in test mode. Default is using ‘logical_or’ with 127 as padding shape value.

– 'logical_or': final_shape = input_shape | padding_shape_value

–'size_divisor': final_shape = int(ceil(input_shape / padding_shape_value) * padding_shape_value)

• test_pad_add_pix(int) – Extra padding pixel in test mode. Default 0.

• bbox_clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

class mmdet.datasets.pipelines.RandomCrop(crop_size, crop_type='absolute', allow_negative_crop=False, recompute_bbox=False, bbox_clip_border=True)

Random crop the image & bboxes & masks.

The absolute  $ crop\_size $ is sampled based on  $ crop\_type $ and  $ image\_size $, then the cropped results are generated.

## Parameters

• crop_size (tuple) – The relative ratio or absolute pixels of height and width.

• crop_type (str, optional) – one of “relative_range”, “relative”, “absolute”, “absolute_range”. “relative” randomly crops (h * crop_size[0], w * crop_size[1]) part from an input of size (h, w). “relative_range” uniformly samples relative crop size from range [crop_size[0], 1] and [crop_size[1], 1] for height and width respectively. “absolute” crops from an input with absolute size (crop_size[0], crop_size[1]). “absolute_range” uniformly samples crop_h in range [crop_size[0], min(h, crop_size[1])] and crop_w in range [crop_size[0], min(w, crop_size[1])]. Default “absolute”.

• allow_negative_crop (bool, optional) – Whether to allow a crop that does not contain any bbox area. Default False.

• recompute_bbox(bool, optional) – Whether to re-compute the boxes based on cropped instance masks. Default False.

• bbox_clip_border (bool, optional) – Whether clip the objects outside the border of the image. Defaults to True.

## Note:

• If the image is smaller than the absolute crop size, return the original image.

• The keys for bboxes, labels and masks must be aligned. That is,  $ gt\_bboxes $ corresponds to  $ gt\_labels $ and  $ gt\_masks $, and  $ gt\_bboxes\_ignore $ corresponds to  $ gt\_labels\_ignore $ and  $ gt\_masks\_ignore $.

• If the crop does not contain any gt-bbox region and allow_negative_crop is set to False, skip this image.

##### class mmdet.datasets.pipelines.RandomFlip(flip_ratio=None, direction='horizontal')

Flip the image & bbox & mask.

If the input dict contains the key “flip”, then the flag will be used, otherwise it will be randomly decided by a ratio specified in the init method.