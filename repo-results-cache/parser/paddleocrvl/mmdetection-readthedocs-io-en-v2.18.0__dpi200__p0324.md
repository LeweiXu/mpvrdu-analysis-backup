• centripetal loss (Tensor): Centripetal shift loss.

Return type tuple[torch.Tensor]

class mmdet.models.dense_heads.CornerHead(num_classes, in_channels, num_feat_levels=2,

corner_emb_channels=1, train_cfg=None, test_cfg=None, loss_heatmap='alpha': 2.0, 'gamma': 4.0, 'loss_weight': 1, 'type': 'GaussianFocalLoss', loss_embedding='pull_weight': 0.25, 'push_weight': 0.25, 'type': 'AssociativeEmbeddingLoss', loss_offset='beta': 1.0, 'loss_weight': 1, 'type': 'SmoothL1Loss', init_cfg=None)

Head of CornerNet: Detecting Objects as Paired Keypoints.

Code is modified from the official github repo.

More details can be found in the paper.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

- num_feat_levels (int) – Levels of feature from the previous module. 2 for HourglassNet-104 and 1 for HourglassNet-52. Because HourglassNet-104 outputs the final feature and intermediate supervision feature and HourglassNet-52 only outputs the final feature. Default: 2.

• corner_emb_channels (int) – Channel of embedding vector. Default: 1.

• train_cfg (dict / None) – Training config. Useless in CornerHead, but we keep this variable for SingleStageDetector. Default: None.

• test_cfg (dict / None) – Testing config of CornerHead. Default: None.

• loss_heatmap (dict / None) – Config of corner heatmap loss. Default: GaussianFocalLoss.

• loss_embedding (dict / None) – Config of corner embedding loss. Default: AssociativeEmbeddingLoss.

• loss_offset (dict / None) – Config of corner offset loss. Default: SmoothL1Loss.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

decode_heatmap(tl_heat, br_heat, tl_off, br_off, tl_emb=None, br_emb=None, tl_centripetal_shift=None, br_centripetal_shift=None, img_meta=None, k=100, kernel=3, distance_threshold=0.5, num_dets=1000)

Transform outputs for a single batch item into raw bbox predictions.

## Parameters

• tl_heat (Tensor) – Top-left corner heatmap for current level with shape (N, num_classes, H, W).

• br_heat (Tensor) – Bottom-right corner heatmap for current level with shape (N, num_classes, H, W).

• tl_off (Tensor) – Top-left corner offset for current level with shape (N, corner_offset_channels, H, W).

• br_off (Tensor) – Bottom-right corner offset for current level with shape (N, corner_offset_channels, H, W).