• in channels (int) – Number of channels in the input feature map.

• num_feat_levels (int) – Levels of feature from the previous module. 2 for HourglassNet-104 and 1 for HourglassNet-52. HourglassNet-104 outputs the final feature and intermediate supervision feature and HourglassNet-52 only outputs the final feature. Default: 2.

• corner_emb_channels (int) – Channel of embedding vector. Default: 1.

• train_cfg (dict / None) – Training config. Useless in CornerHead, but we keep this variable for SingleStageDetector. Default: None.

• test_cfg (dict / None) – Testing config of CornerHead. Default: None.

• loss_heatmap(dict / None) – Config of corner heatmap loss. Default: GaussianFocalLoss.

• loss_embedding (dict / None) – Config of corner embedding loss. Default: AssociativeEmbeddingLoss.

• loss_offset (dict / None) – Config of corner offset loss. Default: SmoothL1Loss.

• loss_guiding_shift (dict) – Config of guiding shift loss. Default: SmoothL1Loss.

• loss_centripetal_shift (dict) – Config of centripetal shift loss. Default: SmoothL1Loss.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## forward_single(x, lvl_ind)

Forward feature of a single level.

## Parameters

• x (Tensor) – Feature of a single level.

•  $  \text{lvl\_ind(int)}  $ – Level index of current feature.

## Returns

A tuple of CentripetalHead’s output for current feature level. Containing the following Tensors:

• tl_heat (Tensor): Predicted top-left corner heatmap.

• br_heat (Tensor): Predicted bottom-right corner heatmap.

• tl_off (Tensor): Predicted top-left offset heatmap.

• br_off (Tensor): Predicted bottom-right offset heatmap.

• tl_guiding_shift (Tensor): Predicted top-left guiding shift heatmap.

• br_guiding_shift (Tensor): Predicted bottom-right guiding shift heatmap.

• tl_centripetal_shift (Tensor): Predicted top-left centripetal shift heatmap.

• br_centripetal_shift (Tensor): Predicted bottom-right centripetal shift heatmap.

Return type tuple[Tensor]

get_bboxes(tl_heats, br_heats, tl_offs, br_offs, tl_guiding_shifts, br_guiding_shifts, tl_centripetal_shifts,

 $ br\_centripetal\_shifts $,  $ img\_metas $,  $ rescale=False $,  $ with\_nms=True $

Transform network output for a batch into bbox predictions.

## Parameters

• tl_heats (list[Tensor]) – Top-left corner heatmaps for each level with shape (N, num_classes, H, W).