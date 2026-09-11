- optimizer (torch.optim.Optimizer | dict) – The optimizer of runner is passed to train_step(). This argument is unused and reserved.

## Returns

It should contain at least 3 keys: loss, log_vars, num_samples.

• loss is a tensor for back propagation, which can be a weighted sum of multiple losses.

• log_vars contains all the variables to be sent to the logger.

- num_samples indicates the batch size (when the model is DDP, it means the batch size on each GPU), which is used for averaging the logs.

## Return type dict

## val_step(data, optimizer=None)

The iteration step during validation.

This method shares the same signature as  $ train\_step() $, but used during val epochs. Note that the evaluation after training epochs is not implemented with this method, but an evaluation hook.

## property with_bbox

whether the detector has a bbox head

Type bool

property with_mask

whether the detector has a mask head

Type bool

property with\_neck

whether the detector has a neck

Type bool

property with_shared_head

whether the detector has a shared head in the RoI Head

Type bool

class mmdet.models.detectors.CascadeRCNN(backbone, neck=None, rpn_head=None, roi_head=None, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of Cascade R-CNN: Delving into High Quality Object Detection

show_result(data, result, **kwargs)

Show prediction results of the detector.

## Parameters

• data (str or np.ndarray) – Image filename or loaded image.

• result (Tensor or tuple) – The results to draw over img bbox_result or (bbox_result, segm_result).

Returns The image with bboxes drawn on it.

Return type np.ndarray

class mmdet.models.detectors.CenterNet(backbone, neck, bbox_head, train_cfg=None, test_cfg=None,

pretrained=None, init_cfg=None

Implementation of CenterNet(Objects as Points)

<https://arxiv.org/abs/1904.07850>.