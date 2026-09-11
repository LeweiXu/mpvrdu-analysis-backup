#### 12.4.2 Use hooks implemented in MMCV

If the hook is already implemented in MMCV, you can directly modify the config to use the hook as below

### 4. Example: NumClassCheckHook

We implement a customized hook named NumClassCheckHook to check whether the num_classes in head matches the length of CLASSSES in dataset.

We set it in default_runtime.py.

custom_hooks = [dict(type='NumClassCheckHook')]

#### 12.4.3 Modify default runtime hooks

There are some common hooks that are not registered through custom_hooks, they are

• log_config

• checkpoint_config

• evaluation

• lr_config

• optimizer_config

• momentum_config

In those hooks, only the logger hook has the VERY_LOW priority, others' priority are NORMAL. The above-mentioned tutorials already cover how to modify optimizer_config, momentum_config, and lr_config. Here we reveal how what we can do with log_config, checkpoint_config, and evaluation.

## Checkpoint config

The MMCV runner will use checkpoint_config to initialize CheckpointHook.

checkpoint_config = dict(interval=1)

The users could set max_keep_ckpts to only save only small number of checkpoints or decide whether to store state dict of optimizer by save_optimizer. More details of the arguments are here

## Log config

The log_config wraps multiple logger hooks and enables to set intervals. Now MMCV supports WandbLoggerHook, MlflowLoggerHook, and TensorboardLoggerHook. The detail usages can be found in the doc.

log_config = dict(
    interval=50,
    hooks=[
        dict(type='TextLoggerHook'),
        dict(type='TensorboardLoggerHook')
    ])