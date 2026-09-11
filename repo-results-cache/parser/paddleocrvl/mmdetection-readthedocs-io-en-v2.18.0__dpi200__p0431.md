## Example

>>> N, C = 3, 11
>>> H, W = 2, 2
>>> pred = torch.randn(N, C, H, W) * 1000
>>> target = torch.rand(N, H, W)
>>> label = torch.randint(0, C, size=(N,))
>>> reduction ='mean'
>>> avg_factor = None
>>> class_weights = None
>>> loss = mask_cross_entropy(pred, target, label, reduction,
                                    avg_factor, class_weights)
>>> assert loss.shape == (1,)

##### mmdet.models.losses.mse_loss(pred, target)

Warper of mse loss.

##### mmdet.models.losses.reduce_loss(loss, reduction)

Reduce loss as specified.

## Parameters

• loss (Tensor) – Elementwise loss tensor.

• reduction (str) – Options are “none”, “mean” and “sum”.

Returns Reduced loss tensor.

Return type Tensor

mmdet.models.losses.sigmoid_focal_loss(pred, target, weight=None, gamma=2.0, alpha=0.25)

A warpper of cuda version Focal Loss.

## Parameters

• pred (torch.Tensor) – The prediction with shape (N, C), C is the number of classes.

• target (torch.Tensor) – The learning label of the prediction.

• weight (torch.Tensor, optional) – Sample-wise loss weight.

• gamma (float, optional) – The gamma for calculating the modulating factor. Defaults to 2.0.

• alpha (float, optional) – A balanced form for Focal Loss. Defaults to 0.25.

• reduction (str, optional) – The method used to reduce the loss into a scalar. Defaults to ‘mean’. Options are “none”, “mean” and “sum”.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

##### mmdet.models.losses.weighted_loss(loss_func)

Create a weighted version of a given loss function.

To use this decorator, the loss function must have the signature like  $ loss\_func(pred, target, **kwargs) $. The function only needs to compute element-wise loss without any reduction. This decorator will add weight and reduction arguments to the function. The decorated function will have the signature like  $ loss\_func(pred, target, weight=None, reduction='mean', avg\_factor=None, **kwargs) $.

## Example