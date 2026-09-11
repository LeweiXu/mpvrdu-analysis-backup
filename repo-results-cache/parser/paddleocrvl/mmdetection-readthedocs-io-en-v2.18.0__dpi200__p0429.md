• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.VarifocalLoss(use_sigmoid=True, alpha=0.75, gamma=2.0,

 $ iou\_weighted=True,\ reduction='mean', loss\_weight=1.0 $

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Options are “none”, “mean” and “sum”.

Returns The calculated loss

Return type torch.Tensor

mmdet.models.losses.binary_cross_entropy(pred, label, weight=None, reduction='mean',

avg_factor=None, class_weight=None, ignore_index=-100

Calculate the binary CrossEntropy loss.

## Parameters

• pred (torch.Tensor) – The prediction with shape  $ (N, 1) $.

• label (torch.Tensor) – The learning label of the prediction.

• weight (torch.Tensor, optional) – Sample-wise loss weight.

• reduction (str, optional) – The method used to reduce the loss. Options are “none”, “mean” and “sum”.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• class_weight (list[float], optional) – The weight for each class.

• ignore_index (int / None) – The label index to be ignored. If None, it will be set to default value. Default: -100.

Returns The calculated loss.

Return type torch.Tensor