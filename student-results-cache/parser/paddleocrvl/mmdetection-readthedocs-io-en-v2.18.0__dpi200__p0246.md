Return type list

## Examples

>>> pipelines = [
...     dict(type='LoadImageFromFile'),
...     dict(
...         type='MultiScaleFlipAug',
...         img_scale=(1333, 800),
...         flip=False,
...         transforms=[
...             dict(type='Resize', keep_ratio=True),
...             dict(type='RandomFlip'),
...             dict(type='Normalize', mean=[0, 0, 0], std=[1, 1, 1]),
...             dict(type='Pad', size_divisor=32),
...             dict(type='ImageToTensor', keys=['img']),
...             dict(type='Collect', keys=['img']),
...         ]
...     ]
...
>>> expected_pipelines = [
...     dict(type='LoadImageFromFile'),
...     dict(
...         type='MultiScaleFlipAug',
...         img_scale=(1333, 800),
...         flip=False,
...         transforms=[
...             dict(type='Resize', keep_ratio=True),
...             dict(type='RandomFlip'),
...             dict(type='Normalize', mean=[0, 0, 0], std=[1, 1, 1]),
...             dict(type='Pad', size_divisor=32),
...             dict(type='DefaultFormatBundle'),
...             dict(type='Collect', keys=['img']),
...         ]
...     ]
>>> assert expected_pipelines == replace_ImageToTensor(pipelines)

### 38.2 pipelines

class mmdet.datasets.pipelines.Albu(transforms, bbox_params=None, keymap=None, update_pad_shape=False, skip_img_without_anno=False)

Albumentation augmentation.

Adds custom transformations from Albumentations library. Please, visit https://albumentations.readthedocs.io to get more information.

An example of transforms is as followed:

dict(
    type='ShiftScaleRotate',
    shift_limit=0.0625,

(continues on next page)