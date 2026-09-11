As well as the components in TwoStageDetector, Panoptic Segmentor has extra semantic_head and panoptic_fusion_head.

forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/get_flops.py

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, gt_semantic_seg=None, proposals=None, **kwargs)

## Parameters

• img (Tensor) – of shape (N, C, H, W) encoding input images. Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

• proposals – override rpn proposals with custom proposals. Use when with_rpn is False.

Returns a dictionary of loss components

Return type dict[str, Tensor]

simple_test(img, img_metas, proposals=None, rescale=False)

Test without Augmentation.

simple_test_mask(x, img_metas, det_bboxes, det_labels, rescale=False)

Simple test for mask head without augmentation.

class mmdet.models.detectors.VFNet(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of `VarifocalNet (VFNet).<https://arxiv.org/abs/2008.13367>`

class mmdet.models.detectors.YOLACT(backbone, neck, bbox_head, segm_head, mask_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of YOLACT

aug_test(imgs, img_metas, rescale=False)

Test with augmentations.

forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/analysis_tools/get_flops.py

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None)

## Parameters