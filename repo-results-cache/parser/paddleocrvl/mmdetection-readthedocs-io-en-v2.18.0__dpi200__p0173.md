• Migrate to modules and methods in MMCV. (#2502, #2511, #2569, #2572)

• Support PyTorch 1.5. (#2524)

• Drop the support for Python 3.5 and use F-string in the codebase. (#2531)

## Bug Fixes

• Fix the scale factors for resized images without keeping the aspect ratio. (#2039)

• Check if max_num > 0 before slicing in NMS. (#2486)

• Fix Deformable RoIPool when there is no instance. (#2490)

• Fix the default value of assigned labels. (#2536)

• Fix the evaluation of Cityscapes. (#2578)

## New Features

• Add deep_stem and avg_down option to ResNet, i.e., support ResNetV1d. (#2252)

• Add L1 loss. (#2376)

• Support both polygon and bitmap for instance masks. (#2353, #2540)

• Support CPU mode for inference. (#2385)

• Add optimizer constructor for complicated configuration of optimizers. (#2397, #2488)

• Implement PAFPN. (#2392)

• Support empty tensor input for some modules. (#2280)

• Support for custom dataset classes without overriding it. (#2408, #2443)

• Support to train subsets of coco dataset. (#2340)

• Add iou_calculator to potentially support more IoU calculation methods. (2405)

• Support class wise mean AP (was removed in the last version). (#2459)

• Add option to save the testing result images. (#2414)

• Support MomentumUpdateHook. (#2571)

• Add a demo to inference a single image. (#2605)

##### 32.21 v1.1.0 (24/2/2020)

## Highlights

• Dataset evaluation is rewritten with a unified api, which is used by both evaluation hooks and test scripts.

• Support new methods: CARAFE.

## Breaking Changes

• The new MMDDP inherits from the official DDP, thus the __init__ api is changed to be the same as official DDP.

• The mask_head field in HTC config files is modified.

• The evaluation and testing script is updated.

• In all transforms, instance masks are stored as a numpy array shaped (n, h, w) instead of a list of (h, w) arrays, where n is the number of instances.