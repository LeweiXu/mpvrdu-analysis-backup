• Add batch dimension in second stage of Faster-RCNN (#4785)

• Support batch inference in bbox coder (#4721)

• Add check for ann_ids in COCODataset to ensure it is unique (#4789)

• support for showing the FPN results (#4716)

• support dynamic shape for grid_anchor (#4684)

• Move pycocotools version check to when it is used (#4880)

## Bug Fixes

• Fix a bug of TridentNet when doing the batch inference (#4717)

• Fix a bug of Pytorch2ONNX in FASF (#4735)

• Fix a bug when show the image with float type (#4732)

##### 32.10 v2.10.0 (01/03/2021)

#### 32.10.1 Highlights

• Support new methods: FPG

• Support ONNX2TensorRT for SSD, FSAF, FCOS, YOLOv3, and Faster R-CNN.

#### 32.10.2 New Features

• Support ONNX2TensorRT for SSD, FSAF, FCOS, YOLOv3, and Faster R-CNN (#4569)

• Support Feature Pyramid Grids (FPG) (#4645)

• Support video demo (#4420)

• Add seed option for sampler (#4665)

• Support to customize type of runner (#4570, #4669)

• Support synchronizing BN buffer in EvalHook (#4582)

• Add script for GIF demo (#4573)

#### 32.10.3 Bug Fixes

• Fix ConfigDict AttributeError and add Colab link (#4643)

• Avoid crash in empty gt training of GFL head (#4631)

• Fix iou_thrs bug in RPN evaluation (#4581)

• Fix syntax error of config when upgrading model version (#4584)