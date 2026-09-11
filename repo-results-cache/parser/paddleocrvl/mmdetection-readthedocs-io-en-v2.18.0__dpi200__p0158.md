#### 32.8.4 Improvements

• Use MMCV MODEL_REGISTRY (#5059)

• Unified parameter initialization for more flexible usage (#4750)

• Rename variable names and fix docstring in anchor head (#4883)

• Support training with empty GT in Cascade RPN (#4928)

• Add more details of usage of test_robustness in documentation (#4917)

• Changing to use pycocotools instead of mmpycocotools to fully support Detectron2 and MMDetection in one environment (#4939)

• Update torch serve dockerfile to support dockers of more versions (#4954)

• Add check for training with single class dataset (#4973)

• Refactor transformer and DETR Head (#4763)

• Update FPG model zoo (#5079)

• More accurate mask AP of small/medium/large instances (#4898)

#### 32.8.5 Bug Fixes

• Fix bug in mean_ap.py when calculating mAP by 11 points (#4875)

• Fix error when key meta is not in old checkpoints (#4936)

• Fix hanging bug when training with empty GT in VFNet, GFL, and FCOS by changing the place of reduce_mean (#4923, #4978, #5058)

• Fix asynchronized inference error and provide related demo (#4941)

• Fix IoU losses dimensionality unmatch error (#4982)

• Fix torch.randperm whtn using PyTorch 1.8 (#5014)

• Fix empty bbox error in mask_head when using CARAFE (#5062)

• Fix supplement_mask bug when there are zero-size RoIs (#5065)

• Fix testing with empty rois in RoI Heads (#5081)

##### 32.9 v2.11.0 (01/4/2021)

## Highlights

• Support new method: Localization Distillation for Object Detection

• Support Pytorch2ONNX with batch inference and dynamic shape

## New Features

• Support Localization Distillation for Object Detection (#4758)

• Support Pytorch2ONNX with batch inference and dynamic shape for Faster-RCNN and mainstream one-stage detectors ( $ #4796 $)

## Improvements

• Support batch inference in head of RetinaNet (#4699)