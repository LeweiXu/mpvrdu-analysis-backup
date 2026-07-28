Note that YOLACT head is a light version of RetinaNet head. Four differences are described as follows:

1. YOLACT box head has three-times fewer anchors.

2. YOLACT box head shares the convs for box and cls branches.

3. YOLACT box head uses OHEM instead of Focal loss.

4. YOLACT box head predicts a set of mask coefficients for each box.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• anchor_generator (dict) – Config dict for anchor generator

• loss_cls (dict) – Config of classification loss.

• loss_bbox(dict) – Config of localization loss.

• num_head_convs (int) – Number of the conv layers shared by box and cls branches.

• num_proto(int) – Number of the mask coefficients.

• use_ohem (bool) – If true, loss_single_OHEM will be used for cls loss calculation. If false, loss_single will be used.

• conv_cfg(dict) – Dictionary to construct and configure conv layer.

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward_single(x)

Forward feature of a single scale level.

Parameters x (Tensor) – Features of a single scale level.

Returns cls_score (Tensor): Cls scores for a single scale level the channels number is num_anchors * num_classes. bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_anchors * 4. coeff_pred (Tensor): Mask coefficients for a single scale level, the channels number is num_anchors * num_protos.

## Return type tuple

get_bboxes(cls_scores, bbox_preds, coeff_preds, img_metas, cfg=None, rescale=False)

“Similar to func:AnchorHead.get_bboxes, but additionally processes coeff_preds.”

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level with shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

• coeff_preds (list[Tensor]) – Mask coefficients for each scale level with shape (N, num_anchors * num_protos, H, W)

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

•cfg (mmcv.Config / None) – Test / postprocessing configuration, if None, test_cfg would be used