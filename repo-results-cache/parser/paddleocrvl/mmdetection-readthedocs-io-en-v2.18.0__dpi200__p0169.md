• Support to convert RetinaNet from Pytorch to ONNX (#3075)

## Improvements

• Support to process ignore boxes in ATSS assigner (#3082)

• Allow to crop images without ground truth in RandomCrop (#3153)

• Enable the Accuracy module to set threshold (#3155)

• Refactoring unit tests (\#3206)

• Unify the training settings of to_float32 and norm_cfg in RegNets config (#3210)

• Add colab training tutorials for beginners (#3213, #3273)

• Move CUDA/C++ operators into mmcv.ops and keep mmdet.ops as warppers for backward compatibility (#3232)(#3457)

• Update installation scripts in documentation (#3290) and dockerfile (#3320)

• Support to set image resize backend (#3392)

• Remove git hash in version file (#3466)

• Check mmcv version to force version compatibility (#3460)

##### 32.18 v2.2.0 (1/7/2020)

## Highlights

• Support new methods: DetectoRS, PointRend, Generalized Focal Loss, Dynamic R-CNN

## Bug Fixes

• Fix FreeAnchor when no gt in image (#3176)

• Clean up deprecated usage of register_module() (#3092, #3161)

• Fix pretrain bug in NAS FCOS (#3145)

• Fix num_classes in SSD (#3142)

• Fix FCOS warmup (#3119)

• Fix rstrip in tools/publish_model.py

• Fix flip_ratio default value in RandomFLip pipeline (#3106)

• Fix cityscapes eval with ms_rcnn (#3112)

• Fix RPN softmax ( $ #3056 $)

• Fix filename of LVIS@v0.5 (#2998)

• Fix nan loss by filtering out-of-frame gt\_bboxes in COCO (#2999)

• Fix bug in FSAF (#3018)

• Add FocalLoss num_classes check (#2964)

• Fix PISA Loss when there are no gts (#2992)

• Avoid nan in iou_calculator (#2975)

• Prevent possible bugs in loading and transforms caused by shallow copy (#2967)

## New Features