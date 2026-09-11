class mmdet.models.losses.DiceLoss(use_sigmoid=True, activate=True, reduction='mean', loss_weight=1.0, eps=0.001)

forward(pred, target, weight=None, reduction_override=None, avg_factor=None)

Forward function.

## Parameters

• pred (torch.Tensor) – The prediction, has a shape (n, *).

• target (torch.Tensor) – The label of the prediction, shape  $ (n, *) $, same shape of pred.

• weight (torch.Tensor, optional) – The weight of loss for each prediction, has a shape (n,). Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Options are “none”, “mean” and “sum”.

Returns The calculated loss

Return type torch.Tensor

class mmdet.models.losses.DistributionFocalLoss(reduction='mean', loss_weight=1.0)

Distribution Focal Loss (DFL) is a variant of Generalized Focal Loss: Learning Qualified and Distributed Bounding Boxes for Dense Object Detection.

## Parameters

• reduction (str) – Options are ‘none’, ‘mean’ and ‘sum’.

• loss_weight (float) – Loss weight of current loss.

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (torch.Tensor) – Predicted general distribution of bounding boxes (before softmax) with shape  $ (N, n+1) $, n is the max value of the integral set  $ \{0, \ldots, n\} $ in paper.

• target (torch.Tensor) – Target distance label for bounding boxes with shape (N,).

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.FocalLoss(use_sigmoid=True, gamma=2.0, alpha=0.25, reduction='mean', loss_weight=1.0)

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

Parameters

• pred (torch.Tensor) – The prediction.