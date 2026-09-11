MMDetection, Release 2.18.0
Parameters
- transforms (list[dict]) – Transforms to apply in each augmentation.
- img_scale (tuple / list[tuple] / None) – Images scales for resizing.
- scale_factor(float / list[float] / None) – Scale factors for resizing.
- flip (bool) – Whether apply flip augmentation. Default: False.
- flip_direction (str / list[str]) – Flip augmentation directions, options are “horizontal”, “vertical” and “diagonal”. If flip_direction is a list, multiple flip augmentations will be applied. It has no effect when flip == False. Default: “horizontal”.
class mmdet.datasets.pipelines.Normalize(mean, std, to_rgb=True)
Normalize the image.
Added key is "img_norm_cfg".
Parameters
- mean (sequence) – Mean values of 3 channels.
- std (sequence) – Std values of 3 channels.
- to_rgb (bool) – Whether to convert the image from BGR to RGB, default is true.
class mmdet.datasets.pipelines.Pad(size=None, size_divisor=None, pad_to_square=False, pad_val={'img': 0, 'masks': 0, 'seg': 255})
Pad the image & masks & segmentation map.
There are two padding modes: (1) pad to a fixed size and (2) pad to the minimum size that is divisible by some number. Added keys are “pad_shape”, “pad_fixed_size”, “pad_size_divisor”,
Parameters
- size (tuple, optional) – Fixed padding size.
- size_divisor (int, optional) – The divisor of padded size.
- pad_to_square (bool) – Whether to pad the image into a square. Currently only used for YOLOX. Default: False.
- pad_val (dict, optional) – A dict for padding value, the default value is dict(img=0, masks=0, seg=255).
class mmdet.datasets.pipelines.PhotoMetricDistortion(brightness_delta=32, contrast_range=(0.5,
1.5), saturation_range=(0.5, 1.5),
hue_delta=18)
Apply photometric distortion to image sequentially, every transformation is applied with a probability of 0.5. The position of random contrast is in second or second to last.
1. random brightness
2. random contrast (mode 0)
3. convert color from BGR to HSV
4. random saturation
5. random hue
6. convert color from HSV to BGR
7. random contrast (mode 1)
8. randomly swap channels
248
Chapter 38. mmdet.datasets