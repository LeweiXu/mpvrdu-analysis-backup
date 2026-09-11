Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.losses.CIoULoss(eps=1e-06, reduction='mean', loss_weight=1.0)

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.losses.CrossEntropyLoss(use_sigmoid=False, use_mask=False, reduction='mean', class_weight=None, ignore_index=None, loss_weight=1.0)

forward(cls_score, label, weight=None, avg_factor=None, reduction_override=None, ignore_index=None, **kwargs)

Forward function.

## Parameters

• cls_score (torch.Tensor) – The prediction.

• label (torch.Tensor) – The learning label of the prediction.

• weight (torch.Tensor, optional) – Sample-wise loss weight.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override(str, optional) – The method used to reduce the loss. Options are “none”, “mean” and “sum”.

• ignore_index(int / None) – The label index to be ignored. If not None, it will override the default value. Default: None.

Returns The calculated loss.

Return type torch.Tensor

class mmdet.models.losses.DIoULoss(eps=1e-06, reduction='mean', loss_weight=1.0)

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.