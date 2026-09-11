• target (torch.Tensor) – The learning label of the prediction.

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Options are “none”, “mean” and “sum”.

Returns The calculated loss

Return type torch.Tensor

class mmdet.models.losses.GHMC(bins=10, momentum=0, use_sigmoid=True, loss_weight=1.0)

 $$ reduction=^{\prime}mean^{\prime}) $$ 

GHM Classification Loss.

Details of the theorem can be viewed in the paper Gradient Harmonized Single-stage Detector.

## Parameters

• bins (int) – Number of the unit regions for distribution calculation.

• momentum (float) – The parameter for moving average.

• use_sigmoid(bool) – Can only be true for BCE based loss now.

• loss_weight (float) – The weight of the total GHM-C loss.

• reduction (str) – Options are “none”, “mean” and “sum”. Defaults to “mean”

forward(pred, target, label_weight, reduction_override=None, **kwargs)

Calculate the GHM-C loss.

## Parameters

• pred(float tensor of size [batch_num, class_num])—The direct prediction of classification fc layer.

• target (float tensor of size [batch_num, class_num]) – Binary class target for each sample.

• label_weight (float tensor of size [batch_num, class_num]) – the value is 1 if the sample is valid and 0 if ignored.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

Returns The gradient harmonized loss.

class mmdet.models.losses.GHMR(mu=0.02, bins=10, momentum=0, loss_weight=1.0, reduction='mean') GHM Regression Loss.

Details of the theorem can be viewed in the paper Gradient Harmonized Single-stage Detector.

## Parameters

• mu (float) – The parameter for the Authentic Smooth L1 loss.

• bins (int) – Number of the unit regions for distribution calculation.

• momentum (float) – The parameter for moving average.

• loss_weight (float) – The weight of the total GHM-R loss.

• reduction (str) – Options are “none”, “mean” and “sum”. Defaults to “mean”