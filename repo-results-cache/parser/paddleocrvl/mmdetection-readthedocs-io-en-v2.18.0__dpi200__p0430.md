mmdet.models.losses.cross_entropy(pred, label, weight=None, reduction='mean', avg_factor=None, class_weight=None, ignore_index=-100)

Calculate the CrossEntropy loss.

## Parameters

• pred (torch.Tensor) – The prediction with shape (N, C), C is the number of classes.

• label (torch.Tensor) – The learning label of the prediction.

• weight (torch.Tensor, optional) – Sample-wise loss weight.

• reduction (str, optional) – The method used to reduce the loss.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• class_weight (list[float], optional) – The weight for each class.

• ignore_index (int / None) – The label index to be ignored. If None, it will be set to default value. Default: -100.

Returns The calculated loss

Return type torch.Tensor

mmdet.models.losses.mask_cross_entropy(pred, target, label, reduction='mean', avg_factor=None, class_weight=None, ignore_index=None)

Calculate the CrossEntropy loss for masks.

## Parameters

• pred (torch.Tensor) – The prediction with shape (N, C, *), C is the number of classes. The trailing * indicates arbitrary shape.

• target (torch.Tensor) – The learning label of the prediction.

• label (torch.Tensor) – label indicates the class label of the mask corresponding object. This will be used to select the mask in the class which the object belongs to when the mask prediction is not class-agnostic.

• reduction (str, optional) – The method used to reduce the loss. Options are “none”, “mean” and “sum”.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• class_weight (list[float], optional) – The weight for each class.

• ignore_index (None) – Placeholder, to be consistent with other loss. Default: None.

Returns The calculated loss

Return type torch.Tensor