class mmdet.models.dense_heads.LDHead(num_classes, in_channels, loss_ld='T': 10, 'loss_weight': 0.25, 'type': 'LocalizationDistillationLoss'}, **kwargs)

Localization distillation Head. (Short description)

It utilizes the learned bbox distributions to transfer the localization dark knowledge from teacher to student. Original paper: Localization Distillation for Object Detection.

## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• loss_ld (dict) – Config of Localization Distillation Loss (LD), T is the temperature for distillation.

forward_train(x, out_teacher, img_metas, gt_bboxes, gt_labels=None, gt_bboxes_ignore=None, proposal_cfg=None, **kwargs)

## Parameters

• x (list [Tensor]) – Features from FPN.

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• gt_bboxes (Tensor) – Ground truth bboxes of the image, shape (num_gts, 4).

• gt_labels (Tensor) – Ground truth labels of each box, shape (num_gts,).

- gt_bboxes_ignore (Tensor) – Ground truth bboxes to be ignored, shape (num_ignored_gts, 4).

• proposal_cfg (mmcv.Config) – Test / postprocessing configuration, if None, test_cfg would be used

## Returns

The loss components and proposals of each image.

• losses (dict[str, Tensor]): A dictionary of loss components.

• proposal_list (list[Tensor]): Proposals of each image.

Return type tuple[dict, list]

loss(cls_scores, bbox_preds, gt_bboxes, gt_labels, soft_target, img_metas, gt_bboxes_ignore=None) Compute losses of the head.

## Parameters

• cls_scores (list[Tensor]) – Cls and quality scores for each scale level has shape (N, num_classes, H, W).

• bbox_preds (list [Tensor]) – Box distribution logits for each scale level with shape (N, 4*(n+1), H, W), n is max value of integral set.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.