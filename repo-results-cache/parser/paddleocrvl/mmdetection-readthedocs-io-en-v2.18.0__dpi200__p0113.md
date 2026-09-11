arg1,
arg2,
init_cfg=None):
super(FooModel, self).__init__(init_cfg)

(continued from previous page)

• Initialize model by using init_cfg directly in code

import torch.nn as nn
from mmcv.runner import BaseModule
# or directly inherit mmdet models
class FooModel(BaseModule)
    def __init__(self,
                         arg1,
                         arg2,
                         init_cfg=XXX):
            super(FooModel, self).__init__(init_cfg)

• Initialize model by using init_cfg directly in mmcv.Sequential or mmcv.ModuleList code

from mmcv.runner import BaseModule, ModuleList
class FooModel(BaseModule)
    def __init__(self,
                         arg1,
                         arg2,
                         init_cfg=None):
            super(FooModel, self).__init__(init_cfg)
        self.conv1 = ModuleList(init_cfg=XXX)

• Initialize model by using init_cfg in config file

model = dict(
    model = dict(
        type='FooModel',
        arg1=XXX,
        arg2=XXX,
        init_cfg=XXX),
   ...
)