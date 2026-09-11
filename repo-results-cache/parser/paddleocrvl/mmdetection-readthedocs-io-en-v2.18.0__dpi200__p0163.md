##### 32.13 v2.7.0 (30/11/2020)

• Support new method: DETR, ResNest, Faster R-CNN DC5.

• Support YOLO, Mask R-CNN, and Cascade R-CNN models exportable to ONNX.

#### 32.13.1 New Features

• Support DETR (#4201, #4206)

• Support to link the best checkpoint in training (#3773)

• Support to override config through options in inference.py (#4175)

• Support YOLO, Mask R-CNN, and Cascade R-CNN models exportable to ONNX (#4087, #4083)

• Support ResNeSt backbone (#2959)

• Support unclip border bbox regression (#4076)

• Add tpfp func in evaluating AP (#4069)

• Support mixed precision training of SSD detector with other backbones (#4081)

• Add Faster R-CNN DC5 models (#4043)

#### 32.13.2 Bug Fixes

• Fix bug of gpu_id in distributed training mode (#4163)

• Support Albumentations with version higher than 0.5 (#4032)

• Fix num_classes bug in faster rcnn config (#4088)

• Update code in docs/2_new_data_model.md (#4041)

#### 32.13.3 Improvements

• Ensure DCN offset to have similar type as features in VFNet (#4198)

• Add config links in README files of models (#4190)

• Add tutorials for loss conventions (#3818)

• Add solution to installation issues in 30-series GPUs (#4176)

• Update docker version in get_started.md (#4145)

• Add model statistics and polish some titles in configS README (#4140)

• Clamp neg probability in FreeAnchor (#4082)

• Speed up expanding large images (#4089)

• Fix Pytorch 1.7 incompatibility issues (#4103)

• Update trouble shooting page to resolve segmentation fault (#4055)

• Update aLRP-Loss in project page (#4078)

• Clean duplicated reduce_mean function (#4056)

• Refactor Q&A (#4045)