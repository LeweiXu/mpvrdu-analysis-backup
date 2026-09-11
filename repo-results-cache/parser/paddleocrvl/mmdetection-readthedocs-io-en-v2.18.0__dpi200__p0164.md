##### 32.14 v2.6.0 (1/11/2020)

• Support new method: VarifocalNet.

• Refactored documentation with more tutorials.

#### 32.14.1 New Features

• Support GIoU calculation in BboxOverlaps2D, and re-implement giou_loss using bbox_overlaps (#3936)

• Support random sampling in CPU mode (#3948)

• Support VarifocalNet (\#3666, \#4024)

#### 32.14.2 Bug Fixes

• Fix SABL validating bug in Cascade R-CNN (#3913)

• Avoid division by zero in PAA head when num_pos=0 (#3938)

• Fix temporary directory bug of multi-node testing error (#4034, #4017)

• Fix --show-dir option in test script (#4025)

• Fix GA-RetinaNet r50 model url (#3983)

• Update code in docs and fix broken urls (#3947)

#### 32.14.3 Improvements

• Refactor pytorch2onnx API into mmdet.core.export and use generate_inputs_and_wrap_model for pytorch2onnx (#3857, #3912)

• Update RPN upgrade scripts for v2.5.0 compatibility (#3986)

• Use mmcv tensor2imgs (#4010)

• Update test robustness (\#4000)

• Update trouble shooting page (#3994)

• Accelerate PAA training speed (#3985)

• Support batch_size > 1 in validation (#3966)

• Use RoIAlign implemented in MMCV for inference in CPU mode (#3930)

• Documentation refactoring (#4031)