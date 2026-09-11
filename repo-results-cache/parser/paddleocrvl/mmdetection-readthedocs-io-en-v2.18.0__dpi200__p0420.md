## Return type tuple[float]

####### class mmdet.models.losses.AssociativeEmbeddingLoss(pull_weight=0.25, push_weight=0.25)

Associative Embedding Loss.

More details can be found in Associative Embedding and CornerNet. Code is modified from kp_utils.py # noqa: E501

## Parameters

• pull_weight (float) – Loss weight for corners from same object.

• push_weight (float) – Loss weight for corners from different object.

forward(pred, target, match)

Forward function.

class mmdet.models.losses.BalancedL1Loss(alpha=0.5, gamma=1.5, beta=1.0, reduction='mean', loss_weight=1.0)

Balanced L1 Loss.

arXiv: https://arxiv.org/pdf/1904.02701.pdf (CVPR 2019)

## Parameters

• alpha (float) – The denominator alpha in the balanced L1 loss. Defaults to 0.5.

• gamma (float) – The gamma in the balanced L1 loss. Defaults to 1.5.

• beta (float, optional) – The loss is a piecewise function of prediction and target. beta serves as a threshold for the difference between the prediction and target. Defaults to 1.0.

• reduction (str, optional) – The method that reduces the loss to a scalar. Options are “none”, “mean” and “sum”.

• loss_weight (float, optional) – The weight of the loss. Defaults to 1.0

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Forward function of loss.

## Parameters

• pred (torch.Tensor) – The prediction with shape (N, 4).

• target (torch.Tensor) – The learning target of the prediction with shape  $ (N, 4) $.

• weight (torch.Tensor, optional) – Sample-wise loss weight with shape (N, ).

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Options are “none”, “mean” and “sum”.

Returns The calculated loss

Return type torch.Tensor

class mmdet.models.losses.BoundedIoULoss(beta=0.2, eps=0.001, reduction='mean', loss_weight=1.0)

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Defines the computation performed at every call.

Should be overridden by all subclasses.