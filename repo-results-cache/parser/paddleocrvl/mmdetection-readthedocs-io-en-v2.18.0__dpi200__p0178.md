#### 32.24 v1.0rc0 (27/07/2019)

• Implement lots of new methods and components (Mixed Precision Training, HTC, Libra R-CNN, Guided Anchoring, Empirical Attention, Mask Scoring R-CNN, Grid R-CNN (Plus), GHM, GCNet, FCOS, HRNet, Weight Standardization, etc.). Thank all collaborators!

• Support two additional datasets: WIDER FACE and Cityscapes.

• Refactoring for loss APIs and make it more flexible to adopt different losses and related hyper-parameters.

• Speed up multi-gpu testing.

• Integrate all compiling and installing in a single script.

##### 32.25 v0.6.0 (14/04/2019)

• Up to 30% speedup compared to the model zoo.

• Support both PyTorch stable and nightly version.

• Replace NMS and SigmoidFocalLoss with Pytorch CUDA extensions.

#### 32.26 v0.6rc0(06/02/2019)

• Migrate to PyTorch 1.0.

##### 32.27 v0.5.7 (06/02/2019)

• Add support for Deformable ConvNet v2. (Many thanks to the authors and @chengdazhi)

• This is the last release based on PyTorch 0.4.1.

##### 32.28 v0.5.6 (17/01/2019)

• Add support for Group Normalization.

• Unify RPNHead and single stage heads (RetinaHead, SSDHead) with AnchorHead.

##### 32.29 v0.5.5 (22/12/2018)

• Add SSD for COCO and PASCAL VOC.

• Add ResNeXt backbones and detection models.

• Refactoring for Samplers/Assigners and add OHEM.

• Add VOC dataset and evaluation scripts.