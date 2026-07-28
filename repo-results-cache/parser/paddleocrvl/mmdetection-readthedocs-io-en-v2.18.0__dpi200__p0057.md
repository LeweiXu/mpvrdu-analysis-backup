(continued from previous page)

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
samples_per_gpu=2  # Batch size of a single GPU used in testing
))
evaluation = dict(  # The config to build the evaluation hook, refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/evaluation/eval_hooks.py#L7 for more details.
    interval=1,  # Evaluation interval
    metric=['bbox','segm']  # Metrics used during evaluation
    optimizer = dict(  # Config used to build optimizer, support all the optimizers in
        PyTorch whose arguments are also the same as those in PyTorch
        type='SGD',  # Type of optimizers, refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/optimizer/default_constructor.py#L13 for more details
    lr=0.02,  # Learning rate of optimizers, see detail usages of the parameters in the documentation of PyTorch
    momentum=0.9,  # Momentum
    weight_decay=0.0001)  # Weight decay of SGD
    optimizer_config = dict(  # Config used to build the optimizer hook, refer to https://github.com/open-mmlab/mmcv/blob/master/mmcv/runner/hooks/optimizer.py#L8 for implementation details.
    grad_clip=None)  # Most of the methods do not use gradient clip
    lr_config = dict(  # Learning rate scheduler config used to register lrUp日前 hook policy='step',  # The policy of scheduler, also support CosineAnnealing, Cyclic, etc.
    refer to details of supported lrUp日前 from https://github.com/open-mmlab/mmcv/blob/master/mmcv/runner/hooks/lr_update.py#L9.
    warmup='linear',  # The warmup policy, also support exp and constant
    warmup_iters=500,  # The number of iterations for warmup
    warmup_ratio=0.001,  # The ratio of the starting learning rate used for warmup
    step=[8, 11])  # Steps to decay the learning rate

runner = dict(
    type='EpochBasedRunner',  # Type of runner to use (i.e. IterBasedRunner or
    EpochBasedRunner)
    max_epochs=12)  # Runner that runs the workflow in total max_epochs. For
    IterBasedRunner use max_iters
)