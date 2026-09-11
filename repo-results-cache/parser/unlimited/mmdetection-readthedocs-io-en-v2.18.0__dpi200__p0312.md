MMDetection, Release 2.18.0
- gt_bboxes(list[Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.
- gt_labels (list[Tensor]) – class indices corresponding to each box
- img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.
- gt_bboxes_ignore (None | list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.
class mmdet.models.dense_heads.AnchorHead(num_classes, in_channels, feat_channels=256,
anchor_generator={'ratios': [0.5, 1.0, 2.0], 'scales': [8, 16, 32], 'strides': [4, 8, 16, 32, 64], 'type': 'AnchorGenerator'}, bbox_coder={'clip_border': True, 'target_means': (0.0, 0.0, 0.0, 0.0), 'target_stds': (1.0, 1.0, 1.0, 1.0), 'type': 'DeltaXYWHBBoxCoder'}, reg decoded_bbox=False, loss_cls={'loss_weight': 1.0, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, loss_bbox={'beta': 0.1111111111111111, 'loss_weight': 1.0, 'type': 'SmoothL1Loss'}, train_cfg=None, test_cfg=None, init_cfg={'layer': 'Conv2d', 'std': 0.01, 'type': 'Normal'})
Anchor-based head (RPN, RetinaNet, SSD, etc.).
Parameters
- num_classes (int) – Number of categories excluding the background category.
- in_channels (int) – Number of channels in the input feature map.
- feat_channels (int) – Number of hidden channels. Used in child classes.
- anchor_generator (dict) – Config dict for anchor generator
- bbox_coder (dict) – Config of bounding box coder.
- reg decoded_bbox (bool) – If true, the regression loss would be applied directly on decoded bounding boxes, converting both the predicted boxes and regression targets to absolute coordinates format. Default False. It should be True when using IoULoss, GIoULoss, or DIoULoss in the bbox head.
- loss_cls (dict) – Config of classification loss.
- loss_bbox(dict) – Config of localization loss.
- train_cfg (dict) – Training config of anchor head.
- test_cfg (dict) – Testing config of anchor head.
- init_cfg (dict or list [dict], optional) – Initialization config dict.
aug_test(feats, img_metas, rescale=False)
Test function with test time augmentation.
Parameters
- feats (list[Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains features for all images in the batch.
- img_metas (list[list[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch. each dict has image information.
- rescale (bool, optional) – Whether to rescale the results. Defaults to False.
Returns
39.4. dense_heads
305