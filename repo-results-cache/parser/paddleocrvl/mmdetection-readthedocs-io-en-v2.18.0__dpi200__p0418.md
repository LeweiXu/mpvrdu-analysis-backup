forward_dummy(x, proposals)

Dummy forward function.

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, **kwargs)

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposals (list [Tensors]) – list of region proposals.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

## init_assigner_sampler()

Initialize assigner and sampler.

init_bbox_head(bbox_roi_extractor, bbox_head)

Initialize bbox_head

init_mask_head(mask_roi_extractor, mask_head)

Initialize mask_head

mask_onnx_export(x, img_metas, det_bboxes, det_labels, **kwargs)

Export mask branch to onnx which supports batch inference.

Parameters

• x (tuple[Tensor]) – Feature maps of all scale level.

• img_metas (list[dict]) – Image meta info.

• det_bboxes (Tensor) – Bboxes and corresponding scores. has shape [N, num_bboxes, 5].

• det_labels (Tensor) – class labels of shape [N, num_bboxes].

## Returns

The segmentation results of shape [N, num_bboxes, image_height, image_width].

Return type Tensor

onnx_export(x, proposals, img_metas, rescale=False)

Test without augmentation.