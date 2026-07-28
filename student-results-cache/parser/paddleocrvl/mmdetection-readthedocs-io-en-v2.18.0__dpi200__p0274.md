### Return type list[np.ndarray]

class mmdet.models.detectors.RepPointsDetector(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

RepPoints: Point Set Representation for Object Detection.

This detector is the implementation of: - RepPoints detector (https://arxiv.org/pdf/1904.11490)

class mmdet.models.detectors.RetinaNet(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of RetinaNet

##### class mmdet.models.detectors.SCNet(**kwargs)

Implementation of SCNet

class mmdet.models.detectors.SOLO(backbone, neck=None, bbox_head=None, mask_head=None, train_cfg=None, test_cfg=None, init_cfg=None, pretrained=None)

SOLO: Segmenting Objects by Locations

class mmdet.models.detectors.SingleStageDetector(backbone, neck=None, bbox_head=None, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Base class for single-stage detectors.

Single-stage detectors directly and densely predict bounding boxes on the output features of the backbone+neck.

## aug_test(imgs, img_metas, rescale=False)

Test function with test time augmentation.

## Parameters

• imgs (list\[Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains all images in the batch.

• img_metas (list[list[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch. each dict has image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

## Returns

BBox results of each image and classes. The outer list corresponds to each image. The inner list corresponds to each class.

Return type list[list[np.ndarray]]

## extract_feat(img)

Directly extract features from the backbone+neck.

## forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/analysis_tools/get_flops.py

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None)

## Parameters

• img (Tensor) – Input images of shape (N, C, H, W). Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – A List of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and