• Fix the bug of returning None when no gt bboxes are in the original image in RandomCrop. Fix the bug that misses to handle gt_bboxes_ignore, gt_label_ignore, and gt_masks_ignore in RandomCrop, MinIoURandomCrop and Expand modules. (#2810)

• Fix bug of base_channels of regnet (#2917)

• Fix the bug of logger when loading pre-trained weights in base detector (#2936)

## New Features

• Add IoU models (#2666)

• Add colab demo for inference

• Support class agnostic nms (#2553)

• Add benchmark gathering scripts for development only (#2676)

• Add mmdet-based project links (#2736, #2767, #2895)

• Add config dump in training (#2779)

• Add ClassBalancedDataset (#2721)

• Add res2net backbone (#2237)

• Support RegNetX models (#2710)

• Use mmcv.FileClient to support different storage backends (#2712)

• Add ClassBalancedDataset (#2721)

• Code Release: Prime Sample Attention in Object Detection (CVPR 2020) (#2626)

• Implement NASFCOS (#2682)

• Add class weight in CrossEntropyLoss (#2797)

• Support LVIS dataset (#2088)

• Support GRoIE (#2584)

## Improvements

• Allow different x and y strides in anchor heads. (#2629)

• Make FSAF loss more robust to no gt (#2680)

• Compute pure inference time instead (#2657) and update inference speed (#2730)

• Avoided the possibility that a patch with 0 area is cropped. (#2704)

• Add warnings when deprecated imgs_per_gpu is used. (#2700)

• Add a mask rcnn example for config (#2645)

• Update model zoo (#2762, #2866, #2876, #2879, #2831)

• Add ori_filename to img_metas and use it in test show-dir (#2612)

• Use img_fields to handle multiple images during image transform (#2800)

• Add upsample_cfg support in FPN (#2787)

• Add ['img'] as default img_fields for back compatibility (#2809)

• Rename the pretrained model from open-mmlab://resnet50_caffe and open-mmlab://resnet50_caffe_bgr to open-mmlab://detectron/resnet50_caffe and open-mmlab://detectron2/resnet50_caffe. (#2832)