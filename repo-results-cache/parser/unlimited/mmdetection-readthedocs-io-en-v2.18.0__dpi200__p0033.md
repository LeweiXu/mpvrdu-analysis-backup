MMDetection, Release 2.18.0
(continued from previous page)
# manually replace ImageToTensor to DefaultFormatBundle (recommended)
pipelines = [
    dict(type='loadImageFromFile'),
    dict(
    type='MultiScaleFlipAug',
    img_scale=(1333, 896),
    flip=False,
    transforms=[
    dict(type='Resize', keep_ratio=True),
    dict(type='RandomFlip'),
    dict(type='Normalize', mean=[0, 0, 0], std=[1, 1, 1]),
    dict(type='Pad', size_divisor=32),
    dict(type='DefaultFormatBundle'),
    dict(type='Collect', keys=['img'],
    ])
]
5.3 Train predefined models on standard datasets
MMDetection also provides out-of-the-box tools for training detection models. This section will show how to train predefined models (under configs) on standard datasets i.e. COCO.
Important: The default learning rate in config files is for 8 GPUs and 2 img/pqu (batch size = 8*2 = 16). According to the linear scaling rule, you need to set the learning rate proportional to the batch size if you use different GPUs or images per GPU, e.g., lr=0.01 for 4 GPUs * 2 img/squ and lr=0.05 for 16 GPUs * 4 img/squ.
5.3.1 Prepare datasets
Training requires preparing datasets too. See section Prepare datasets above for details.
Note: Currently, the config files under configs/cityscapes use COCO pretrained weights to initialize. You could download the existing models in advance if the network connection is unavailable or slow. Otherwise, it would cause errors at the beginning of training.
5.3.2 Training on a single GPU
We provide tools/train.py to launch training jobs on a single GPU. The basic usage is as follows.
python tools/train.py \
#CONFIG_HASH \
[optional arguments]
During training, log files and checkpoints will be saved to the working directory, which is specified by work_dir in the config file or via CLI argument --work-dir.
By default, the model is evaluated on the validation set every epoch, the evaluation interval can be specified in the config file as shown below.
# evaluate the model every 12 epoch.
evaluation = dict(interval=12)
26
Chapter 5. 1: Inference and train with existing models and standard datasets