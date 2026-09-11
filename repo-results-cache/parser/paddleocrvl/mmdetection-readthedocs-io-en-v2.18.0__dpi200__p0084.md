(continued from previous page)

@LOSSES.register_module()
class MyLoss(nn.Module):
    def __init__(self, reduction='mean', loss_weight=1.0):
        super(MyLoss, self).__init__()
        self.reduction = reduction
        self.loss_weight = loss_weight

    def forward(self, pred, target, weight=None, avg_factor=None, reduction_override=None):
        assert reduction_override in (None, 'none','mean','sum')
        reduction = (
            reduction_override if reduction_override else self.reduction)
            loss_bbox = self.loss_weight * my_loss(
                pred, target, weight, reduction=reduction, avg_factor=avg_factor)
            return loss_bbox

Then the users need to add it in the mmdet/models/losses/_init_.py.

from.my_loss import MyLoss, my_loss

Alternatively, you can add

custom_imports=dict(
    imports=['mmdet.models.losses.my_loss'])
)

to the config file and achieve the same goal.

To use it, modify the loss_xxx field. Since MyLoss is for regression, you need to modify the loss_bbox field in the head.

loss_bbox=dict(type='MyLoss', loss_weight=1.0))