(continued from previous page)

return my_optimizer

The default optimizer constructor is implemented here, which could also serve as a template for new optimizer constructor.

#### 12.1.4 Additional settings

Tricks not implemented by the optimizer should be implemented through optimizer constructor (e.g., set parameter-wise learning rates) or hooks. We list some common settings that could stabilize the training or accelerate the training. Feel free to create PR, issue for more settings.

• Use gradient clip to stabilize training: Some models need gradient clip to clip the gradients to stabilize the training process. An example is as below:

optimizer_config = dict(
    _delete_=True,
    grad_clip=dict(max_norm=35, norm_type=2))
)

If your config inherits the base config which already sets the optimizer_config, you might need _delete_=True to override the unnecessary settings. See the config documentation for more details.

• Use momentum schedule to accelerate model convergence: We support momentum scheduler to modify model’s momentum according to learning rate, which could make the model converge in a faster way. Momentum scheduler is usually used with LR scheduler, for example, the following config is used in 3D detection to accelerate convergence. For more details, please refer to the implementation of CyclicLrUpdatet and CyclicMomentumUpdatet.

lr_config = dict(
    policy='cyclic',
    target_ratio=(10, 1e-4),
    cyclic_times=1,
    step_ratio_up=0.4,
)

momentum_config = dict(
    policy='cyclic',
    target_ratio=(0.85 / 0.95, 1),
    cyclic_times=1,
    step_ratio_up=0.4,
)

### 12.2 Customize training schedules

By default we use step learning rate with 1x schedule, this calls StepLRHook in MMCV. We support many other learning rate schedule here, such as CosineAnnealing and Poly schedule. Here are some examples

• Poly schedule:

lr_config = dict(policy='poly', power=0.9, min_lr=1e-4, by_epoch=False)

• ConsineAnnealing schedule: