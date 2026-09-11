MMDetection, Release 2.18.0
13.3 Tweaking loss
Tweaking a loss is more related with step 2, 4, 5, and most modifications can be specified in the config. Here we take Focal Loss (FL) as an example. The following code sniper are the construction method and config of FL respectively, they are actually one to one correspondence.
@LOSSES.register_module()
class FocalLoss(nn.Module):
    def __init__(self,
    use_sigmoid=True,
    gamma=2.0,
    alpha=0.25,
    reduction='mean',
    loss_weight=1.0):
loss_cls=dict(
    type='FocalLoss',
    use_sigmoid=True,
    gamma=2.0,
    alpha=0.25,
    loss_weight=1.0)
13.3.1 Tweaking hyper-parameters (step 2)
gamma and beta are two hyper-parameters in the Focal Loss. Say if we want to change the value of gamma to be 1.5 and alpha to be 0.5, then we can specify them in the config as follows:
loss_cls=dict(
    type='FocalLoss',
    use_sigmoid=True,
    gamma=1.5,
    alpha=0.5,
    loss_weight=1.0)
13.3.2 Tweaking the way of reduction (step 3)
The default way of reduction is mean for FL. Say if we want to change the reduction from mean to sum, we can specify it in the config as follows:
loss_cls=dict(
    type='FocalLoss',
    use_sigmoid=True,
    gamma=2.0,
    alpha=0.25,
    loss_weight=1.0,
    reduction='sum')
88
Chapter 13. Tutorial 6: Customize Losses