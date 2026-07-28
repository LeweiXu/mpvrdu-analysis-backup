(continued from previous page)

add_gt_as_proposals=True
), # Whether add GT as proposals after sampling.
mask_size=28, # Size of mask
pos_weight=-1, # The weight of positive samples during training.
debug=False) # Whether to set the debug mode
test_cfg = dict( # Config for testing hyperparameters for rpn and rcnn
    rpn=dict( # The config to generate proposals during testing
        nms_across_levels=False, # Whether to do NMS for boxes across levels. Only_work in 'GARPNHead', naive rpn does not support do nms cross levels.
    nms_pre=1000, # The number of boxes before NMS
    nms_post=1000, # The number of boxes to be kept by NMS, Only work in 'GARPNHead'.
    max_per_img=1000, # The number of boxes to be kept after NMS.
    nms=dict( # Config of NMS
        type='nms', # Type of NMS
        iou_threshold=0.7 # NMS threshold
    ),
    min_bbox_size=0), # The allowed minimal box size

rcnn=dict( # The config for the roi heads.
    score_thr=0.05, # Threshold to filter out boxes
    nms=dict( # Config of NMS in the second stage
        type='nms', # Type of NMS
        iou_thr=0.5), # NMS threshold
    max_per_img=100, # Max number of detections of each image
    mask_thr_binary=0.5)) # Threshold of mask prediction

dataset_type = 'CocoDataset' # Dataset type, this will be used to define the dataset
data_root = 'data/coco/' # Root path of data
img_norm_cfg = dict( # Image normalization config to normalize the input images
    mean=[123.675, 116.28, 103.53], # Mean values used to pre-training the pre-trained backbone models

std=[58.395, 57.12, 57.375], # Standard variance used to pre-training the pre-trained backbone models

to_rgb=True
) # The channel orders of image used to pre-training the pre-trained backbone models
train_pipeline = [ # Training pipeline
    dict(type='LoadImageFromFile'), # First pipeline to load images from file path
    dict(
        type='LoadAnnotations', # Second pipeline to load annotations for current image with_bbox=True, # Whether to use bounding box, True for detection
        with_mask=True, # Whether to use instance mask, True for instance segmentation
        poly2mask=False), # Whether to convert the polygon mask to instance mask, set_False for acceleration and to save memory
    dict(
        type='Resize', # Augmentation pipeline that resize the images and their_
    )
    annotations
    img_scale=(1333, 800), # The largest scale of image
    keep_ratio=True
), # whether to keep the ratio between height and width.

dict(
    type='RandomFlip', # Augmentation pipeline that flip the images and their_
    annotations
    flip_ratio=0.5), # The ratio or probability to flip

(continues on next page)