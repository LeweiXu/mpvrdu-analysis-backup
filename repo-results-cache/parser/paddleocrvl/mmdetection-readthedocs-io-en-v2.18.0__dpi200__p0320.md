## Returns

The float value is mean avg_factor, the dict has components below: - center_heatmap_target (Tensor): targets of center heatmap, shape (B, num_classes, H, W). - wh_target (Tensor): targets of wh predict, shape (B, 2, H, W). - offset_target (Tensor): targets of offset predict, shape (B, 2, H, W). - wh_offset_target_weight (Tensor): weights of wh and offset predict, shape (B, 2, H, W).

## Return type tuple[dict, float]

## init_weights()

Initialize weights of the head.

loss(center_heatmap_preds, wh_preds, offset_preds, gt_bboxes, gt_labels, img_metas,

gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

- center_heatmap_pred(list[Tensor]) – center predict heatmaps for all levels with shape (B, num_classes, H, W).

• wh_preds (list[Tensor]) – wh predicts for all levels with shape (B, 2, H, W).

• offset_preds (list [Tensor]) – offset predicts for all levels with shape (B, 2, H, W).

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss. Default: None

## Returns

which has components below:

• loss center heatmap (Tensor): loss of center heatmap.

• loss_wh (Tensor): loss of hw heatmap

• loss offset (Tensor): loss of offset heatmap.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.CentripetalHead(*args, centripetal_shift_channels=2)

guiding_shift_channels=2,

feat\_adaption\_conv\_kernel=3,

 $ loss\_guiding\_shift=\{beta':1.0,\ 'loss\_weight':0.05, $

'type': 'SmoothL1Loss'}, loss_centripetal_shift={'beta':

1.0, 'loss_weight': 1, 'type': 'SmoothL1Loss'},

Head of CentripetalNet: Pursuing High-quality Keypoint Pairs for Object Detection.

CentripetalHead inherits from CornerHead. It removes the embedding branch and adds guiding shift and centripetal shift branches. More details can be found in the paper.

## Parameters

• num_classes (int) – Number of categories excluding the background category.