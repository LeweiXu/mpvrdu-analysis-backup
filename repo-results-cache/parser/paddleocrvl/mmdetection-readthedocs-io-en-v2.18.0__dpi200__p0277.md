aug_test(imgs, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

extract_feat(img)

Directly extract features from the backbone+neck.

forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/analysis_tools/get_flops.py

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, proposals=None, **kwargs)

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

Test without augmentation.

property with_roi_head

whether the detector has a RoI head

Type bool

property with_rpn

whether the detector has RPN

Type bool

class mmdet.models.detectors.TwoStagePanopticSegmentor(backbone, neck=None, rpn_head=None, roi_head=None, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None, semantic_head=None, panoptic_fusion_head=None)

Base class of Two-stage Panoptic Segmentor.