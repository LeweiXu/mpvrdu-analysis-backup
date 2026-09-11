loss(point_pred, point_targets, labels)

Calculate loss for MaskPointHead.

## Parameters

• point_pred (Tensor) – Point prediction result, shape (num_rois, num_classes, num_points).

• point targets (Tensor) – Point targets, shape (num_roi, num_points).

• labels (Tensor) – Class label of corresponding boxes, shape (num_rois,)

Returns a dictionary of point loss components

Return type dict[str, Tensor]

class mmdet.models.roi_heads.MaskScoringRoIHead(mask_iou_head, **kwargs)

Mask Scoring RoIHead for Mask Scoring RCNN.

https://arxiv.org/abs/1903.00241

simple_test_mask(x, img_metas, det_bboxes, det_labels, rescale=False)

Obtain mask prediction without augmentation.

class mmdet.models.roi_heads.PISARoIHead(bbox_roi_extractor=None, bbox_head=None, mask_roi_extractor=None, mask_head=None, shared_head=None, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

The RoI head for Prime Sample Attention in Object Detection.

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None,

gt_masks=None)

Forward function for training.

## Parameters

• x (list[Tensor]) – List of multi-level img features.

• img_metas (list[dict]) – List of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposals (list [Tensors]) – List of region proposals.

- gt_bboxes (list [Tensor]) – Each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – Class indices corresponding to each box

- gt_bboxes_ignore (list[Tensor], optional) – Specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – True segmentation masks for each box used if the architecture supports a segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

class mmdet.models.roi_heads.PointRendRoIHead(point_head, *args, **kwargs)

PointRend.

aug_test_mask(feats, img_metas, det_bboxes, det_labels)

Test for mask head with test time augmentation.