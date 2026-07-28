(continued from previous page)

dict(type='Collect', keys=['img', 'gt_bboxes', 'gt_labels'])

test_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='MultiScaleFlipAug', img_scale=(1333, 800), flip=False, transforms=[
        dict(type='Resize', keep_ratio=True),
        dict(type='RandomFlip'),
        dict(type='Normalize', **img_norm_cfg),
        dict(type='Pad', size_divisor=32),
        dict(type='ImageToTensor', keys=['img']),
        dict(type='Collect', keys=['img']),
    ])
]

For each operation, we list the related dict fields that are added/updated/removed.

#### 10.1.1 Data loading

LoadImageFromFile

• add: img, img_shape, ori_shape

LoadAnnotations

• add: gt_bboxes, gt_bboxes_ignore, gt_labels, gt_masks, gt_semantic_seg, bbox_fields, mask_fields LoadProposals

• add: proposals

#### 10.1.2 Pre-processing

Resize

• add: scale, scale_idx, pad_shape, scale_factor, keep_ratio

• update: img, img_shape, *bbox_fields, *mask_fields, *seg_fields

RandomFlip

• add: flip

• update: img, *bbox_fields, *mask_fields, *seg_fields

## Pad

• add: pad fixed size, pad size divisor

• update: img, pad_shape, *mask_fields, *seg_fields

RandomCrop

• update: img, pad_shape, gt_bboxes, gt_labels, gt_masks, *bbox_fields

Normalize