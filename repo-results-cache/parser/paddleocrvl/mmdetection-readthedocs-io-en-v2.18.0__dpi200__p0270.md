merge_aug_results(aug_results, img_metas)

Merge augmented detection bboxes and score.

## Parameters

• aug_results (list[list[Tensor]]) – Det_bboxes and det_labels of each image.

• img_metas (list[list[dict]]) – Meta information of each image, e.g., image size, scaling factor, etc.

Returns (bboxes, labels)

Return type tuple

class mmdet.models.detectors.DETR(backbone, bbox_head, train_cfg=None, test_cfg=None,

pretrained=None, init_cfg=None

Implementation of DETR: End-to-End Object Detection with Transformers

forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/analysis_tools/get_flops.py

onnx_export(img, img_metas)

Test function for exporting to ONNX, without test time augmentation.

Parameters

• img (torch.Tensor) – input images.

• img_metas (list[dict]) – List of image information.

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].

Return type tuple[Tensor, Tensor]

class mmdet.models.detectors.DeformableDETR(*args, **kwargs)

class mmdet.models.detectors.FCOS(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of FCOS

class mmdet.models.detectors.FOVEA(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of FoveaBox

class mmdet.models.detectors.FSAF(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of FSAF

class mmdet.models.detectors.FastRCNN(backbone, roi_head, train_cfg, test_cfg, neck=None,

Implementation of Fast R-CNN

forward_test(imgs, img_metas, proposals, **kwargs)

## Parameters

• imgs (List\[Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains all images in the batch.

• img_metas (List[List[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch.