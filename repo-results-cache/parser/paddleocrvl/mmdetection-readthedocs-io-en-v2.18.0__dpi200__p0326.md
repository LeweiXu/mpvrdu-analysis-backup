## forward_single(x, lvl_ind, return_pool=False)

Forward feature of a single level.

## Parameters

• x (Tensor) – Feature of a single level.

• lvl_ind(int) – Level index of current feature.

• return_pool (bool) – Return corner pool feature or not.

## Returns

A tuple of CornerHead’s output for current feature level. Containing the following Tensors:

• tl_heat (Tensor): Predicted top-left corner heatmap.

• br_heat (Tensor): Predicted bottom-right corner heatmap.

• tl_emb (Tensor | None): Predicted top-left embedding heatmap. None for self.with_corner_emb == False.

• br_emb (Tensor | None): Predicted bottom-right embedding heatmap. None for self.with_corner_emb == False.

• tl_off (Tensor): Predicted top-left offset heatmap.

• br_off (Tensor): Predicted bottom-right offset heatmap.

• tl_pool (Tensor): Top-left corner pool feature. Not must have.

• br_pool (Tensor): Bottom-right corner pool feature. Not must have.

Return type tuple[Tensor]

get_bboxes(tl_heats, br_heats, tl_embs, br_embs, tl_offs, br_offs, img_metas, rescale=False,

with_nms=True)

Transform network output for a batch into bbox predictions.

## Parameters

• tl_heats (list[Tensor]) – Top-left corner heatmaps for each level with shape (N, num_classes, H, W).

• br_heats (list[Tensor]) – Bottom-right corner heatmaps for each level with shape (N, num_classes, H, W).

• tl_embs (list[Tensor]) – Top-left corner embeddings for each level with shape (N, corner_emb_channels, H, W).

• br_embs (list[Tensor]) – Bottom-right corner embeddings for each level with shape (N, corner_emb_channels, H, W).

• tl_offs (list[Tensor]) – Top-left corner offsets for each level with shape (N, corner_offset_channels, H, W).

• br_offs (list[Tensor]) – Bottom-right corner offsets for each level with shape (N, corner_offset_channels, H, W).

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If True, return boxes in original image space. Default: False.

• with_nms (bool) – If True, do nms before return boxes. Default: True.