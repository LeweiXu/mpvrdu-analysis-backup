## Queries

## Parameters

• num_stages (int) – Number of stage whole iterative process. Defaults to 6.

• stage_loss_weights (Tuple[float]) – The loss weight of each stage. By default all stages have the same weight 1.

• bbox_roi_extractor(dict) – Config of box roi extractor.

• mask_roi_extractor (dict) – Config of mask roi extractor.

• bbox_head (dict) – Config of box head.

• mask_head (dict) – Config of mask head.

• train_cfg (dict, optional) – Configuration information in train stage. Defaults to None.

• test_cfg(dict, optional) – Configuration information in test stage. Defaults to None.

• pretrained (str, optional) – model pretrained path. Default: None

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

aug_test(features, proposal_list, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

forward_dummy(x, proposal_boxes, proposal_features, img_metas)

Dummy forward function when do the flops computing.

forward_train(x, proposal_boxes, proposal_features, img_metas, gt_bboxes, gt_labels,

gt_bboxes_ignore=None, imgs_whwh=None, gt_masks=None

Forward function in training stage.

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• proposals (Tensor) – Decoded proposal bboxes, has shape (batch_size, num_proposals, 4)

• proposal_features (Tensor) – Expanded proposal features, has shape (batch_size, num_proposals, proposal_feature_channel)

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

• imgs_whwh (Tensor) – Tensor with shape (batch_size, 4), the dimension means [img_width, img_height, img_width, img_height].

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.