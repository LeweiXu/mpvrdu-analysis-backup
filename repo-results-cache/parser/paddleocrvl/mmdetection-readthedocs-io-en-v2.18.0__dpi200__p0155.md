#### 32.6.3 Bug Fixes

• Fix size mismatch bug in multiclass_nms (#4980)

• Fix the import path of MultiScaleDeformableAttention (#5338)

• Fix errors in config of GCNet ResNext101 models (#5360)

• Fix Grid-RCNN error when there is no bbox result (#5357)

• Fix errors in onnx_export of bbox_head when setting reg_class_agnostic (#5468)

• Fix type error of AutoAssign in the document (#5478)

• Fix web links ending with.md (#5315)

#### 32.6.4 Improvements

• Add simple_test to dense heads to improve the consistency of single-stage and two-stage detectors (#5264)

• Add support for mask diagonal flip in TTA (#5403)

• Revert the test_mixins to single image test to improve efficiency and readability (#5249)

• Make YOLOv3 Neck more flexible (#5218)

• Refactor SSD to make it more general (#5291)

• Refactor anchor_generator and point_generator (#5349)

• Allow to configure out the mask_head of the HTC algorithm (#5389)

• Delete deprecated warning in FPN (#5311)

• Move model.pretrained to model.backbone.init_cfg (#5370)

• Make deployment tools more friendly to use (#5280)

• Clarify installation documentation (#5316)

• Add ImageNet Pretrained Models docs (#5268)

• Add FAQ about training loss=nan solution and COCO AP or AR = -1 (# 5312, #5313)

• Change all weight links of http to https (#5328)

##### 32.7 v2.13.0 (01/6/2021)

#### 32.7.1 Highlights

• Support new methods: CenterNet, Seesaw Loss, MobileNetV2