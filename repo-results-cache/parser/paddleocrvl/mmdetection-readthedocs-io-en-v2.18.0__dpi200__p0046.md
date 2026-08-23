(continued from previous page)

use_sigmoid=False,
loss_weight=1.0,
loss_bbox=dict(type='SmoothL1Loss', beta=1.0, loss_weight=1.0))
],
mask_head=dict(
    type='FCNMaskHead',
    num_convs=4,
    in_channels=256,
    conv_out_channels=256,
    # change the number of classes from defaultly COCO to cityscapes
    num_classes=8,
    loss_mask=dict(
        type='CrossEntropyLoss', use_mask=True, loss_weight=1.0))))

# over-write 'train_pipeline' for new added 'AutoAugment' training setting
img_norm_cfg = dict(
    mean=[123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], to_rgb=True)
train_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='LoadAnnotations', with_bbox=True, with_mask=True),
    dict(type='AutoAugment', policies=[
        [dict(type='Rotate', level=5, img_fill_val=(124, 116, 104), prob=0.5, scale=1)
        ],
        [dict(type='Rotate', level=7, img_fill_val=(124, 116, 104)), dict(type='Translate', level=5, prob=0.5, img_fill_val=(124, 116, 104))
    ],
])

dict(
    type='Resize', img_scale=[(2048, 800), (2048, 1024)], keep_ratio=True,
    dict(type='RandomFlip', flip_ratio=0.5),
    dict(type='Normalize', **img_norm_cfg),
    dict(type='Pad', size_divisor=32),
    dict(type='DefaultFormatBundle'),
    dict(type='Collect', keys=['img', 'gt_bboxes', 'gt_labels', 'gt_masks'])
])

# set batch_size per gpu, and set new training pipeline
data = dict(
    samples_per_gpu=1,
    workers_per_gpu=3,
    # over-write 'pipeline' with new training pipeline setting

(continues on next page)

#### 7.3. Prepare a config