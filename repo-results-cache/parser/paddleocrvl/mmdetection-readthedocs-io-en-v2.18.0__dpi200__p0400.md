class mmdet.models.roi_heads.DynamicRoIHead(**kwargs)

RoI head for Dynamic R-CNN.

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None)

Forward function for training.

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposals (list [Tensors]) – list of region proposals.

- gt_bboxes (list[Tensor]) – each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

## update_hyperparameters()

Update hyperparameters like IoU thresholds for assigner and beta for SmoothL1 loss based on the training statistics.

Returns the updated iou_thr and beta.

Return type tuple[float]

class mmdet.models.roi_heads.FCNMaskHead(num_convs=4, roi_feat_size=14, in_channels=256)

(num_convs=4, roi_feat_size=14, in_channels=256, conv_kernel_size=3, conv_out_channels=256, num_classes=80, class_agnostic=False, upsample_cfg='scale_factor': 2, 'type': 'deconv'),
conv_cfg=None, norm_cfg=None, predictor_cfg='type': 'Conv'},
loss_mask='loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_mask': True, init_cfg=None)

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

get_seg_masks(mask_pred, det_bboxes, det_labels, rcnn_test_cfg, ori_shape, scale_factor, rescale)

Get segmentation masks from mask_pred and bboxes.