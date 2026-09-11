MMDetection, Release 2.18.0
(continued from previous page)

use_sigmoid=False,
loss_weight=1.0),
loss_bbox_dict(type='SmoothLoss', beta=1.9, loss_weight=1.0))
],
mask_head_dict(
    type='FCN#masklead',
    num_conv=4,
    in_channels=256,
    conv_out_channels=256,
    # change the number of classes from defaultly COCO to cityscapes
    num_classes=8,
    loss_mask_dict(
    type='CrossEntropyLoss', use_mask=True, loss_weight=1.0))))

# over-write train_pipeline for new added 'AutoAugment' training setting
img_norm_cfg = dict(
    mean([123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], to_rgb=True)
train_pipeline = (
    dict(type='LoadImageFromFile'),
    dict(type='LoadAnnotations', with_bbox=True, with_mask=True),
    dict(
    type='AutoAugment',
    policies=[
    dict(
    type='Rotate',
    levels=[
    img_fill_val=(124, 116, 104),
    prob=0.5,
    scale=1)
    ],
    [dict(type='Rotate', level=7, img_fill_val=(124, 116, 1044)),
    dict(
    type='Translate',
    levels=[,
    prob=0.5,
    img_fill_val=(124, 116, 104))
    ],
    ]),
dict(
    type='Resize', img_scale=[C048, S80), (2048, 1024)], keep_ratio=True),
dict(type='RandomFlip', flip_ratio=0.5),
dict(type='Normalize', "*img_norm_cfg),
dict(type='Pad', size_divisor=32),
dict(type='DefaultFormatBundle'),
dict(type='Collect', keys=['img', 'gt_bboxes', 'gt_labels', 'gt_masks'],
)
# set bstrch_size per gpu, and set new training pipeline
data = dict(
    samples_per_gpu=1,
    workers_per_gpu=3,
    # over-write pipeline with new training pipeline setting
(continues on next page)
7.3. Prepare a config
39