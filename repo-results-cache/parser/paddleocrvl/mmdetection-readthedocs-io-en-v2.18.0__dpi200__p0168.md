• Add config to runner meta (#3534)

• Add eval-option flag for testing (#3537)

• Add init_eval to evaluation hook (#3550)

• Add include_bkg in ClassBalancedDataset (#3577)

• Using config’s loading in inference_detector (#3611)

• Add ATSS ResNet-101 models in model zoo (#3639)

• Update urls to download.openmmlab.com (#3665)

• Support non-mask training for CocoDataset (#3711)

##### 32.17 v2.3.0 (5/8/2020)

## Highlights

• The CUDA/C++ operators have been moved to mmcv.ops. For backward compatibility mmdet.ops is kept as warppers of mmcv.ops.

• Support new methods CornerNet, DIOU/CIOU loss, and new dataset: LVIS V1

• Provide more detailed colab training tutorials and more complete documentation.

• Support to convert RetinaNet from Pytorch to ONNX.

## Bug Fixes

• Fix the model initialization bug of DetectoS ( $ #3187 $)

• Fix the bug of module names in NASFCOSHead (#3205)

• Fix the filename bug in publish_model.py (#3237)

• Fix the dimensionality bug when inside_flags.any() is False in dense heads (#3242)

• Fix the bug of forgetting to pass flip directions in MultiScaleFlipAug (#3262)

• Fixed the bug caused by default value of stem_channels (#3333)

• Fix the bug of model checkpoint loading for CPU inference (#3318, #3316)

• Fix topk bug when box number is smaller than the expected topk number in ATSSAssigner (#3361)

• Fix the gt priority bug in center_region_assigner.py (#3208)

• Fix NaN issue of iou calculation in iou_loss.py (#3394)

• Fix the bug that iou_thrs is not actually used during evaluation in coco.py (#3407)

• Fix test-time augmentation of RepPoints (#3435)

• Fix runtimeError caused by incontiguous tensor in Res2Net+DCN (#3412)

## New Features

• Support CornerNet (#3036)

• Support DIOU/CIOU loss (#3151)

• Support LVIS V1 dataset (#)

• Support customized hooks in training (#3395)

• Support fp16 training of generalized focal loss (#3410)