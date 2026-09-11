${CHECKPOINT_FILE} \
${GPU_NUM} \
--format-only \
--options ${JSONFILE_PREFIX} \
[--show]

(continued from previous page)

Assuming that the checkpoints in the model zoo have been downloaded to the directory checkpoints/, we can test Mask R-CNN on COCO test-dev with 8 GPUs, and generate JSON files using the following command.

./tools/dist_test.sh \
configs/mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py \
checkpoints/mask_rcnn_r50_fpn_1x_coco_20200205-d4b0c5d6.pth \
8 \
--format-only \
--options "jsonfile_prefix=.mask_rcnn_test-dev_results"

This command generates two JSON files mask_rcnn_test-dev_results.bbox.json and mask_rcnn_test-dev_results.segm.json.

#### 5.2.5 Batch Inference

MMDetection supports inference with a single image or batched images in test mode. By default, we use single-image inference and you can use batch inference by modifying samples_per_gpu in the config of test data. You can do that either by modifying the config as below.

data = dict(train=dict(...), val=dict(...), test=dict(samples_per_gpu=2,...)

Or you can set it through --cfg-options as --cfg-options data.test.samples_per_gpu=2

#### 5.2.6 Deprecated ImageToTensor

In test mode, ImageToTensor pipeline is deprecated, it’s replaced by DefaultFormatBundle that recommended to manually replace it in the test data pipeline in your config file. examples:

# use ImageToTensor (deprecated)

pipelines = [
    dict(type='LoadImageFromFile'),
    dict(
        type='MultiScaleFlipAug',
        img_scale=(1333, 800),
        flip=False,
        transforms=[
            dict(type='Resize', keep_ratio=True),
            dict(type='RandomFlip'),
            dict(type='Normalize', mean=[0, 0, 0], std=[1, 1, 1]),
            dict(type='Pad', size_divisor=32),
            dict(type='ImageToTensor', keys=['img']),
            dict(type='Collect', keys=['img']),
        ])
    ]
]

(continues on next page)