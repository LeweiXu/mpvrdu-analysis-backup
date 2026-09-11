• Update the PyTorch and CUDA version in the docker file. (#1615)

• Raise a warning when specifying --validate in non-distributed training. (#1624, #1651)

• Beautify the mAP printing. (#1614)

• Add pre-commit hook. (#1536)

• Add the argument in_channels to backbones. (#1475)

• Add lots of docstrings and unit tests, thanks to @Erotemic. (#1603, #1517, #1506, #1505, #1491, #1479, #1477, #1475, #1474)

• Add support for multi-node distributed test when there is no shared storage. (#1399)

• Optimize Dockerfile to reduce the image size. (#1306)

• Update new results of HRNet. (#1284, #1182)

• Add an argument no_norm_on_lateral in FPN. (#1240)

• Test the compiling in CI. (#1235)

• Move docs to a separate folder. (#1233)

• Add a jupyter notebook demo. (#1158)

• Support different type of dataset for training. (#1133)

• Use int64_t instead of long in cuda kernels. (#1131)

• Support unsquare RoIs for bbox and mask heads. (#1128)

• Manually add type promotion to make compatible to PyTorch 1.2. (#1114)

• Allowing validation dataset for computing validation loss. (#1093)

• Use.scalar_type() instead of.type() to suppress some warnings. (#1070)

## New Features

• Add an option --with_ap to compute the AP for each class. (#1549)

• Implement “FreeAnchor: Learning to Match Anchors for Visual Object Detection”. (#1391)

• Support Albumentations for augmentations in the data pipeline. (#1354)

• Implement “FoveaBox: Beyond Anchor-based Object Detector”. (#1339)

• Support horizontal and vertical flipping. (#1273, #1115)

• Implement “RepPoints: Point Set Representation for Object Detection”. (#1265)

• Add test-time augmentation to HTC and Cascade R-CNN. (#1251)

• Add a COCO result analysis tool. (#1228)

• Add Dockerfile. (#1168)

• Add a webcam demo. (#1155, #1150)

• Add FLOPs counter. (#1127)

• Allow arbitrary layer order for ConvModule. (#1078)