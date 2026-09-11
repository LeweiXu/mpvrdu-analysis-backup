• Added sleep(2) in test.py to reduce hanging problem (#2847)

• Support c10::half in CARAFE (#2890)

• Improve documentations (#2918, #2714)

• Use optimizer constructor in mmcv and clean the original implementation in mmdet.core.optimizer (#2947)

##### 32.20 v2.0.0 (6/5/2020)

In this release, we made lots of major refactoring and modifications.

1. Faster speed. We optimize the training and inference speed for common models, achieving up to 30% speedup for training and 25% for inference. Please refer to model zoo for details.

2. Higher performance. We change some default hyperparameters with no additional cost, which leads to a gain of performance for most models. Please refer to compatibility for details.

3. More documentation and tutorials. We add a bunch of documentation and tutorials to help users get started more smoothly. Read it here.

4. Support PyTorch 1.5. The support for 1.1 and 1.2 is dropped, and we switch to some new APIs.

5. Better configuration system. Inheritance is supported to reduce the redundancy of config.

6. Better modular design. Towards the goal of simplicity and flexibility, we simplify some encapsulation while add more other configurable modules like BBoxCoder, IoUCalculator, OptimizerConstructor, RoIHead. Target computation is also included in heads and the call hierarchy is simpler.

7. Support new methods: FSAF and PAFPN (part of PAFPN).

Breaking Changes Models training with MMDetection 1.x are not fully compatible with 2.0, please refer to the compatibility doc for the details and how to migrate to the new version.

## Improvements

• Unify cuda and cpp API for custom ops. (#2277)

• New config files with inheritance. (#2216)

• Encapsulate the second stage into RoI heads. (#1999)

• Refactor GCNet/EmpericalAttention into plugins. (#2345)

• Set low quality match as an option in IoU-based bbox assigners. (#2375)

• Change the codebase’s coordinate system. (#2380)

• Refactor the category order in heads. 0 means the first positive class instead of background now. (#2374)

• Add bbox sampler and assigner registry. (#2419)

• Speed up the inference of RPN. (#2420)

• Add train_cfg and test_cfg as class members in all anchor heads. (#2422)

• Merge target computation methods into heads. (#2429)

• Add bbox coder to support different bbox encoding and losses. (#2480)

• Unify the API for regression loss. (#2156)

• Refactor Anchor Generator. (#2474)

• Make lr an optional argument for optimizers. (#2509)