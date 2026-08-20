#### 32.7.2 New Features

• Support paper Objects as Points (#4602)

• Support paper Seesaw Loss for Long-Tailed Instance Segmentation (CVPR 2021) (#5128)

• Support MobileNetV2 backbone and inverted residual block (#5122)

• Support MIM (#5143)

• ONNX exportation with dynamic shapes of CornerNet (#5136)

• Add mask_soft config option to allow non-binary masks (#4615)

• Add PWC metafile (#5135)

#### 32.7.3 Bug Fixes

• Fix YOLOv3 FP16 training error (#5172)

• Fix Cascade R-CNN TTA test error when det_bboxes length is 0 (#5221)

• Fix iou_thr variable naming errors in VOC recall calculation function (#5195)

• Fix Faster R-CNN performance dropped in ONNX Runtime (#5197)

• Fix DETR dict changed error when using python 3.8 during iteration (#5226)

#### 32.7.4 Improvements

• Refactor ONNX export of two stage detector (#5205)

• Replace MMDetection’s EvalHook with MMCV’s EvalHook for consistency (#4806)

• Update RoI extractor for ONNX (#5194)

• Use better parameter initialization in YOLOv3 head for higher performance (#5181)

• Release new DCN models of Mask R-CNN by mixed-precision training (#5201)

• Update YOLOv3 model weights (#5229)

• Add DetectoS ResNet-101 model weights (#4960)

• Discard bboxes with sizes equals to min_bbox_size (#5011)

• Remove duplicated code in DETR head (#5129)

• Remove unnecessary object in class definition (#5180)

• Fix doc link (#5192)