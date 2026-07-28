class mmdet.models.dense_heads.RPNHead(in_channels, init_cfg={'layer': 'Conv2d','std': 0.01, 'type': 'Normal'}, num_convs=1, **kwargs)

## RPN head

## Parameters

• in channels (int) – Number of channels in the input feature map.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

• num_convs (int) – Number of convolution layers in the head. Default 1.

## forward_single(x)

Forward feature map of a single scale level.

loss(cls_scores, bbox_preds, gt_bboxes, img_metas, gt_bboxes_ignore=None)

Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level Has shape (N, num_anchors * num_classes, H, W)

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level with shape (N, num_anchors * 4, H, W)

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

onnx_export(x, img_metas)

Test without augmentation.

## Parameters

• x (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

• img_metas (list[dict]) – Meta info of each image.

Returns dets of shape [N, num_det, 5].

Return type Tensor