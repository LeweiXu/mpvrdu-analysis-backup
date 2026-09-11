MMDetection, Release 2.18.0
(continued from previous page)
roi_head-dict(
    bbox_head([
    dtype='SharedZFCBBoxHead',
    in_channels=256,
    fc_out_channels=1024,
    roi_feat_size=7,
    # change the number of classes from defaultly COCO to cityscapes
    num_classes=8,
    bbox_coder-dict(
    type='DeltaYWHBBoxCoder',
    target_means=[0., 0., 0., 0.],
    target_stds=[0., 1., 0.1, 0.2, 0.2]),
    reg_class_apostropic=True,
    loss_cls=dict(
    type='CrossEntropyLoss',
    use_sigmoid=False,
    loss_weight=1.0),
    loss_block_dict(type='SmoothL1oss', beta=1.0,
    loss_weight=1.0)),
dict(
    type='SharedZFCBookHead',
    in_channels=256,
    fc_out_channels=1924,
    roi_feat_size=7,
    # change the number of classes from defaultly COCO to cityscapes
    num_classes=8,
    bbox_coder_dict(
    type='DeltaXTHWBBoxCoder',
    target_names=[0, 0, 0., 0.],
    target_stds=[0.95, 0.65, 0.1, 0.1]),
    reg_class_agnostic=True,
    loss_cls_dict(
    type='CrossEntropyLoss',
    use_sigmoid=False,
    loss_weight=1.0),
    loss_block_dict(
    type='DeltaXTHWBBoxCoder',
    target_names=[0, 0., 0., 0.],
    target_stds=[0.63, 0.63, 0.867, 0.667]),
    reg_class_agnostic=True,
    loss_cls_dict(
    type='CrossEntropyLoss',
(continues on next page)
38
Chapter 7. 3: Train with customized models and standard datasets