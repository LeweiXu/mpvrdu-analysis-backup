class mmdet.models.losses.QualityFocalLoss(use_sigmoid=True, beta=2.0, reduction='mean',

loss_weight=1.0)

Quality Focal Loss (QFL) is a variant of Generalized Focal Loss: Learning Qualified and Distributed Bounding Boxes for Dense Object Detection.

## Parameters

• use_sigmoid(bool) – Whether sigmoid operation is conducted in QFL. Defaults to True.

• beta (float) – The beta parameter for calculating the modulating factor. Defaults to 2.0.

• reduction (str) – Options are “none”, “mean” and “sum”.

• loss_weight (float) – Loss weight of current loss.

forward(pred, target, weight=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters

• pred (torch.Tensor) – Predicted joint representation of classification and quality (IoU) estimation with shape (N, C), C is the number of classes.

- target (tuple([torch.Tensor])) – Target category label with shape (N,) and target quality label with shape (N,).

• weight (torch.Tensor, optional) – The weight of loss for each prediction. Defaults to None.

• avg_factor (int, optional) – Average factor that is used to average the loss. Defaults to None.

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Defaults to None.

class mmdet.models.losses.SeesawLoss(use_sigmoid=False, p=0.8, q=2.0, num_classes=1203, eps=0.01, reduction='mean', loss_weight=1.0, return_dict=True)

Seesaw Loss for Long-Tailed Instance Segmentation (CVPR 2021) arXiv: https://arxiv.org/abs/2008.10032

## Parameters

• use_sigmoid(bool, optional) – Whether the prediction uses sigmoid of softmax. Only False is supported.

• p (float, optional) – The p in the mitigation factor. Defaults to 0.8.

• q (float, optional) – The q in the compensation factor. Defaults to 2.0.

• num_classes (int, optional) – The number of classes. Default to 1203 for LVIS v1 dataset.

• eps (float, optional) – The minimal value of divisor to smooth the computation of compensation factor

• reduction (str, optional) – The method that reduces the loss to a scalar. Options are “none”, “mean” and “sum”.

• loss_weight (float, optional) – The weight of the loss. Defaults to 1.0

• return_dict (bool, optional) – Whether return the losses as a dict. Default to True.

forward(cls_score, labels, label_weights=None, avg_factor=None, reduction_override=None)

Forward function.

## Parameters