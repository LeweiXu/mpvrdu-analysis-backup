• tl_heats (list[Tensor]) – Top-left corner heatmaps for each level with shape (N, num_classes, H, W).

• br_heats (list [Tensor]) – Bottom-right corner heatmaps for each level with shape (N, num_classes, H, W).

• tl_embs (list[Tensor]) – Top-left corner embeddings for each level with shape (N, corner_emb_channels, H, W).

• br_embs (list[Tensor]) – Bottom-right corner embeddings for each level with shape (N, corner_emb_channels, H, W).

• tl_offs (list[Tensor]) – Top-left corner offsets for each level with shape (N, corner_offset_channels, H, W).

• br_offs (list[Tensor]) – Bottom-right corner offsets for each level with shape (N, corner_offset_channels, H, W).

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [left, top, right, bottom] format.

• gt_labels (list[Tensor]) – Class indices corresponding to each box.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (list[Tensor] / None) – Specify which bounding boxes can be ignored when computing the loss.

## Returns

A dictionary of loss components. Containing the following losses:

• det_loss (list[Tensor]): Corner keypoint losses of all feature levels.

• pull_loss (list[Tensor]): Part one of AssociativeEmbedding losses of all feature levels.

• push_loss (list[Tensor]): Part two of AssociativeEmbedding losses of all feature levels.

• off_loss (list[Tensor]): Corner offset losses of all feature levels.

Return type dict[str, Tensor]

## loss_single(tl_hmp, br_hmp, tl_emb, br_emb, tl_off, br_off, targets)

Compute losses for single level.

## Parameters

• tl_hmp (Tensor) – Top-left corner heatmap for current level with shape (N, num_classes, H, W).

• br_hmp (Tensor) – Bottom-right corner heatmap for current level with shape (N, num_classes, H, W).

• tl_emb (Tensor) – Top-left corner embedding for current level with shape (N, corner_emb_channels, H, W).

• br_emb (Tensor) – Bottom-right corner embedding for current level with shape (N, corner_emb_channels, H, W).

• tl_off (Tensor) – Top-left corner offset for current level with shape (N, corner_offset_channels, H, W).

• br_off (Tensor) – Bottom-right corner offset for current level with shape (N, corner_offset_channels, H, W).