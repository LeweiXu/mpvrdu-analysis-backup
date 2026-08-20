simple_test_rpn(x, img_metas)

Simple forward test function.

class mmdet.models.dense_heads.CenterNetHead(in_channel, feat_channel, num_classes,

loss_center_heatmap=\{'loss_weight': 1.0, 'type': 'GaussianFocalLoss'\}, loss_wh=\{'loss_weight': 0.1, 'type': 'L1Loss'\}, loss_offset=\{'loss_weight': 1.0, 'type': 'L1Loss'\}, train_cfg=None, test_cfg=None, init_cfg=None)

Objects as Points Head. CenterHead use center_point to indicate object's position. Paper link <https://arxiv.org/abs/1904.07850>

## Parameters

• in channel (int) – Number of channel in the input feature map.

• feat channel (int) – Number of channel in the intermediate feature map.

• num_classes (int) – Number of categories excluding the background category.

• loss_center_heatmap(dict / None) – Config of center heatmap loss. Default: GaussianFocalLoss.

• loss_wh (dict / None) – Config of wh loss. Default: L1Loss.

• loss_offset (dict / None) – Config of offset loss. Default: L1Loss.

• train_cfg (dict / None) – Training config. Useless in CenterNet, but we keep this variable for SingleStageDetector. Default: None.

• test_cfg (dict / None) – Testing config of CenterNet. Default: None.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

decode_heatmap(center_heatmap_pred, wh_pred, offset_pred, img_shape, k=100, kernel=3)

Transform outputs into detections raw bbox prediction.

## Parameters

• center_heatmap_pred (Tensor) – center predict heatmap, shape (B, num_classes, H, W).

• wh_pred (Tensor) – wh predict, shape (B, 2, H, W).

• offset_pred (Tensor) – offset predict, shape (B, 2, H, W).

• img_shape (list[int]) – image shape in [h, w] format.

• k(int) – Get top k center keypoints from heatmap. Default 100.

• kernel (int) – Max pooling kernel for extract local maximum pixels. Default 3.

## Returns

Decoded output of CenterNetHead, containing

the following Tensors:

• batch\_bboxes (Tensor): Coords of each box with shape (B, k, 5)

• batch_topk_labels (Tensor): Categories of each box with shape (B, k)

### Return type tuple[torch.Tensor]

## forward(feats)

Forward features. Notice CenterNet head does not use FPN.