# recommended
model = dict(
    type=...,
   ...
    train_cfg=dict(...),
    test_cfg=dict(...),
)

### 8.5 An Example of Mask R-CNN

To help the users have a basic idea of a complete config and the modules in a modern detection system, we make brief comments on the config of Mask R-CNN using ResNet50 and FPN as the following. For more detailed usage and the corresponding alternative for each module, please refer to the API documentation.

model = dict(
    type='MaskRCNN',  # The name of detector
    backbone=dict(  # The config of backbone
        type='ResNet',  # The type of the backbone, refer to https://github.com/open-
        mmlab/mmdetection/blob/master/mmdet/models/backbones/resnet.py#L308 for more details.
        depth=50,  # The depth of backbone, usually it is 50 or 101 for ResNet and
    ).
    num_stages=4,  # Number of stages of the backbone.
    out_indices=(0, 1, 2, 3),  # The index of output feature maps produced in each
    stages
    frozen_stages=1,  # The weights in the first 1 stage are fronzen
    norm_cfg=dict(  # The config of normalization layers.
        type='BN',  # Type of norm layer, usually it is BN or GN
        requires_grad=True),  # Whether to train the gamma and beta in BN
    norm_eval=True,  # Whether to freeze the statistics in BN
    style='pytorch'  # The style of backbone, 'pytorch' means that stride 2 layers.
    are in 3x3 conv, 'caffe' means stride 2 layers are in 1x1 conv.
    init_cfg=dict(type='Pretrained', checkpoint='torchvision://resnet50'),  # The ImageNet pretrained backbone to be loaded
    neck=dict(
        type='FPN',  # The neck of detector is FPN. We also support 'NASFPN', 'PAFPN',
        etc. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/models/necks/
        fpn.py#L10 for more details.
        in_channels=[256, 512, 1024, 2048],  # The input channels, this is consistent
    with the output channels of backbone
    out_channels=256,  # The output channels of each level of the pyramid feature map
    num_outs=5),  # The number of output scales
    rpn_head=dict(
        type='RPNHead',  # The type of RPN head is 'RPNHead', we also support 'GARPNHead', etc. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/models/dense_heads/rpn_head.py#L12 for more details.
        in_channels=256,  # The input channels of each input feature map, this is consistent with the output channels of neck
        feat_channels=256,  # Feature channels of convolutional layers in the head.
        anchor_generator=dict(  # The config of anchor generator
            type='AnchorGenerator',  # Most of methods use AnchorGenerator, SSD.
        )
    )
    Detectors uses 'SSDAnchorGenerator'. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/anchor/anchor_generator.py#L10 for more details.