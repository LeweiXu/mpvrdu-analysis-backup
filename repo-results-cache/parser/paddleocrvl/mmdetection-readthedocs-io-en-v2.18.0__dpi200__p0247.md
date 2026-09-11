(continued from previous page)

scale_limit=0.0,
rotate_limit=0,
interpolation=1,
p=0.5),
dict(
    type='RandomBrightnessContrast',
    brightness_limit=[0.1, 0.3],
    contrast_limit=[0.1, 0.3],
    p=0.2),
dict(type='ChannelShuffle', p=0.1),
dict(
    type='OneOf',
    transforms=[
        dict(type='Blur', blur_limit=3, p=1.0),
        dict(type='MedianBlur', blur_limit=3, p=1.0)
    ],
    p=0.1),
]

## Parameters

• transforms (list[dict]) – A list of albu transformations

• bbox_params (dict) – Bbox_params for albumentation Compose

• keymap (dict) – Contains {‘input key’:’albumentation-style key’}

• skip_img_without_anno (bool) – Whether to skip the image if no ann left after aug

## albu_builder(cfg)

Import a module from albumentations.

It inherits some of build_from_cfg() logic.

Parameters cfg(dict) – Config dict. It should at least contain the key “type”.

Returns The constructed object.

Return type obj

static mapper(d, keymap)

Dictionary mapper. Renames keys according to keymap provided.

Parameters

• d(dict) - old dict

• keymap (dict) - { 'old_key': 'new_key' }

Returns new dict.

Return type dict

##### class mmdet.datasets.pipelines.AutoAugment(policies)

Auto augmentation.

This data augmentation is proposed in Learning Data Augmentation Strategies for Object Detection.

TODO: Implement ‘Shear’, ‘Sharpness’ and ‘Rotate’ transforms