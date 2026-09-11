## Parameters

• dataset (Dataset) – A PyTorch dataset.

- samples_per_gpu (int) – Number of training samples on each GPU, i.e., batch size of each GPU.

• workers_per_gpu (int) – How many subprocesses to use for data loading for each GPU.

• num_gpus (int) – Number of GPUs. Only used in non-distributed training.

• dist (bool) – Distributed training/test or not. Default: True.

• shuffle (bool) – Whether to shuffle the data at every epoch. Default: True.

• runner_type (str) – Type of runner. Default: EpochBasedRunner

• kwargs – any keyword argument to be used to initialize DataLoader

Returns A PyTorch dataloader.

Return type DataLoader

mmdet.datasets.get_loading_pipeline(pipeline)

Only keep loading image and annotations related configuration.

Parameters pipeline (list[dict]) – Data pipeline config.

Returns

The new pipeline list with only keep loading image and annotations related configuration.

Return type list[dict]

## Examples

>>> pipelines = [
...     dict(type='LoadImageFromFile'),
...     dict(type='LoadAnnotations', with_bbox=True),
...     dict(type='Resize', img_scale=(1333, 800), keep_ratio=True),
...     dict(type='RandomFlip', flip_ratio=0.5),
...     dict(type='Normalize', **img_norm_cfg),
...     dict(type='Pad', size_divisor=32),
...     dict(type='DefaultFormatBundle'),
...     dict(type='Collect', keys=['img', 'gt_bboxes', 'gt_labels'])
... ]
>>> expected_pipelines = [
...     dict(type='LoadImageFromFile'),
...     dict(type='LoadAnnotations', with_bbox=True)
... ]
>>> assert expected_pipelines ==... get_loading_pipeline(pipelines)

mmdet.datasets.replace_ImageToTensor(pipelines)

Replace the ImageToTensor transform in a data pipeline to DefaultFormatBundle, which is normally useful in batch inference.

Parameters pipelines (list[dict]) – Data pipeline config.

Returns

The new pipeline list with all ImageToTensor replaced by DefaultFormatBundle.