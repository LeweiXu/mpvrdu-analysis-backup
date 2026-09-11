min_pos_iou=0.3, # The minimal IoU threshold to take boxes as positive_samples
match_low_quality=True, # Whether to match the boxes under low quality
(see API doc for more details).
ignore_iof_thr=-1, # IoF threshold for ignoring bboxes
sampler=dict( # Config of positive/negative sampler
    type='RandomSampler', # Type of sampler, PseudoSampler and other_
    samplers are also supported. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/bbox/samplers/random_sampler.py#L8 for implementation details.
    num=256, # Number of samples
    pos_fraction=0.5, # The ratio of positive samples in the total samples.
    neg_pos_ub=-1, # The upper bound of negative samples based on the_
    number of positive samples.
    add_gt_as_proposals=False), # Whether add GT as proposals after_
    sampling.
    allowed_border=-1, # The border allowed after padding for valid anchors.
    pos_weight=-1, # The weight of positive samples during training.
    debug=False), # Whether to set the debug mode
    rpn_proposal=dict( # The config to generate proposals during training
        nms_across_levels=False, # Whether to do NMS for boxes across levels. Only_
    work in 'GARPNHead', naive rpn does not support do nms cross levels.
    nms_pre=2000, # The number of boxes before NMS
    nms_post=1000, # The number of boxes to be kept by NMS, Only work in_
    GARPNHead.
    max_per_img=1000, # The number of boxes to be kept after NMS.
    nms=dict(# Config of NMS
        type='nms', # Type of NMS
        iou_threshold=0.7 # NMS threshold
    ),
    min_bbox_size=0), # The allowed minimal box size
    rcnn=dict(# The config for the roi heads.
    assigner=dict( # Config of assigner for second stage, this is different for_
    that in rpn
        type='MaxIoUAssigner', # Type of assigner, MaxIoUAssigner is used for_
    all roi_heads for now. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/bbox/assigners/max_iou_assigner.py#L10 for more details.
    pos_iou_thr=0.5, # IoU >= threshold 0.5 will be taken as positive_
    samples
        neg_iou_thr=0.5, # IoU < threshold 0.5 will be taken as negative samples
        min_pos_iou=0.5, # The minimal IoU threshold to take boxes as positive_
    samples
        match_low_quality=False, # Whether to match the boxes under low quality
    (see API doc for more details).
    ignore_iof_thr=-1), # IoF threshold for ignoring bboxes
    sampler=dict(
        type='RandomSampler', # Type of sampler, PseudoSampler and other_
    samplers are also supported. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/core/bbox/samplers/random_sampler.py#L8 for implementation details.
    num=512, # Number of samples
    pos_fraction=0.25, # The ratio of positive samples in the total samples.
    neg_pos_ub=-1, # The upper bound of negative samples based on the_
    number of positive samples.

(continues on next page)