• Fix bug when using dataset wrappers (#5552)

• Fix a typo error in demo/MMDet_Tutorial.ipynb (#5511)

• Fixing crash in get_root_logger whencfg.log_level is not None (#5521)

• Fix docker version (#5502)

• Fix optimizer parameter error when using IterBasedRunner (#5490)

#### 32.5.4 Improvements

• Add unit tests for MMTracking (#5620)

• Add Chinese translation of documentation (#5718, #5618, #5558, #5423, #5593, #5421, #5408, #5369, #5419, #5530, #5531)

• Update resource limit (#5697)

• Update docstring for InstaBoost (#5640)

• Support key reduction_override in all loss functions (#5515)

• Use repeatdataset to accelerate CenterNet training (#5509)

• Remove unnecessary code in autoassign (#5519)

• Add documentation about init_cfg (#5273)

#### 32.5.5 Contributors

A total of 18 developers contributed to this release. Thanks @OceanPang, @AronLin, @hellock, @Outsider565, @RangiLyu, @ElectronicElephant, @likyoo, @BIGWangYuDong, @hhaAndroid, @noobying, @yyz561, @likyoo, @zeakey, @ZwwWayne, @ChenyangLiu, @johnson-magic, @qingswu, @BuxianChen

##### 32.6 v2.14.0 (29/6/2021)

#### 32.6.1 Highlights

• Add simple_test to dense heads to improve the consistency of single-stage and two-stage detectors

• Revert the test mixins to single image test to improve efficiency and readability

• Add Faster R-CNN and Mask R-CNN config using multi-scale training with 3x schedule

#### 32.6.2 New Features

• Support pretrained models from MoCo v2 and SwAV (#5286)

• Add Faster R-CNN and Mask R-CNN config using multi-scale training with 3x schedule (#5179, #5233)

• Add reduction_override in MSELoss (#5437)

• Stable support of exporting DETR to ONNX with dynamic shapes and batch inference (#5168)

• Stable support of exporting PointRend to ONNX with dynamic shapes and batch inference ( $ #5440 $)