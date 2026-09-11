• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.L1Loss(reduction='mean', loss_weight=1.0)

L1 loss.

## Parameters

• reduction (str, optional) – The method to reduce the loss. Options are “none”, “mean” and “sum”.

• loss_weight (float, optional) – The weight of loss.

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.MSELoss(reduction='mean', loss_weight=1.0)

MSELoss.

## Parameters

• reduction (str, optional) – The method that reduces the loss to a scalar. Options are “none”, “mean” and “sum”.

• loss_weight (float, optional) – The weight of the loss. Defaults to 1.0

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function of loss.

## Parameters

• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction.

• weight (torch.Tensor, optional) – Weight of the loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

Returns The calculated loss

Return type torch.Tensor