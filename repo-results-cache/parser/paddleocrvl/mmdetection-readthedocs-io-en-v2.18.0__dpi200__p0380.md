• num_proto(int) – Number of prototypes.

• num_classes (int) – Number of categories excluding the background category.

• loss_mask_weight (float) – Reweight the mask loss by this factor.

• max_masks_to_train(int) – Maximum number of masks to train for each image.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## crop(masks, boxes, padding=1)

Crop predicted masks by zeroing out everything not in the predicted bbox.

## Parameters

• masks (Tensor) – shape [H, W, N].

• boxes (Tensor) – bbox coords in relative point form with shape [N, 4].

Returns The cropped masks.

## Return type Tensor

## forward(x, coeff_pred, bboxes, img_meta, sampling_results=None)

Forward feature from the upstream network to get prototypes and linearly combine the prototypes, using masks coefficients, into instance masks. Finally, crop the instance masks with given bboxes.

## Parameters

• x (Tensor) – Feature from the upstream network, which is a 4D-tensor.

• coeff_pred (list[Tensor]) – Mask coefficients for each scale level with shape (N, num_anchors * num_protos, H, W).

• bboxes (list[Tensor]) – Box used for cropping with shape (N, num_anchors * 4, H, W). During training, they are ground truth boxes. During testing, they are predicted boxes.

• img_meta (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

• sampling_results (List[:obj:SamplingResult]) – Sampler results for each image.

Returns Predicted instance segmentation masks.

Return type list[Tensor]

## get_seg_masks(mask_pred, label_pred, img_meta, rescale)

Resize, binarize, and format the instance mask predictions.

## Parameters

• mask pred (Tensor) – shape (N, H, W).

• label pred (Tensor) – shape (N, ).

• img_meta(dict) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If rescale is False, then returned masks will fit the scale of imgs $$ 0 $$ .

Returns Mask predictions grouped by their predicted classes.

Return type list[ndarray]

get_targets(mask_pred, gt_masks, pos_assigned_gt_inds)

Compute instance segmentation targets for each image.

Parameters

• mask_pred (Tensor) – Predicted prototypes with shape (num_classes, H, W).