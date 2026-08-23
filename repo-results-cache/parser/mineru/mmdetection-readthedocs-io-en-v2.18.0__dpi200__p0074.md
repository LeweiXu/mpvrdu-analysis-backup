TUTTORIAL 3: CUSTOMIZE DATA PIPELINES
10.1 Design of Data pipelines
Following typical conventions, we use Dataset and DataLoader for data loading with multiple workers. Dataset
returns a dict of data items corresponding the arguments of models' forward method. Since the data in object detection
may not be the same size (image size, gt bbox size, etc.), we introduce a new DataContainer type in MMCV to help
collect and distribute data of different size. See here for more details.
The data preparation pipeline and the dataset is decomposed. Usually a dataset defines how to process the annotations
and a data pipeline defines all the steps to prepare a data dict. A pipeline consists of a sequence of operations. Each
operation takes a dict as input and also output a dict for the next transform.
We present a classical pipeline in the following figure. The blue blocks are pipeline operations. With the pipeline going
on, each operator can add new keys (marked as green) to the result dict or update the existing keys (marked as orange).
LoadImageFromFile
LoadAnnotations
Resize
RandomFlip
Normalize
Pad
DefaultFormat
Bundle
Collect
{ img:
img_shape:
'ori_shape':
'gt_shape':
'gt_bboxes':
'gt_labels':
'bbox_fields':
} { img:
img_shape:
'ori_shape':
'pad_shape':
'gt_bboxes':
'gt_labels':
'bbox_fields':
'scale':
'scale_xd':
'scale_yd':
'scale_zd':
'keep_ratio':
} { img:
img_shape:
'ori_shape':
'pad_shape':
'gt_bboxes':
'gt_labels':
'bbox_fields':
'scale':
'scale_xd':
'scale_yd':
'scale_zd':
'keep_ratio':
'flip':
'img_norm_cfg':
'scale_xd':
'scale_yd':
'keep_ratio':
'flip':
'img_norm_cfg':
'pad_size':
'pad_size_divisor':
} { img:
img_shape:
'ori_shape':
'pad_shape':
'gt_bboxes':
'gt_labels':
} pipeline
figure
The operations are categorized into data loading, pre-processing, formatting and test-time augmentation.
Here is a pipeline example for Faster R-CNN.
img_norm_cfg = dict(
mean=[123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], torgb=True)
trainpipeline = [
dict(type='LoadImageFromFile'),
dict(type='LoadAnnotations', with_bbox=True),
dict(type='Resize', img_scale=(1333, 800), keep_ratio=True),
dict(type='RandomFlip', flip_ratio=0.5),
dict(type='Normalize', '*img_norm_cfg'),
dict(type='Pad', size_divisor=32),
dict(type='DefaultFormatBundle'),
(continues on next page)