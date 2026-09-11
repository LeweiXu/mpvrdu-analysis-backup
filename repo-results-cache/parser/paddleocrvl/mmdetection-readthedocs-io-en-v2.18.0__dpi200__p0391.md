- scale_factor (ndarray) – Scale factor of the image arrange as (w_scale, h_scale, w_scale, h_scale).

• rescale (bool) – If True, return boxes in original image space. Default: False.

• (obj (cfg) – ConfigDict): test_cfg of Bbox Head. Default: None

Returns First tensor is det_bboxes, has the shape (num_boxes, 5) and last dimension 5 represent (tl_x, tl_y, br_x, br_y, score). Second tensor is the labels with shape (num_boxes, ).

Return type tuple[Tensor, Tensor]

get_targets(sampling_results, gt_bboxes, gt_labels, rcnn_train_cfg, concat=True)

Calculate the ground truth for all samples in a batch according to the sampling_results.

Almost the same as the implementation in bbox_head, we passed additional parameters pos_inds_list and neg_inds_list to _get_target_single function.

## Parameters

• (List[obj (sampling_results) – SamplingResults]): Assign results of all images in a batch after sampling.

- gt_bboxes (list[Tensor]) – Gt_bboxes of all images in a batch, each tensor has shape (num_gt, 4), the last dimension 4 represents [tl_x, tl_y, br_x, br_y].

- gt_labels (list[Tensor]) – Gt_labels of all images in a batch, each tensor has shape (num_gt,).

• (obj (rcnn_train_cfg) – ConfigDict): train_cfg of RCNN.

• concat (bool) – Whether to concatenate the results of all the images in a single batch.

## Returns

Ground truth for proposals in a single image. Containing the following list of Tensors:

• labels (list[Tensor], Tensor): Gt_labels for all proposals in a batch, each tensor in list has shape (num_proposals,) when concat=False, otherwise just a single tensor has shape (num_all_proposals,).

• label_weights (list[Tensor]): Labels_weights for all proposals in a batch, each tensor in list has shape (num_proposals,) when concat=False, otherwise just a single tensor has shape (num_all_proposals,).

• bbox_targets (list[Tensor], Tensor): Regression target for all proposals in a batch, each tensor in list has shape (num_proposals, 4) when  $ concat=False $, otherwise just a single tensor has shape (num_all_proposals, 4), the last dimension 4 represents [tl_x, tl_y, br_x, br_y].

• bbox_weights (list[tensor], Tensor): Regression weights for all proposals in a batch, each tensor in list has shape (num_proposals, 4) when  $ concat=False $, otherwise just a single tensor has shape (num_all_proposals, 4).

## Return type Tuple[Tensor]

onnx_export(rois, cls_score, bbox_pred, img_shape, cfg=None, **kwargs)

Transform network output for a batch into bbox predictions.

## Parameters

• rois (Tensor) – Boxes to be transformed. Has shape (B, num_boxes, 5)

• cls_score (Tensor) – Box scores. has shape (B, num_boxes, num_classes + 1), 1 represent the background.