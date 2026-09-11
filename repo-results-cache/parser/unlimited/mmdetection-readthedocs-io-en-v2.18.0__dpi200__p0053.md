MMDetection, Release 2.18.0
(continued from previous page)
-samples min_pos_iou=6.3, # The minimal IoU threshold to take boxes as positive...
-samples match_low_quality=True, # Whether to match the boxes under low quality...
-(see API doc for more details). ignore_lof_thr=1, # IoF threshold for ignoring bboxes sample-dict = Config of positive/negative sampler type="RandomSampler", # Type of sampler, PseudoSampler and other...
-samples are also supported. Refer to https://github.com/open-mllib/mdetection/blob/--master/mmdet/core/bbox/samplers/random_sampler.py#L8 for implementation details.
num=256, # Number of samples
pos_fraction=0.5, # The ratio of positive samples in the total samples.
neg_pos_ub=-1, # The upper bound of negative samples based on the...
-number of positive samples
add_gt_as_proposals=False), # Whether add GT as proposals after...
- allowing_border=-1, # The border allowed after padding for valid anchors.
pos_weight=-1, # The weight of positive samples during training.
debugFalse), # Whether to set the debug mode
rpn_proposaldict of # The config to generate proposals during training
ms_across_levels=False, # Whether to do NMS for boxes across levels. Only...
-work # GAPNMeind = min pos from most support do ms cross levels.
ms_pre=2960, # The number of boxes before NMS
ms_post=1960, # The number of boxes to be kept by NMS. Only work in...
...
GAPNMeind = max_per_img=0, # The number of boxes to be kept after NMS.
msdict(# Config of MS
type='nms', # Type of NMS
iou_threshold=0.7 # NMS threshold
...
min_box_size=0, # The allowed minimal box size
rcm=dict(# The config for the roi heads.
assigner-dict(# Config of assigner for second stage, this is different for...
-that in rpm
type='MaxIoUAssigner', # Type of assigner, MaxIoUAssigner is used for...
- all roi_heads for now. Ref = the https://github.com/open-mlabs/inspection/blob/master/
-mmdet/core/bbox/assigners/max_iou_assigner_pyMI@ for more details.
pos_iou_thr=6.5, # IoU >= threshold 0.5 will be taken as positive.
-samples
neg_iou_thr=0.5, # IoU < threshold 0.5 will be taken as negative samples
-min_pos_iou=0.5, # The minimal IoU threshold to take boxes as positive.
-samples
match_low_quality=False, # Whether to match the boxes under low quality.
-(see API doc for more details.)
ignore_loI_thr=-1) # IoF threshold for ignoring bboxes
sampledict()
-type "RandomSampler", # Type of sampler, PseudoSampler and other.
-samples are also supported. Refer to https://github.com/open-mmlab/mmdetection/blob/
-master/mmdet/core/bbox/samplers/random_sampler.py#L8 for implementation details.
num=512, # Number of samples
pos_fraction=0.25, # The ratio of positive samples in the total samples.
neg_pos_ub=-1, # The upper bound of negative samples based on the.
-number of positive samples.
(continues on next page)
46
Chapter 8. Tutorial 1: Learn about Configs