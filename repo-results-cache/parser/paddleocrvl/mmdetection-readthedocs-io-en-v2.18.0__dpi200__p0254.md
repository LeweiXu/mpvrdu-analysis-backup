(continued from previous page)

The mosaic transform steps are as follows:
1. Choose the mosaic center as the intersections of 4 images
2. Get the left top image according to the index, and randomly sample another 3 images from the custom dataset.
3. Sub image will be cropped if image is larger than mosaic patch

## Parameters

• img_scale (Sequence[int]) – Image size after mosaic pipeline of single image. Default to (640, 640).

• center_ratio_range (Sequence $$ float $$ ) – Center ratio range of mosaic output. Default to (0.5, 1.5).

• min_bbox_size (int | float) – The minimum pixel for filtering invalid bboxes after the mosaic pipeline. Default to 0.

• pad_val (int) – Pad value. Default to 114.

## get_indexes(dataset)

Call function to collect indexes.

Parameters dataset (MultiImageMixDataset) – The dataset.

Returns indexes.

Return type list

class mmdet.datasets.pipelines.MultiScaleFlipAug(transforms, img_scale=None, scale_factor=None, flip=False, flip_direction='horizontal')

Test-time augmentation with multiple scales and flipping.

An example configuration is as followed:

img_scale=[(1333, 400), (1333, 800)],
flip=True,
transforms=[
dict(type='Resize', keep_ratio=True),
dict(type='RandomFlip'),
dict(type='Normalize', **img_norm_cfg),
dict(type='Pad', size_divisor=32),
dict(type='ImageToTensor', keys=['img']),
dict(type='Collect', keys=['img']),
]

After MultiScaleFLipAug with above configuration, the results are wrapped into lists of the same length as followed:

dict(
    img=[ $ \ldots $],
    img_shape=[...],
    scale=[(1333, 400), (1333, 400), (1333, 800), (1333, 800)]
    flip=[False, True, False, True]
)