• Support RandomFlip with horizontal/vertical/diagonal direction (#3608): Since v2.4.0, MMDetection supports horizontal/vertical/diagonal flip in the data augmentation. This influences bounding box, mask, and image transformations in data augmentation process and the process that will map those data back to the original format.

• Migrate to use mmlvis and mmpycocotools for COCO and LVIS dataset (#3727). The APIs are fully compatible with the original lvis and pycocotools. Users need to uninstall the existing pycocotools and lvis packages in their environment first and install mmlvis & mmpycocotools.

## Bug Fixes

• Fix default mean/std for onnx (#3491)

• Fix coco evaluation and add metric items (#3497)

• Fix typo for install.md (#3516)

• Fix atss when sampler per gpu is 1 (\#3528)

• Fix import of fuse conv bn (#3529)

• Fix bug of gaussian_target, update unittest of heatmap (#3543)

• Fixed VOC2012 evaluate (#3553)

• Fix scale factor bug of rescale (#3566)

• Fix with xxx attributes in base detector (#3567)

• Fix boxes scaling when number is 0 (#3575)

• Fix rfp check when neck config is a list (#3591)

• Fix import of fuse conv bn in benchmark.py (#3606)

• Fix webcam demo (#3634)

• Fix typo and itemize issues in tutorial (#3658)

• Fix error in distributed training when some levels of FPN are not assigned with bounding boxes (#3670)

• Fix the width and height orders of stride in valid flag generation (#3685)

• Fix weight initialization bug in Res2Net DCN (#3714)

• Fix bug in OHEMSampler (#3677)

## New Features

• Support Cutout augmentation (#3521)

• Support evaluation on multiple datasets through ConcatDataset (#3522)

• Support PAA assign #(3547)

• Support eval metric with pickle results (#3607)

• Support YOLOv3 (#3083)

• Support SABL (#3603)

• Support to publish to Pypi in github-action (#3510)

• Support custom imports (\#3641)

## Improvements

• Refactor common issues in documentation (#3530)

• Add pytorch 1.6 to CI config (#3532)