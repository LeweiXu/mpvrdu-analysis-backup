Please refer to https://arxiv.org/abs/1901.03278 for more details.

## Parameters

• num_classes (int) – Number of classes.

• in channels (int) – Number of channels in the input feature map.

• feat channels (int) – Number of hidden channels.

• approx_anchor_generator (dict) – Config dict for approx generator

• square_anchor_generator (dict) – Config dict for square generator

• anchor_coder (dict) – Config dict for anchor code

• bbox_coder(dict) – Config dict for bbox coder

• reg_ decoded_bbox (bool) – If true, the regression loss would be applied directly on decoded bounding boxes, converting both the predicted boxes and regression targets to absolute coordinates format. Default False. It should be True when using IoULoss, GIoULoss, or DIoULoss in the bbox head.

• deform_groups – (int): Group number of DCN in FeatureAdaption module.

• loc_filter_thr (float) – Threshold to filter out unconcerned regions.

• loss_loc(dict) – Config of location loss.

• loss_shape (dict) – Config of anchor shape loss.

• loss_cls (dict) – Config of classification loss.

• loss_bbox(dict) – Config of bbox regression loss.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

A tuple of classification scores and bbox prediction.

• cls_scores (list[Tensor]): Classification scores for all scale levels, each is a 4D-tensor, the channels number is num_base_priors * num_classes.

• bbox_pred(list[Tensor]): Box energies / deltas for all scale levels, each is a 4D-tensor, the channels number is num_base_priors * 4.

## Return type tuple

## forward_single(x)

Forward feature of a single scale level.

Parameters x (Tensor) – Features of a single scale level.

Returns cls_score (Tensor): Cls scores for a single scale level the channels number is num_base_priors * num_classes. bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_base_priors * 4.

Return type tuple