• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.IoULoss(linear=False, eps=1e-06, reduction='mean', loss_weight=1.0)

 $$ mode=^{\prime}log^{\prime}) $$ 

IoULoss.

Computing the IoU loss between a set of predicted bboxes and target bboxes.

## Parameters

• linear (bool) – If True, use linear scale of loss else determined by mode. Default: False.

• eps (float) – Eps to avoid  $ \log(0) $.

• reduction (str) – Options are “none”, “mean” and “sum”.

• loss_weight (float) – Weight of loss.

• mode(str) – Loss scaling mode, including “linear”, “square”, and “log”. Default: ‘log’

forward(pred, target, weight=None, avg_factor=None, reduction_override=None, **kwargs)

Forward function.

## Parameters

• pred (torch.Tensor) – The prediction.

• target (torch.Tensor) – The learning target of the prediction.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None. Options are “none”, “mean” and “sum”.

class mmdet.models.losses.KnowledgeDistillationKLDivLoss(reduction='mean', loss_weight=1.0)

 $$ T=10) $$ 

Loss function for knowledge distilling using KL divergence.

## Parameters

• reduction (str) – Options are ‘none’, ‘mean’ and ‘sum’.

• loss_weight (float) – Loss weight of current loss.

• T (int) – Temperature for distillation.

forward(pred, soft_label, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (Tensor) – Predicted logits with shape  $ (N, n + 1) $.

• soft_label (Tensor) – Target logits with shape  $ (N, N + 1) $.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.