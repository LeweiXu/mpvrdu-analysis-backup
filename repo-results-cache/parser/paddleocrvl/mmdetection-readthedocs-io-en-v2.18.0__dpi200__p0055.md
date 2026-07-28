(continued from previous page)

dict(
    type='Normalize', # Augmentation pipeline that normalize the input images
    mean=[123.675, 116.28, 103.53], # These keys are the same of img_norm_cfg since
    the
        std=[58.395, 57.12, 57.375], # keys of img_norm_cfg are used here as arguments to_rgb=True),
    dict(
        type='Pad', # Padding config
        size_divisor=32), # The number the padded images should be divisible
        dict(type='DefaultFormatBundle'), # Default format bundle to gather data in the
        -pipeline
        dict(
            type='Collect', # Pipeline that decides which keys in the data should be passed
            to the detector
            keys=['img', 'gt_bboxes', 'gt_labels', 'gt_masks'])
        ]
    test_pipeline = [
        dict(type='LoadImageFromFile'), # First pipeline to load images from file path
        dict(
            type='MultiScaleFlipAug', # An encapsulation that encapsulates the testing
            -augmentations
            img_scale=(1333, 800), # Decides the largest scale for testing, used for the
            -Resize pipeline
            flip=False, # Whether to flip images during testing
            transforms=[
                dict(type='Resize', # Use resize augmentation
                    keep_ratio=True), # Whether to keep the ratio between height and width,
                    the img_scale set here will be suppressed by the img_scale set above.
                    dict(type='RandomFlip'), # Thought RandomFlip is added in pipeline, it is
                    not used because flip=False
                    dict(
                        type='Normalize', # Normalization config, the values are from img_norm_
                    -cfg
                        mean=[123.675, 116.28, 103.53],
                        std=[58.395, 57.12, 57.375],
                        to_rgb=True),
                        dict(
                            type='Pad', # Padding config to pad images divisible by 32.
                            size_divisor=32),
                            dict(
                                type='ImageToTensor', # convert image to tensor
                                keys=['img']),
                            dict(
                                type='Collect', # Collect pipeline that collect necessary keys for
                                -testing.
                                    keys=['img'])
                            ])
        )
    data = dict(
        samples_per_gpu=2, # Batch size of a single GPU
        workers_per_gpu=2, # Worker to pre-fetch data for each single GPU
        train=dict( # Train dataset config

(continues on next page)