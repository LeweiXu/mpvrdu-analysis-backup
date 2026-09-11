## forward_single(x)

Forward feature of a single scale level.

Parameters x (Tensor) – Features of a single scale level.

## Returns

cls_score (Tensor): Cls scores for a single scale level the channels number is num_anchors * num_classes.

bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_anchors * 4.

Return type tuple

class mmdet.models.dense_heads.RetinaSepBNHead(num_classes, num_ins, in_channels, stacked_convs=4, conv_cfg=None, norm_cfg=None, init_cfg=None, **kwargs)

“RetinaHead with separate BN.

In RetinaHead, conv/norm layers are shared across different FPN levels, while in RetinaSepBNHead, conv layers are shared across different FPN levels, but BN layers are separated.

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

Usually a tuple of classification scores and bbox prediction

cls_scores (list[Tensor]): Classification scores for all scale levels, each is a 4D-tensor, the channels number is num_anchors * num_classes.

bbox_pred(list[Tensor]): Box energies / deltas for all scale levels, each is a 4D-tensor, the channels number is num_anchors * 4.

Return type tuple

## init_weights()

Initialize weights of the head.