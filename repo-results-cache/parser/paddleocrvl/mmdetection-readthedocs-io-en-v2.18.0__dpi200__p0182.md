2. Reduce the learning rate: the learning rate might be too large due to some reasons, e.g., change of batch size. You can rescale them to the value that could stably train the model.

3. Extend the warmup iterations: some models are sensitive to the learning rate at the start of the training. You can extend the warmup iterations, e.g., change the warmup_iters from 500 to 1000 or 2000.

4. Add gradient clipping: some models require gradient clipping to stabilize the training process. The default of grad_clip is None, you can add gradient clippint to avoid gradients that are too large, i.e., set optimizer_config=dict(_delete_=True, grad_clip=dict(max_norm=35, norm_type=2)) in your config file. If your config does not inherit from any basic config that contains optimizer_config=dict(grad_clip=None), you can simply add optimizer_config=dict(grad_clip=dict(max_norm=35, norm_type=2)).

## • 'GPU out of memory"

1. There are some scenarios when there are large amounts of ground truth boxes, which may cause OOM during target assignment. You can set  $ gpu\_assign\_thr=N $ in the config of assigner thus the assigner will calculate box overlaps through CPU when there are more than N GT boxes.

2. Set with_cp=True in the backbone. This uses the sublinear strategy in PyTorch to reduce GPU memory cost in the backbone.

3. Try mixed precision training using the following examples in config/fp16. The loss_scale might need further tuning for different models.

• "RuntimeError: Expected to have finished reduction in the prior iteration before starting a new one"

1. This error indicates that your module has parameters that were not used in producing loss. This phenomenon may be caused by running different branches in your code in DDP mode.

2. You can set find_unused_parameters = True in the config to solve the above problems or find those unused parameters manually.

### 33.4 Evaluation

## • COCO Dataset, AP or AR = -1

1. According to the definition of COCO dataset, the small and medium areas in an image are less than 1024 (32*32), 9216 (96*96), respectively.

2. If the corresponding area has no object, the result of AP and AR will set to -1.