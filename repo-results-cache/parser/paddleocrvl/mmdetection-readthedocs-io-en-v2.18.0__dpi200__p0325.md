• tl_emb (Tensor / None) – Top-left corner embedding for current level with shape (N, corner_emb_channels, H, W).

• br_emb (Tensor / None) – Bottom-right corner embedding for current level with shape (N, corner_emb_channels, H, W).

• tl_centripetal_shift (Tensor / None) – Top-left centripetal shift for current level with shape (N, 2, H, W).

• br_centripetal_shift (Tensor / None) – Bottom-right centripetal shift for current level with shape (N, 2, H, W).

• img_meta (dict) – Meta information of current image, e.g., image size, scaling factor, etc.

• k(int) – Get top k corner keypoints from heatmap.

• kernel (int) – Max pooling kernel for extract local maximum pixels.

• distance_threshold (float) – Distance threshold. Top-left and bottom-right corner keypoints with feature distance less than the threshold will be regarded as keypoints from same object.

• num_dets (int) – Num of raw boxes before doing nms.

## Returns

Decoded output of CornerHead, containing the following Tensors:

• bboxes (Tensor): Coords of each box.

• scores (Tensor): Scores of each box.

• closes (Tensor): Categories of each box.

Return type tuple[torch.Tensor]

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

Usually a tuple of corner heatmaps, offset heatmaps and embedding heatmaps.

• tl_heats (list[Tensor]): Top-left corner heatmaps for all levels, each is a 4D-tensor, the channels number is num_classes.

• br_heats (list[Tensor]): Bottom-right corner heatmaps for all levels, each is a 4D-tensor, the channels number is num_classes.

• tl_embs (list[Tensor] | list[None]): Top-left embedding heatmaps for all levels, each is a 4D-tensor or None. If not None, the channels number is corner_emb_channels.

• br_embs (list[Tensor] | list[None]): Bottom-right embedding heatmaps for all levels, each is a 4D-tensor or None. If not None, the channels number is corner_emb_channels.

• tl_offs (list[Tensor]): Top-left offset heatmaps for all levels, each is a 4D-tensor. The channels number is corner_offset_channels.

• br_offs (list[Tensor]): Bottom-right offset heatmaps for all levels, each is a 4D-tensor. The channels number is corner_offset_channels.

Return type tuple