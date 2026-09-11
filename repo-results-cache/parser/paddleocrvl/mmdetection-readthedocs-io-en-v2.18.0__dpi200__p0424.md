forward(pred, target, label_weight, avg_factor=None, reduction_override=None)

Calculate the GHM-R loss.

## Parameters

• pred(float tensor of size [batch_num, 4 (* class_num)]) – The prediction of box regression layer. Channel number can be 4 or 4 * class_num depending on whether it is class-agnostic.

• target (float tensor of size [batch_num, 4 (* class_num)]) – The target regression values with the same size of pred.

• label_weight(float tensor of size [batch_num, 4 (* class_num)]) – The weight of each sample, 0 if ignored.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

Returns The gradient harmonized loss.

class mmdet.models.losses.GIoULoss(eps=1e-06, reduction='mean', loss_weight=1.0)

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

####### class mmdet.models.losses.GaussianFocalLoss(alpha=2.0, gamma=4.0, reduction='mean',

 $ loss\_weight=1.0 $

GaussianFocalLoss is a variant of focal loss.

More details can be found in the paper Code is modified from kp_utils.py # noqa: E501 Please notice that the target in GaussianFocalLoss is a gaussian heatmap, not 0/1 binary target.

## Parameters

• alpha (float) – Power of prediction.

• gamma (float) – Power of target for negative samples.

• reduction (str) – Options are “none”, “mean” and “sum”.

• loss_weight (float) – Loss weight of current loss.

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction in a gaussian distribution.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.