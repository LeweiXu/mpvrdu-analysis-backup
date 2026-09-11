### 2. Add the optimizer to registry

To find the above module defined above, this module should be imported into the main namespace at first. There are two options to achieve it.

• Modify mmdet/core/optimizer/__init__.py to import it.

The newly defined module should be imported in mmdet/core/optimizer/__init__.py so that the registry will find the new module and add it:

from.my_optimizer import MyOptimizer

• Use custom_imports in the config to manually import it

custom_imports = dict(imports=['mmdet.core.optimizer.my_optimizer'], allow_failed_imports=False)

The module mmdet.core.optimizer.my_optimizer will be imported at the beginning of the program and the class MyOptimizer is then automatically registered. Note that only the package containing the class MyOptimizer should be imported. mmdet.core.optimizer.my_optimizer.MyOptimizer cannot be imported directly.

Actually users can use a totally different file directory structure using this importing method, as long as the module root can be located in PYTHONPATH.

### 3. Specify the optimizer in the config file

Then you can use MyOptimizer in optimizer field of config files. In the config, the optimizers are defined by the field optimizer like the following:

optimizer = dict(type='SGD', lr=0.02, momentum=0.9, weight_decay=0.0001)

To use your own optimizer, the field can be changed to

optimizer = dict(type='MyOptimizer', a=a_value, b=b_value, c=c_value)

#### 12.1.3 Customize optimizer constructor

Some models may have some parameter-specific settings for optimization, e.g. weight decay for BatchNorm layers. The users can do those fine-grained parameter tuning through customizing optimizer constructor.

from mmcv.utils import build_from_cfg
from mmcv.runner.optimizer import OPTIMIZER_BUILDERS, OPTIMIZERS
from mmdet.utils import get_root_logger
from.my_optimizer import MyOptimizer
@OPTIMIZER_BUILDERS.register_module()
class MyOptimizerConstructor(object):
    def __init__(self, optimizer_cfg, paramwise_cfg=None):
        def __call__(self, model):

(continues on next page)