• proposals (List[List[Tensor]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch. The Tensor should have a shape Px4, where P is the number of proposals.

class mmdet.models.detectors.FasterRCNN(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None, pretrained=None, init_cfg=None)

Implementation of Faster R-CNN

class mmdet.models.detectors.GFL(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

class mmdet.models.detectors.GridRCNN(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None, pretrained=None, init_cfg=None)

Grid R-CNN.

This detector is the implementation of: - Grid R-CNN (https://arxiv.org/abs/1811.12030) - Grid R-CNN Plus: Faster and Better (https://arxiv.org/abs/1906.05688)

class mmdet.models.detectors.HybridTaskCascade(**kwargs)

Implementation of HTC

property with_semantic

whether the detector has a semantic head

Type bool

class mmdet.models.detectors.KnowledgeDistillationSingleStageDetector(backbone, neck,

(backbone, neck,

 $  \text{bbox\_head},  $

 $  \text{teacher\_config},  $

 $  \text{teacher\_ckpt}=\text{None},  $

 $  \text{eval\_teacher}=\text{True},  $

 $  \text{train\_cfg}=\text{None},  $

 $  \text{test\_cfg}=\text{None},  $

 $  \text{pretrained}=\text{None}  $

Implementation of Distilling the Knowledge in a Neural Network..

## Parameters

• teacher_config (str / dict) – Config file path or the config object of teacher model.

• teacher_ckpt(str, optional) – Checkpoint path of teacher model. If left as None, the model will not load any weights.

cuda(device=None)

Since teacher_model is registered as a plain object, it is necessary to put the teacher model to cuda when calling cuda function.

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None)

## Parameters

• img (Tensor) – Input images of shape (N, C, H, W). Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – A List of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet.datasets.pipelines.Collect.

- gt_bboxes (list[Tensor]) – Each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.