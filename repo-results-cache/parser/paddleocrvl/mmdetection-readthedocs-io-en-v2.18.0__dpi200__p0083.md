custom_imports=dict(
    imports=['mmdet.models.roi_heads.double_roi_head','mmdet.models.bbox_heads.double_bbox_head'])
)

to the config file and achieve the same goal.

The config file of Double Head R-CNN is as the following

_base_ = '../faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py'
model = dict(
    roi_head=dict(
        type='DoubleHeadRoIHead',
        reg_roi_scale_factor=1.3,
        bbox_head=dict(
            _delete_=True,
            type='DoubleConvFCBBoxHead',
            num_convs=4,
            num_fcs=2,
            in_channels=256,
            conv_out_channels=1024,
            fc_out_channels=1024,
            roi_feat_size=7,
            num_classes=80,
            bbox_coder=dict(
                type='DeltaXYWHBBoxCoder',
                target_means=[0., 0., 0., 0.],
                target_stds=[0.1, 0.1, 0.2, 0.2]),
                reg_class_agnostic=False,
                loss_cls=dict(
                    type='CrossEntropyLoss', use_sigmoid=False, loss_weight=2.0),
                    loss_bbox=dict(type='SmoothL1Loss', beta=1.0, loss_weight=2.0)))
            )
        )
)

Since MMDetection 2.0, the config system supports to inherit configs such that the users can focus on the modification. The Double Head R-CNN mainly uses a new DoubleHeadRoIHead and a new DoubleConvFCBBoxHead, the arguments are set according to the __init__ function of each module.

#### 11.1.4 Add new loss

Assume you want to add a new loss as MyLoss, for bounding box regression. To add a new loss function, the users need to implement it in mmdet/models/losses/my_loss.py. The decorator weighted_loss enables the loss to be weighted for each element.

import torch
import torch.nn as nn
from..builder import LOSSES
from..utils import weighted_loss
@weighted_loss
def my_loss(pred, target):
    assert pred.size() == target.size() and target.numel() > 0
    loss = torch.abs(pred - target)
    return loss

(continues on next page)