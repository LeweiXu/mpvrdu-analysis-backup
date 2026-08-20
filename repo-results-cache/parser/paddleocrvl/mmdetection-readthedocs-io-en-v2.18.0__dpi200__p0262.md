class mmdet.datasets.pipelines.Translate(level, prob=0.5, img_fill_val=128, seg_ignore_label=255, direction='horizontal', max_translate_offset=250.0, random_negative_prob=0.5, min_size=0)

• max_shear_magnitude (float) – The maximum magnitude for Shear transformation.

• random_negative_prob (float) – The probability that turns the offset negative. Should be in range [0,1]

• interpolation (str) – Same as in mmcv.imshear().

class mmdet.datasets.pipelines.ToDataContainer(fields=({'key': 'img','stack': True}, {'key': 'gt_bboxes'},

Convert results to mmcv.DataContainer by given fields.

Parameters fields (Sequence[dict]) – Each field is a dict like dict(key='xxx', **kwargs). The key in result will be converted to mmcv.DataContainer with **kwargs. Default: (dict(key='img', stack=True), dict(key='gt_bboxes'), dict(key='gt_labels'))).

class mmdet.datasets.pipelines.ToTensor(keys)

Convert some results to torch.Tensor by given keys.

Parameters keys (Sequence[str]) – Keys that need to be converted to Tensor.

Translate the images, bboxes, masks and segmentation maps horizontally or vertically.

## Parameters

• level (int / float) – The level for Translate and should be in range [0, MAX_LEVEL].

• prob (float) – The probability for performing translation and should be in range [0, 1].

• img_fill_val (int | float | tuple) – The filled value for image border. If float, the same fill value will be used for all the three channels of image. If tuple, the should be 3 elements (e.g. equals the number of channels for image).

- seg_ignore_label(int) – The fill value used for segmentation map. Note this value must equals ignore_label in semantic_head of the corresponding config. Default 255.

• direction (str) – The translate direction, either “horizontal” or “vertical”.

• max_translate_offset (int / float) – The maximum pixel’s offset for Translate.

• random_negative_prob (float) – The probability that turns the offset negative.

• min_size(int | float) – The minimum pixel for filtering invalid bboxes after the translation.

class mmdet.datasets.pipelines.Transpose(keys, order)

Transpose some results by given keys.

## Parameters

• keys (Sequence[str]) – Keys of results to be transposed.

• order (Sequence[int]) – Order of transpose.

mmdet.datasets.pipelines.to_tensor(data)

Convert objects of various python types to torch.Tensor.

Supported types are: numpy.ndarray, torch.Tensor, Sequence, int and float.

Parameters data (torch.Tensor | numpy.ndarray | Sequence | int | float) – Data to be converted.