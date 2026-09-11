## Parameters

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_priors * 4.

• objectnesses (list[Tensor], Optional) – Score factor for all scale level, each is a 4D-tensor, has shape (batch_size, 1, H, W).

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

### 39.5 roi heads

class mmdet.models.roi_heads.BBoxHead(with_avg_pool=False, with_cls=True, with_reg=True,

(with_avg_pool=False, with_cls=True, with_reg=True,
roi_feat_size=7, in_channels=256, num_classes=80,
bbox_coder={'clip_border': True, 'target_means': [0.0, 0.0, 0.0, 0.0], 'target_stds': [0.1, 0.1, 0.2, 0.2], 'type': 'DeltaXYWHBBoxCoder'}, reg_class_agnostic=False,
reg_ decoded_bbox=False, reg_predictor_cfg={'type': 'Linear'},
cls_predictor_cfg={'type': 'Linear'}, loss_cls={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': False},
loss_bbox={'beta': 1.0, 'loss_weight': 1.0, 'type': 'SmoothL1Loss'},
init_cfg=None)

Simplest RoI head, with only two fc layers for classification and regression respectively.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

get_bboxes(rois, cls_score, bbox_pred, img_shape, scale_factor, rescale=False, cfg=None)

Transform network output for a batch into bbox predictions.

## Parameters

• rois (Tensor) – Boxes to be transformed. Has shape (num_boxes, 5). last dimension 5 arrange as (batch_index, x1, y1, x2, y2).

• cls_score (Tensor) – Box scores, has shape (num_boxes, num_classes + 1).

• bbox_pred (Tensor, optional) – Box energies / deltas. has shape (num_boxes, num_classes * 4).

• img_shape (Sequence[int], optional) – Maximum bounds for boxes, specifies (H, W, C) or (H, W).