#### 32.15.4 Bug Fixes

• Fix the bug of training ATSS when there is no ground truth boxes (#3702)

• Fix the bug of using Focal Loss when there is num_pos is 0 (#3702)

• Fix the label index mapping in dataset browser (#3708)

• Fix Mask R-CNN training stuck problem when there is no positive rois (#3713)

• Fix the bug of self.rpn_head.test_cfg in RPNTestMixin by using self.rpn_head in rpn head (#3808)

• Fix deprecated Conv2d from mmcv.ops (#3791)

• Fix device bug in RepPoints (#3836)

• Fix SABL validating bug (#3849)

• Use https://download.openmmlab.com/mmcv/dist/index.html for installing MMCV (#3840)

• Fix nonzero in NMS for PyTorch 1.6.0 (#3867)

• Fix the API change bug of PAA (#3883)

• Fix typo in bbox_flip (#3886)

• Fix cv2 import error of ligGL.so.1 in Dockerfile (#3891)

#### 32.15.5 Improvements

• Change to use mmcv.utils.collect_env for collecting environment information to avoid duplicate codes (#3779)

• Update checkpoint file names to v2.0 models in documentation (#3795)

• Update tutorials for changing runtime settings (#3778), modifying loss (#3777)

• Improve the function of simple_test_bboxes in SABL (#3853)

• Convert mask to bool before using it as img's index for robustness and speedup (#3870)

• Improve documentation of modules and dataset customization (#3821)

##### 32.16 v2.4.0 (5/9/2020)

## Highlights

• Fix lots of issues/bugs and reorganize the trouble shooting page

• Support new methods SABL, YOLOv3, and PAA Assign

• Support Batch Inference

• Start to publish mmdet package to PyPI since v2.3.0

• Switch model zoo to download.openmmlab.com

## Backwards Incompatible Changes

• Support Batch Inference (#3564, #3686, #3705): Since v2.4.0, MMDetection could inference model with multiple images in a single GPU. This change influences all the test APIs in MMDetection and downstream code-bases. To help the users migrate their code, we use replace_ImageToTensor (#3686) to convert legacy test data pipelines during dataset initialization.