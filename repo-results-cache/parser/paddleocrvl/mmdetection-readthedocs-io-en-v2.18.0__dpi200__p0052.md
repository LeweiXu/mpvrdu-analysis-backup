(continued from previous page)

roi_feat_size=7, # Size of RoI features
num_classes=80, # Number of classes for classification
bbox_coder=dict( # Box coder used in the second stage.
    type='DeltaXYWHBBoxCoder', # Type of box coder. 'DeltaXYWHBBoxCoder' is applied for most of methods.
    target_means=[0.0, 0.0, 0.0, 0.0, 0.0], # Means used to encode and decode box target_stds=[0.1, 0.1, 0.2, 0.2]), # Standard variance for encoding and decoding. It is smaller since the boxes are more accurate. [0.1, 0.1, 0.2, 0.2] is a conventional setting.

reg_class_agnostic=False, # Whether the regression is class agnostic.
loss_cls=dict( # Config of loss function for the classification branch
    type='CrossEntropyLoss', # Type of loss for classification branch, we also support FocalLoss etc.
    use_sigmoid=False, # Whether to use sigmoid.
    loss_weight=1.0), # Loss weight of the classification branch.
    loss_bbox=dict( # Config of loss function for the regression branch.
        type='L1Loss', # Type of loss, we also support many IoU Losses and smooth L1-loss, etc.
    loss_weight=1.0)), # Loss weight of the regression branch.
    mask_roi_extractor=dict( # RoI feature extractor for mask generation.
        type='SingleRoIExtractor', # Type of the RoI feature extractor, most of methods uses SingleRoIExtractor.
    roi_layer=dict( # Config of RoI Layer that extracts features for instance segmentation
        type='ROIAlign', # Type of RoI Layer, DeformRoIPoolingPack and ModulatedDeformRoIPoolingPack are also supported
        output_size=14, # The output size of feature maps.
        sampling_ratio=0), # Sampling ratio when extracting the RoI features.
        out_channels=256, # Output channels of the extracted feature.
        featmap_strides=[4, 8, 16, 32], # Strides of multi-scale feature maps.
        mask_head=dict( # Mask prediction head
            type='FCNMaskHead', # Type of mask head, refer to https://github.com/openmmlab/mmdetection/blob/master/mmdet/models/roi_heads/mask_heads/fcn_mask_head.py#L21
        for implementation details.
        num_convs=4, # Number of convolutional layers in mask head.
        in_channels=256, # Input channels, should be consistent with the output channels of mask roi extractor.
        conv_out_channels=256, # Output channels of the convolutional layer.
        num_classes=80, # Number of class to be segmented.
        loss_mask=dict( # Config of loss function for the mask branch.
            type='CrossEntropyLoss', # Type of loss used for segmentation
            use_mask=True, # Whether to only train the mask in the correct class.
            loss_weight=1.0))) # Loss weight of mask branch.
        train_cfg = dict( # Config of training hyperparameters for rpn and rcnn
            rpn=dict( # Training config of rpn
                assigner=dict( # Config of assigner
                    type='MaxIoUAssigner', # Type of assigner, MaxIoUAssigner is used for many common detectors. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/bbox/assigners/max_iou_assigner.py#L10 for more details.
            pos_iou_thr=0.7, # IoU >= threshold 0.7 will be taken as positive samples
            neg_iou_thr=0.3, # IoU < threshold 0.3 will be taken as negative samples

(continues on next page)