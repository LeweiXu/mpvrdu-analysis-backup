## TUTORIAL 6: CUSTOMIZE LOSSES

MMDetection provides users with different loss functions. But the default configuration may be not applicable for different datasets or models, so users may want to modify a specific loss to adapt the new situation.

This tutorial first elaborates the computation pipeline of losses, then gives some instructions about how to modify each step. The modification can be categorized as tweaking and weighting.

### 13.1 Computation pipeline of a loss

Given the input prediction and target, as well as the weights, a loss function maps the input tensor to the final loss scalar. The mapping can be divided into four steps:

1. Set the sampling method to sample positive and negative samples.

2. Get element-wise or sample-wise loss by the loss kernel function.

3. Weighting the loss with a weight tensor element-wisely.

4. Reduce the loss tensor to a scalar.

5. Weighting the loss with a scalar.

### 13.2 Set sampling method (step 1)

For some loss functions, sampling strategies are needed to avoid imbalance between positive and negative samples.

For example, when using CrossEntropyLoss in RPN head, we need to set RandomSampler in train_cfg

train_cfg=dict(
  rpn=dict(
    sampler=dict(
      type='RandomSampler',
      num=256,
      pos_fraction=0.5,
      neg_pos_ub=-1,
      add_gt_as_proposals=False)
  )

For some other losses which have positive and negative sample balance mechanism such as Focal Loss, GHMC, and QualityFocalLoss, the sampler is no more necessary.