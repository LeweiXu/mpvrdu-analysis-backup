lr_config = dict(
    policy='CosineAnnealing',
    warmup='linear',
    warmup_iters=1000,
    warmup_ratio=1.0 / 10,
    min_lr_ratio=1e-5)

### 12.3 Customize workflow

Workflow is a list of (phase, epochs) to specify the running order and epochs. By default it is set to be

workflow = [('train', 1)]

which means running 1 epoch for training. Sometimes user may want to check some metrics (e.g. loss, accuracy) about the model on the validate set. In such case, we can set the workflow as

[('train', 1), ('val', 1)]

so that 1 epoch for training and 1 epoch for validation will be run iteratively.

## Note:

1. The parameters of model will not be updated during val epoch.

2. Keyword total_epochs in the config only controls the number of training epochs and will not affect the validation workflow.

3. Workflows [('train', 1), ('val', 1)] and [('train', 1)] will not change the behavior of EvalHook because EvalHook is called by after_train_epoch and validation workflow only affect hooks that are called through after_val_epoch. Therefore, the only difference between [('train', 1), ('val', 1)] and [('train', 1)] is that the runner will calculate losses on validation set after each training epoch.

### 12.4 Customize hooks

#### 12.4.1 Customize self-implemented hooks

### 1. Implement a new hook

There are some occasions when the users might need to implement a new hook. MMDetection supports customized hooks in training (\#3395) since v2.3.0. Thus the users could implement a hook directly in mmdet or their mmdet-based codebases and use the hook by only modifying the config in training. Before v2.3.0, the users need to modify the code to get the hook registered before training starts. Here we give an example of creating a new hook in mmdet and using it in training.

from mmcv.runner import HOOKS, Hook
@HOOKS.register_module()
class MyHook(Hook):
def __init__(self, a, b):

(continues on next page)