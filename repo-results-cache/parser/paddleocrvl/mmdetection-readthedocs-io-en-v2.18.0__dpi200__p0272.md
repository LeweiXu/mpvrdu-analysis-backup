• gt_labels (list[Tensor]) – Class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – Specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

train(mode=True)

Set the same train mode for teacher and student model.

class mmdet.models.detectors.MaskRCNN(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None, pretrained=None, init_cfg=None)

Implementation of Mask R-CNN

class mmdet.models.detectors.MaskScoringRCNN(backbone, rpn_head, roi_head, train_cfg, test_cfg,

 $$ neck=None,pretrained=None,init\_{c}fg=None) $$ 

Mask Scoring RCNN.

https://arxiv.org/abs/1903.00241

class mmdet.models.detectors.NASFCOS(backbone, neck, bbox_head, train_cfg=None, test_cfg=None,

pretrained=None, init_cfg=None)

NAS-FCOS: Fast Neural Architecture Search for Object Detection.

https://arxiv.org/abs/1906.0442

class mmdet.models.detectors.PAA(backbone, neck, bbox_head, train_cfg=None, test_cfg=None,

pretrained=None, init_cfg=None

Implementation of PAA.

class mmdet.models.detectors.PanopticFPN(backbone, neck=None, rpn_head=None, roi_head=None,

train_cfg=None, test_cfg=None, pretrained=None,

init_cfg=None, semantic_head=None,

panoptic fusion head=None)

Implementation of Panoptic feature pyramid networks

class mmdet.models.detectors.PointRend(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None,

pretrained=None, init_cfg=None)

PointRend: Image Segmentation as Rendering

This detector is the implementation of PointRend.

class mmdet.models.detectors.QueryInst(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None, pretrained=None, init_cfg=None)

Implementation of Instances as Queries

class mmdet.models.detectors.RPN(backbone, neck, rpn_head, train_cfg, test_cfg, pretrained=None,

Implementation of Region Proposal Network.

aug_test(imgs, img_metas, rescale=False)

Test function with test time augmentation.

Parameters

• imgs (list[torch.Tensor]) – List of multiple images

• img_metas (list[dict]) – List of image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

Returns proposals