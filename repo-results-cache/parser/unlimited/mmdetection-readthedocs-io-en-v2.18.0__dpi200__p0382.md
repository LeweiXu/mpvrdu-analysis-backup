MMDetection, Release 2.18.0
- det_coeffs (list[Tensor]) – BBox coefficient of each image. each element is (n, m) tensor, m is vector length.
- img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.
- rescale (bool, optional) – Whether to rescale the results. Defaults to False.
Returns
encoded masks. The c-th item in the outer list corresponds to the c-th class. Given the c-th outer list, the i-th item in that inner list is the mask for the i-th box with class label c.
Return type list[list]
class mmdet.models.dense_heads.YOLACTSegmHead(num_classes, in_channels=256,
loss_segm={'loss_weight': 1.0, 'type':
'CrossEntropyLoss', 'use_sigmoid': True},
init_cfg={'distribution': 'uniform', 'override': {'name':
'segm_conv'], 'type': 'Xavier'})
YOLACT segmentation head used in https://arxiv.org/abs/1904.02689.
Apply a semantic segmentation loss on feature space using layers that are only evaluated during training to increase performance with no speed penalty.
Parameters
- in_channels (int) – Number of channels in the input feature map.
- num_classes (int) – Number of categories excluding the background category.
- loss_segm(dict) – Config of semantic segmentation loss.
- init_cfg (dict or list[dict], optional) – Initialization config dict.
forward(x)
Forward feature from the upstream network.
Parameters x (Tensor) – Feature from the upstream network, which is a 4D-tensor.
Returns
Predicted semantic segmentation map with shape (N, num_classes, H, W).
Return type Tensor
get_targets(segm_pred, gt_masks, gt_labels)
Compute semantic segmentation targets for each image.
Parameters
- segm_pred (Tensor) – Predicted semantic segmentation map with shape (num_classes, H, W).
- gt_masks (Tensor) – Ground truth masks for each image with the same shape of the input image.
- gt_labels (Tensor) – Class indices corresponding to each box.
Returns
Semantic segmentation targets with shape (num_classes, H, W).
Return type Tensor
39.4. dense heads
375