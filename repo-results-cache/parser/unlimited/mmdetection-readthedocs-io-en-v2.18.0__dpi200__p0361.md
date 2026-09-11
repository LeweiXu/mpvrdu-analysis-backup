MMDetection, Release 2.18.0
class mmdet.models.dense_heads.RepPointsHead(num_classes, in_channels, point_feat_channels=256, num_points=9, gradient_mul=0.1, point_strides=[8, 16, 32, 64, 128], point_base_scale=4, loss_cls={'alpha': 0.25, 'gamma': 2.0, 'loss_weight': 1.0, 'type': 'FocalLoss', 'use_sigmoid': True}, loss_bbox_init={'beta': 0.111111111111111, 'loss_weight': 0.5, 'type': 'SmoothL1Loss'}, loss_bbox_refine={'beta': 0.111111111111111, 'loss_weight': 1.0, 'type': 'SmoothL1Loss'}, use_grid_points=False, center_init=True, transform_method='moment', moment_mul=0.01, init_cfg={'layer': 'Conv2d', 'override': {'bias_prob': 0.01, 'name': 'repoints_cls_out', 'std': 0.01, 'type': 'Normal'}, 'std': 0.01, 'type': 'Normal'}, **kwargs)
RepPoint head.
Parameters
- point_feat_channels (int) – Number of channels of points features.
- gradient_mul (float) – The multiplier to gradients from points refinement and recognition.
- point_strides (Iterable) – points strides.
- point_base_scale (int) – bbox scale for assigning labels.
- loss_cls (dict) – Config of classification loss.
- loss_bbox_init (dict) – Config of initial points loss.
- loss_bbox_refine (dict) – Config of points loss in refinement.
- use_grid_points(bool) – If we use bounding box representation, the
- is represented as grid points on the bounding box. (reppoints) –
- center_init(bool) – Whether to use center point assignment.
- transform_method (str) – The methods to transform RepPoints to bbox.
- init_cfg (dict or list[dict], optional) – Initialization config dict.
centers_to_bboxes(point_list)
Get bboxes according to center points.
Only used in MaxIoUAssigner.
forward(feats)
Forward features from the upstream network.
Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.
Returns
Usually contain classification scores and bbox predictions.
cls_scores (list[Tensor]): Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.
bbox_preds (list[Tensor]): Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.
Return type tuple
354
Chapter 39. mmdet.models