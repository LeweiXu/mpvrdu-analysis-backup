get_targets(gt_bboxes, gt_labels, feat_shape, img_shape, with_corner_emb=False,

with_guiding_shift=False, with_centripetal_shift=False)

Generate corner targets.

Including corner heatmap, corner offset.

Optional: corner embedding, corner guiding shift, centripetal shift.

For CornerNet, we generate corner heatmap, corner offset and corner embedding from this function.

For CentripetalNet, we generate corner heatmap, corner offset, guiding shift and centripetal shift from this function.

## Parameters

- gt_bboxes (list[Tensor]) – Ground truth bboxes of each image, each has shape (num_gt, 4).

• gt_labels (list[Tensor]) – Ground truth labels of each box, each has shape (num_gt,).

• feat_shape (list[int]) – Shape of output feature, [batch, channel, height, width].

• img_shape (list[int]) – Shape of input image, [height, width, channel].

• with_corner_emb (bool) – Generate corner embedding target or not. Default: False.

• with_guiding_shift (bool) – Generate guiding shift target or not. Default: False.

• with_centripetal_shift (bool) – Generate centripetal shift target or not. Default: False.

## Returns

Ground truth of corner heatmap, corner offset, corner embedding, guiding shift and centripetal shift. Containing the following keys:

• topleft_heatmap (Tensor): Ground truth top-left corner heatmap.

• bottomright_heatmap (Tensor): Ground truth bottom-right corner heatmap.

• topleft_offset (Tensor): Ground truth top-left corner offset.

• bottomright_offset (Tensor): Ground truth bottom-right corner offset.

• corner_embedding (list[list[list[int]]]): Ground truth corner embedding. Not must have.

• topleft_guiding_shift (Tensor): Ground truth top-left corner guiding shift. Not must have.

• bottomright_guiding_shift (Tensor): Ground truth bottom-right corner guiding shift. Not must have.

• topleft_centripetal_shift (Tensor): Ground truth top-left corner centripetal shift. Not must have.

• bottomright_centripetal_shift (Tensor): Ground truth bottom-right corner centripetal shift. Not must have.

## Return type dict

## init_weights()

Initialize the weights.

loss(tl_heats, br_heats, tl_embs, br_embs, tl_offs, br_offs, gt_bboxes, gt_labels, img_metas,

gt_bboxes_ignore=None)

Compute losses of the head.

Parameters