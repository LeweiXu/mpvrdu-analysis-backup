• rescale (bool) – If True, return boxes in original image space. Default: False.

## Returns

Each item in result_list is a 3-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (t1\_x, t1\_y, b r\_x, b r\_y) $ and the 5-th column is a score between 0 and 1. The second item is an  $ (n,) $ tensor where each item is the predicted class label of the corresponding box. The third item is an  $ (n, num\_proto) $ tensor where each item is the predicted mask coefficients of instance inside the corresponding box.

Return type list[tuple[Tensor, Tensor, Tensor]]

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None)

A combination of the func:AnchorHead.loss and func:SSDHead.loss.

When self.use_ohem == True, it functions like SSDHead.loss, otherwise, it follows AnchorHead.loss. Besides, it additionally returns sampling_results.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – Class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – Specify which bounding boxes can be ignored when computing the loss. Default: None

Returns dict[str, Tensor]: A dictionary of loss components. List[:obj:SamplingResult]: Sampler results for each image.

Return type tuple

loss_single_OHEM(cls_score, bbox_pred, anchors, labels, label_weights, bbox_targets, bbox_weights,

“See func:SSDHead.loss.”

class mmdet.models.dense_heads.YOLACTProtonet(num_classes, in_channels=256, proto_channels=(256, 256, 256, None, 256, 32), proto_kernel_sizes=(3, 3, 3, 2, 3, 1), include_last_relu=True, num_protos=32, loss_mask_weight=1.0, max_masks_to_train=100, init_cfg='distribution': 'uniform', 'override': {'name': 'protonet'}, 'type': 'Xavier'})

YOLACT mask head used in https://arxiv.org/abs/1904.02689.

This head outputs the mask prototypes for YOLACT.

## Parameters

• in channels (int) – Number of channels in the input feature map.

• proto_channels (tuple[int]) – Output channels of protonet convs.

• proto_kernel_sizes (tuple[int]) – Kernel sizes of protonet convs.

• include last relu (Bool) – If keep the last relu of protonet.