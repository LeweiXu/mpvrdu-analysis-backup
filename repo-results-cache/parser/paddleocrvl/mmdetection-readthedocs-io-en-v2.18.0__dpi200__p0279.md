• img (Tensor) – of shape (N, C, H, W) encoding input images. Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

simple_test(img, img_metas, rescale=False)

Test function without test-time augmentation.

class mmdet.models.detectors.YOLOF(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None)

Implementation of You Only Look One-level Feature

class mmdet.models.detectors.YOLOV3(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

onnx_export(img, img_metas)

Test function for exporting to ONNX, without test time augmentation.

## Parameters

• img (torch.Tensor) – input images.

• img_metas (list[dict]) – List of image information.

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].

Return type tuple[Tensor, Tensor]

class mmdet.models.detectors.YOLOX(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of YOLOX: Exceeding YOLO Series in 2021