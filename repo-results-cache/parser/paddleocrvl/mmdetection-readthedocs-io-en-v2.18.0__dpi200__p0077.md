### 10.2 Extend and use custom pipelines

1. Write a new pipeline in a file, e.g., in my_pipeline.py. It takes a dict as input and returns a dict.

import random
from mmdet.datasets import PIPELINES
@PIPELINES.register_module()
class MyTransform:
    """Add your transform

    Args:
        p (float): Probability of shifts. Default 0.5.
        """
    def __init__(self, p=0.5):
        self.p = p

    def __call__(self, results):
        if random.random() > self.p:
            results['dummy'] = True
        return results

2. Import and use the pipeline in your config file. Make sure the import is relative to where your train script is located.

custom_imports = dict(imports=['path.to.my_pipeline'], allow_failed_imports=False)
img_norm_cfg = dict(
    mean=[123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], to_rgb=True)
train_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='LoadAnnotations', with_bbox=True),
    dict(type='Resize', img_scale=(1333, 800), keep_ratio=True),
    dict(type='RandomFlip', flip_ratio=0.5),
    dict(type='Normalize', **img_norm_cfg),
    dict(type='Pad', size_divisor=32),
    dict(type='MyTransform', p=0.2),
    dict(type='DefaultFormatBundle'),
    dict(type='Collect', keys=['img', 'gt_bboxes', 'gt_labels']),
]

### 3. Visualize the output of your augmentation pipeline

To visualize the output of your agmentation pipeline, tools/misc/browse_dataset.py can help the user to browse a detection dataset (both images and bounding box annotations) visually, or save the image to a designated directory. More details can refer to useful_tools