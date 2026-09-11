MMDetection, Release 2.18.0
- add: img_norm_cfg
- update: img
SeqRescale
- update: gt_semantic_seg
PhotoMetricDistortion
- update: img
Expand
- update: img, gt_bboxes
MiniToRandomCrop
- update: img, gt_bboxes, gt_labels
Corrupt
- update: img
10.1.3 Formatting
ToTensor
- update: specified by keys.
ImageToTensor
- update: specified by keys.
Transpose
- update: specified by keys.
ToDataContainer
- update: specified by fields.
DefaultFormatBundle
- update: img, proposals, gt_bboxes, gt_bboxes_ignore, gt_labels, gt_masks, gt_semantic_seg
Collect
- add: img_meta (the keys of img_meta is specified by meta_keys)
- remove: all other keys except for those specified by keys
10.1.4 Test time augmentation
MultiScaleFlipAug
10.1. Design of Data pipelines
69