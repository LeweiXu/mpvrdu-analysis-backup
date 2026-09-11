• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet.datasets.pipelines.Collect.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (List[Tensor], optional) – Segmentation masks for each box. This is required to train QueryInst.

• proposals (List $$ Tensor $$ , optional) – override rpn proposals with custom proposals. Use when with_rpn is False.

Returns a dictionary of loss components

Return type dict[str, Tensor]

simple_test(img, img_metas, rescale=False)

Test function without test time augmentation.

## Parameters

• imgs (list[torch.Tensor]) – List of multiple images

• img_metas (list[dict]) – List of image information.

• rescale (bool) – Whether to rescale the results. Defaults to False.

## Returns

BBox results of each image and classes. The outer list corresponds to each image. The inner list corresponds to each class.

Return type list[list[np.ndarray]]

class mmdet.models.detectors.TridentFasterRCNN(backbone, rpn_head, roi_head, train_cfg, test_cfg, neck=None, pretrained=None, init_cfg=None)

Implementation of TridentNet

aug_test(imgs, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

forward_train(img, img_metas, gt_bboxes, gt_labels, **kwargs)

make copies of img and gts to fit multi-branch.

simple_test(img, img_metas, proposals=None, rescale=False)

Test without augmentation.

class mmdet.models.detectors.TwoStageDetector(backbone, neck=None, rpn_head=None, roi_head=None, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Base class for two-stage detectors.

Two-stage detectors typically consisting of a region proposal network and a task-specific regression head.

async async_simple_test(img, img_meta, proposals=None, rescale=False)

Async test without augmentation.