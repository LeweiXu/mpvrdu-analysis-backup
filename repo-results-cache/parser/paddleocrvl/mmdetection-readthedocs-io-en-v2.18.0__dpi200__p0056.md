(continued from previous page)

type='CocoDataset', # Type of dataset, refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/datasets/coco.py#L19 for details.
ann_file='data/coco/annotations/instances_train2017.json', # Path of annotation
file
img_prefix='data/coco/train2017/', # Prefix of image path
pipeline=[ # pipeline, this is passed by the train_pipeline created before.
dict(type='LoadImageFromFile'),
dict(
    type='LoadAnnotations',
    with_bbox=True,
    with_mask=True,
    poly2mask=False),
    dict(type='Resize', img_scale=(1333, 800), keep_ratio=True),
    dict(type='RandomFlip', flip_ratio=0.5),
    dict(
        type='Normalize',
        mean=[123.675, 116.28, 103.53],
        std=[58.395, 57.12, 57.375],
        to_rgb=True),
    dict(type='Pad', size=divisor=32),
    dict(type='DefaultFormatBundle'),
    dict(
        type='Collect',
        keys=['img', 'gt_bboxes', 'gt_labels', 'gt_masks']
    ),
    val=dict( # Validation dataset config
        type='CocoDataset',
        ann_file='data/coco/annotations/instances_val2017.json',
        img_prefix='data/coco/val2017/',
        pipeline=[ # Pipeline is passed by test_pipeline created before
            dict(type='LoadImageFromFile'),
            dict(
                type='MultiScaleFlipAug',
                img_scale=(1333, 800),
                flip=False,
                transforms=[
                    dict(type='Resize', keep_ratio=True),
                    dict(type='RandomFlip'),
                    dict(
                        type='Normalize',
                        mean=[123.675, 116.28, 103.53],
                        std=[58.395, 57.12, 57.375],
                        to_rgb=True),
                    dict(type='Pad', size=divisor=32),
                    dict(type='ImageToTensor', keys=['img']),
                    dict(type='Collect', keys=['img'])
                ])
            ],
            test=dict( # Test dataset config, modify the ann_file for test-dev/test submission
            type='CocoDataset',
            ann_file='data/coco/annotations/instances_val2017.json',
            img_prefix='data/coco/val2017/',

(continues on next page)