• multi_scores (Tensor) – shape (n, #class+1), where the last column contains scores of the background class, but this will be ignored.

• multi_coeffs (Tensor) – shape (n, #class*coeffs_dim).

- score_thr (float) – bbox threshold, bboxes with scores lower than it will not be considered.

• iou_thr (float) – IoU threshold to be considered as conflicted.

• top_k(int) – if there are more than top_k bboxes before NMS, only top_k will be kept.

• max_num (int) – if there are more than max_num bboxes after NMS, only top max_num will be kept. If -1, keep all the bboxes. Default: -1.

## Returns

(dets, labels, coefficients), tensors of shape  $ (k, 5) $,  $ (k, 1) $, and  $ (k, \text{coeffs\_dim}) $. Dets are boxes with scores. Labels are 0-based.

Return type tuple

mmdet.core.post_processing.mask_matrix_nms(masks, labels, scores, filter_thr=-1, nms_pre=-1, max_num=-1, kernel='gaussian', sigma=2.0, mask_area=None)

Matrix NMS for multi-class masks.

## Parameters

• masks (Tensor) – Has shape (num_instances, h, w)

• labels (Tensor) – Labels of corresponding masks, has shape (num_instances,).

• scores (Tensor) – Mask scores of corresponding masks, has shape (num_instances).

• filter_thr (float) – Score threshold to filter the masks after matrix nms. Default: -1, which means do not use filter_thr.

• nms_pre (int) – The max number of instances to do the matrix nms. Default: -1, which means do not use nms_pre.

• max_num (int, optional) – If there are more than max_num masks after matrix, only top max_num will be kept. Default: -1, which means do not use max_num.

• kernel (str) – ‘linear’ or ‘gaussian’.

• sigma (float) – std in gaussian method.

• mask_area (Tensor) – The sum of seg_masks.

## Returns

Processed mask results.

• scores (Tensor): Updated scores, has shape  $ (n,) $.

• labels (Tensor): Remained labels, has shape  $ (n,) $.

• masks (Tensor): Remained masks, has shape  $ (n, w, h) $.

• keep_inds (Tensor): The indices number of the remaining mask in the input mask, has shape  $ (n,) $.

Return type tuple(Tensor)

mmdet.core.post_processing.merge_aug_bboxes(aug_bboxes, aug_scores, img_metas, rcnn_test_cfg)

Merge augmented detection bboxes and scores.