MMDetection, Release 2.18.0
class mmdet.models.roi_heads.SABLHead(num_classes, cls_in_channels=256, reg_in_channels=256, roi_feat_size=7, reg_feat_up_ratio=2, reg_pre_kernel=3, reg_post_kernel=3, reg_pre_num=2, reg_post_num=1, cls_out_channels=1024, reg_offset_out_channels=256, reg_cls_out_channels=256, num_cls_fcs=1, num_reg_fcs=0, reg_class_agnostic=True, norm_cfg=None, bbox_coder={'num_buckets': 14, 'scale_factor': 1.7, 'type': 'BucketingBBoxCoder'}, loss_cls={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': False}, loss_bbox_cls={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_bbox_reg={'beta': 0.1, 'loss_weight': 1.0, 'type': 'SmoothL1Loss'}, init_cfg=None)
Side-Aware Boundary Localization (SABL) for RoI-Head.
Side-Aware features are extracted by conv layers with an attention mechanism. Boundary Localization with Bucketing and Bucketing Guided Rescoring are implemented in BucketingBBoxCoder.
Please refer to https://arxiv.org/abs/1912.04260 for more details.
Parameters
- cls_in_channels (int) – Input channels of cls RoI feature. Defaults to 256.
- reg_in_channels (int) – Input channels of reg RoI feature. Defaults to 256.
- roi_feat_size (int) – Size of RoI features. Defaults to 7.
- reg_feat_up_ratio (int) – Upsample ratio of reg features. Defaults to 2.
- reg_pre_kernel (int) – Kernel of 2D conv layers before attention pooling. Defaults to 3.
- reg_post_kernel (int) – Kernel of 1D conv layers after attention pooling. Defaults to 3.
- reg_pre_num (int) – Number of pre convs. Defaults to 2.
- reg_post_num (int) – Number of post convs. Defaults to 1.
- num_classes (int) – Number of classes in dataset. Defaults to 80.
- cls_out_channels (int) – Hidden channels in cls fcs. Defaults to 1024.
- reg_offset_out_channels (int) – Hidden and output channel of reg offset branch. Defaults to 256.
- reg_cls_out_channels (int) – Hidden and output channel of reg cls branch. Defaults to 256.
- num_cls_fcs (int) – Number of fcs for cls branch. Defaults to 1.
- num_reg_fcs (int) – Number of fcs for reg branch.. Defaults to 0.
- reg_class_agnostic(bool) – Class agnostic regression or not. Defaults to True.
- norm_cfg (dict) – Config of norm layers. Defaults to None.
- bbox_coder (dict) – Config of bbox coder. Defaults ‘BucketingBBoxCoder’.
- loss_cls (dict) – Config of classification loss.
- loss_bbox_cls (dict) – Config of classification loss for bbox branch.
- loss_bbox_reg (dict) – Config of regression loss for bbox branch.
- init_cfg(dict or list[dict], optional)-Initialization config dict. Default: None
404
Chapter 39. mmdet.models