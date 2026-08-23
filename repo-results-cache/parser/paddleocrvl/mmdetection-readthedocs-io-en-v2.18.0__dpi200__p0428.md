• cls_score (torch.Tensor) – The prediction with shape  $ (N, C + 2) $.

• labels (torch.Tensor) – The learning label of the prediction.

• label_weights (torch.Tensor, optional) – Sample-wise loss weight.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction (str, optional) – The method used to reduce the loss. Options are “none”, “mean” and “sum”.

Returns if return_dict == False: The calculated loss | if return_dict == True: The dict of calculated losses for objectness and classes, respectively.

Return type torch.Tensor | Dict [str, torch.Tensor]

## get_accuracy(cls_score, labels)

Get custom accuracy w.r.t. cls_score and labels.

## Parameters

• cls_score (torch.Tensor) – The prediction with shape  $ (N, C + 2) $.

• labels (torch.Tensor) – The learning label of the prediction.

## Returns

The accuracy for objectness and classes, respectively.

Return type Dict [str, torch.Tensor]

## get_activation(cls_score)

Get custom activation of cls_score.

Parameters cls_score (torch.Tensor) – The prediction with shape  $ (N, C + 2) $.

Returns

The custom activation of cls_score with shape  $ (N, C + 1) $.

Return type torch.Tensor

## get_cls_channels(num_classes)

Get custom classification channels.

Parameters num_classes (int) – The number of classes.

Returns The custom classification channels.

Return type int

class mmdet.models.losses.SmoothL1Loss(beta=1.0, reduction='mean', loss_weight=1.0)

Smooth L1 loss.

## Parameters

• beta (float, optional) – The threshold in the piecewise function. Defaults to 1.0.

• reduction (str, optional) – The method to reduce the loss. Options are “none”, “mean” and “sum”. Defaults to “mean”.

• loss_weight (float, optional) – The weight of loss.

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Forward function.

Parameters