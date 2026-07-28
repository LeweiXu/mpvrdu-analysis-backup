## Parameters

• aug_bboxes (list[Tensor]) – shape (n, 4*#class)

• aug_scores (list[Tensor] or None) – shape (n, #class)

• img shapes (list [Tensor]) – shape (3, ).

• rcnn_test_cfg(dict) – rcnn test config.

Returns (bboxes, scores)

Return type tuple

mmdet.core.post_processing.merge_aug_masks(aug_masks, img_metas, rcnn_test_cfg, weights=None)

Merge augmented mask prediction.

## Parameters

• aug_masks (list[ndarray]) – shape (n, #class, h, w)

• img_shapes (list[ndarray]) – shape (3, ).

• rcnn_test_cfg(dict) – rcnn test config.

Returns (bboxes, scores)

Return type tuple

mmdet.core.post_processing.merge_aug_proposals(aug_proposals, img_metas, cfg)

Merge augmented proposals (multiscale, flip, etc.)

## Parameters

• aug_proposals (list[Tensor]) – proposals from different testing schemes, shape (n, 5). Note that they are not rescaled to the original image size.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• cfg(dict) – rpn test config.

Returns shape  $ (n, 4) $, proposals corresponding to original image scale.

Return type Tensor

mmdet.core.post_processing.merge_aug_scores(aug_scores)

Merge augmented bbox scores.

mmdet.core.post_processing.multiclass_nms(multi_bboxes, multi_scores, score_thr, nms_cfg, max_num=1, score_factors=None, return_inds=False)

NMS for multi-class bboxes.

## Parameters

• multi_bboxes (Tensor) – shape (n, #class*4) or (n, 4)

• multi_scores (Tensor) – shape (n, #class), where the last column contains scores of the background class, but this will be ignored.

• score_thr (float) – bbox threshold, bboxes with scores lower than it will not be considered.

• nms_thr (float) – NMS IoU threshold