_base_ = '../mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py'
model = dict(
    pretrained='open-mmlab://msra/hrnetv2_w32',
    backbone=dict(
        _delete_=True,
        type='HRNet',
        extra=dict(
            stage1=dict(
                num_modules=1,
                num_branches=1,
                block='BOTTLENECK',
                num_blocks=(4,.),
                num_channels=(64,)),
                stage2=dict(
                    num_modules=1,
                    num_branches=2,
                    block='BASIC',
                    num_blocks=(4,4),
                    num_channels=(32,64)),
                    stage3=dict(
                        num_modules=4,
                        num_branches=3,
                        block='BASIC',
                        num_blocks=(4,4,4),
                        num_channels=(32,64,128)),
                        stage4=dict(
                            num_modules=3,
                            num_branches=4,
                            block='BASIC',
                            num_blocks=(4,4,4,4),
                            num_channels=(32,64,128,256))),
                        neck=dict(...)
                    )
)

The _delete_=True would replace all old keys in backbone field with new keys.

#### 8.6.2 Use intermediate variables in config

Some intermediate variables are used in the config files, like train_pipeline/test_pipeline in datasets. It's worth noting that when modifying intermediate variables in the children config, user need to pass the intermediate variables into corresponding fields again. For example, we would like to use multi scale strategy to train a Mask R-CNN. train_pipeline/test_pipeline are intermediate variable we would like modify.

_base_ = './mask_rcnn_r50_fpn_1x_coco.py'
img_norm_cfg = dict(
    mean=[123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], to_rgb=True)
train_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='LoadAnnotations', with_bbox=True, with_mask=True),
    dict(type='Resize',
        img_scale=[(1333, 640), (1333, 672), (1333, 704), (1333, 736),
                    (1333, 768), (1333, 800)],

(continues on next page)