- gt_bboxes_ignore (list[Tensor] / None) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

loss_single( anchors, cls_score, bbox_pred, labels, label_weights, bbox_targets, stride, soft_targets, num_total_samples)

Compute loss of a single scale level.

## Parameters

• anchors (Tensor) – Box reference for each scale level with shape (N, num_total_anchors, 4).

• cls_score (Tensor) – Cls and quality joint scores for each scale level has shape (N, num_classes, H, W).

• bbox_pred (Tensor) – Box distribution logits for each scale level with shape  $ (N, 4*(n+1), H, W) $, n is max value of integral set.

• labels (Tensor) – Labels of each anchor with shape (N, num_total_anchors).

• label_weights (Tensor) – Label weights of each anchor with shape (N, num_total_anchors)

• bbox_targets (Tensor) – BBox regression targets of each anchor weight shape (N, num_total_anchors, 4).

• stride (tuple) – Stride in this scale level.

• num_total_samples (int) – Number of positive samples that is reduced over all GPUs.

Returns Loss components and weight targets.

Return type dict[tuple, Tensor]

class mmdet.models.dense_heads.NASFCOSHead(*args, init_cfg=None, **kwargs)

Anchor-free head used in NASFCOS.

It is quite similar with FCOS head, except for the searched structure of classification branch and bbox regression branch, where a structure of “dconv3x3, conv3x3, dconv3x3, conv1x1” is utilized instead.

class mmdet.models.dense_heads.PAAHead(*args, topk=9, score_voting=True, covariance_type='diag', **kwargs)

Head of PAAAssignment: Probabilistic Anchor Assignment with IoU Prediction for Object Detection.

Code is modified from the official github repo.

More details can be found in the paper.

## Parameters

• topk (int) – Select topk samples with smallest loss in each level.

• score voting (bool) – Whether to use score voting in post-process.

• covariance_type – String describing the type of covariance parameters to be used in sklearn.mixture.GaussianMixture. It must be one of:

– 'full': each component has its own general covariance matrix

– 'tied': all components share the same general covariance matrix

– 'diag': each component has its own diagonal covariance matrix