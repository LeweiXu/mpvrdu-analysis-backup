(continued from previous page)

checkpoint_config = dict(  # Config to set the checkpoint hook, Refer to https://github.com/open-mmlab/mmcv/blob/master/mmcv/runner/hooks/checkpoint.py for implementation.
    interval=1)  # The save interval is 1

log_config = dict(  # config to register logger hook
    interval=50,  # Interval to print the log
    hooks=[
        # dict(type='TensorboardLoggerHook')  # The Tensorboard logger is also supported
        dict(type='TextLoggerHook')
    ])  # The logger used to record the training process.

dist_params = dict(backend='nccl')  # Parameters to setup distributed training, the port can also be set.

log_level = 'INFO'  # The level of logging.

load_from = None  # load models as a pre-trained model from a given path. This will not resume training.

resume_from = None  # Resume checkpoints from a given path, the training will be resumed from the epoch when the checkpoint's is saved.

workflow = [('train', 1)]  # Workflow for runner. [('train', 1)] means there is only one workflow and the workflow named 'train' is executed once. The workflow trains the model by 12 epochs according to the total_epochs.

work_dir = 'work_dir'  # Directory to save the model checkpoints and logs for the current experiments.

### 8.6 FAQ

#### 8.6.1 Ignore some fields in the base config

Sometimes, you may set _delete_=True to ignore some of fields in base config. You may refer to mmcv for simple illustration.

In MMDetection, for example, to change the backbone of Mask R-CNN with the following config.

model = dict(
    type='MaskRCNN',
    pretrained='torchvision://resnet50',
    backbone=dict(
        type='ResNet',
        depth=50,
        num_stages=4,
        out_indices=(0, 1, 2, 3),
        frozen_stages=1,
        norm_cfg=dict(type='BN', requires_grad=True),
        norm_eval=True,
        style='pytorch'),
    neck=dict(...),
    rpn_head=dict(...),
    roi_head=dict(...))

ResNet and HRNet use different keywords to construct.