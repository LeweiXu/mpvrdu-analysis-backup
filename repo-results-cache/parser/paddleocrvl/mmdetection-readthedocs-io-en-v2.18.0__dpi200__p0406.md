## Parameters

• x(tuple[Tensor]) – Features from upstream network. Each has shape (batch_size, c, h, w).

• proposal_list (list(Tensor)) – Proposals from rpn head. Each has shape (num_proposals, 5), last dimension 5 represent (x1, y1, x2, y2, score).

• img_metas (list[dict]) – Meta information of images.

• rescale (bool) – Whether to rescale the results to the original image. Default: True.

Returns When no mask branch, it is bbox results of each image and classes with type list[list[np.ndarray]]. The outer list corresponds to each image. The inner list corresponds to each class. When the model has mask branch, it contains bbox results and mask results. The outer list corresponds to each image, and first element of tuple is bbox results, second element is mask results.

Return type list[list[np.ndarray]] or list[tuple]

property with_semantic

whether the head has semantic head

Type bool

class mmdet.models.roi_heads.MaskIoUHead(num_convs=4, num_fcs=2, roi_feat_size=14)

(num_convs=4, num_fcs=2, roi_feat_size=14, in_channels=256, conv_out_channels=256, fc_out_channels=1024, num_classes=80, loss_iou={'loss_weight': 0.5, 'type': 'MSELoss'}, init_cfg=[{'type': 'Kaiming', 'override': {'name': 'convs'}, {'type': 'Caffe2Xavier', 'override': {'name': 'fcs'}, {'type': 'Normal','std': 0.01, 'override': {'name': 'fc_mask_iou}}}}])

Mask IoU Head.

This head predicts the IoU of predicted masks and corresponding gt masks.

forward(mask_feat, mask_pred)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

get_mask_scores(mask_iou_pred, det_bboxes, det_labels)

Get the mask scores.

mask score = bbox score * mask iou

get_targets(sampling_results, gt_masks, mask_pred, mask_targets, rcnn_train_cfg)

Compute target of mask IoU.

Mask IoU target is the IoU of the predicted mask (inside a bbox) and the gt mask of corresponding gt mask (the whole instance). The intersection area is computed inside the bbox, and the gt mask area is computed with two steps, firstly we compute the gt area inside the bbox, then divide it by the area ratio of gt area inside the bbox and the gt area of the whole instance.

Parameters

• sampling_results (list[SamplingResult]) – sampling results.