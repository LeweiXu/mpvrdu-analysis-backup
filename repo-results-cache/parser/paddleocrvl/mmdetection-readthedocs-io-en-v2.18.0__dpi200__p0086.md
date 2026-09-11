# TUTORIAL 5: CUSTOMIZE RUNTIME SETTINGS

### 12.1 Customize optimization settings

#### 12.1.1 Customize optimizer supported by Pytorch

We already support to use all the optimizers implemented by PyTorch, and the only modification is to change the optimizer field of config files. For example, if you want to use ADAM (note that the performance could drop a lot), the modification could be as the following.

optimizer = dict(type='Adam', lr=0.0003, weight_decay=0.0001)

To modify the learning rate of the model, the users only need to modify the lr in the config of optimizer. The users can directly set arguments following the API doc of PyTorch.

#### 12.1.2 Customize self-implemented optimizer

### 1. Define a new optimizer

A customized optimizer could be defined as following.

Assume you want to add a optimizer named MyOptimizer, which has arguments a, b, and c. You need to create a new directory named mmdet/core/optimizer. And then implement the new optimizer in a file, e.g., in mmdet/core/optimizer/my_optimizer.py:

from.registry import OPTIMIZERS
from torch.optim import Optimizer
@OPTIMIZERS.register_module()
class MyOptimizer(Optimizer):
    def __init__(self, a, b, c):