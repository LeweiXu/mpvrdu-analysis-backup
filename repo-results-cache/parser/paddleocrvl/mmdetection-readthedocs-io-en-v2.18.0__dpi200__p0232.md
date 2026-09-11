• center_h (Tensor): the center point of the height.

• center_w (Tensor): the center point of the width.

Return type tuple[Tensor]

mmdet.core.utils.filter_scores_and_topk(scores, score_thr, topk, results=None)

Filter results using score threshold and topk candidates.

## Parameters

• scores (Tensor) – The scores, shape (num_bboxes, K).

• score_thr (float) – The score filter threshold.

• topk (int) – The number of topk candidates.

• results (dict or list or Tensor, Optional) – The results to which the filtering rule is to be applied. The shape of each item is (num_bboxes, N).

## Returns

Filtered results

• scores (Tensor): The scores after being filtered, shape (num_bboxes_filtered, ).

• labels (Tensor): The class labels, shape (num_bboxes_filtered, ).

• anchor_idxs (Tensor): The anchor indexes, shape (num_bboxes_filtered, ).

• filtered_results (dict or list or Tensor, Optional): The filtered results. The shape of each item is (num_bboxes_filtered, N).

Return type tuple

mmdet.core.utils.flip_tensor(src_tensor, flip_direction)

flip tensor base on flip_direction.

## Parameters

• src_tensor (Tensor) – input feature map, shape (B, C, H, W).

• flip_direction(str) – The flipping direction. Options are ‘horizontal’, ‘vertical’, ‘diagonal’.

Returns Flipped tensor.

Return type out_tensor (Tensor)

mmdet.core.utils.generate_coordinate(featmap_sizes, device='cuda')

Generate the coordinate.

## Parameters

• featmap_sizes (tuple) – The feature to be calculated, of shape (N, C, W, H).

• device (str) – The device where the feature will be put on.

Returns The coordinate feature, of shape  $ (N, 2, W, H) $.

Return type coord_feat (Tensor)

mmdet.core.utils.mask2ndarray(mask)

Convert Mask to ndarray..

:param mask (BitmapMasks or PolygonMasks or :param torch.Tensor or np.ndarray): The mask to be converted.

Returns Ndarray mask of shape  $ (n, h, w) $ that has been converted