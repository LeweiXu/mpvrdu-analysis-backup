#### 32.4.5 Contributors

A total of 14 developers contributed to this release. Thanks @HAOCHENYE, @xiaohu2015, @HsLOL, @zhiqwang, @Adamdad, @shinya7y, @Johnson-Wang, @RangiLyu, @jshilong, @mmeendez8, @AronLin, @BIGWangYuDong, @hhaAndroid, @ZwwWayne

##### 32.5 v2.15.0 (02/8/2021)

#### 32.5.1 Highlights

• Support adding MIM dependencies during pip installation

• Support MobileNetV2 for SSD-Lite and YOLOv3

• Support Chinese Documentation

#### 32.5.2 New Features

• Add function upsample_like (#5732)

• Support to output pdf and epub format documentation (#5738)

• Support and release Cascade Mask R-CNN 3x pre-trained models (#5645)

• Add ignore_index to CrossEntropyLoss (#5646)

• Support adding MIM dependencies during pip installation (#5676)

• Add MobileNetV2 config and models for YOLOv3 (#5510)

• Support COCO Panoptic Dataset (#5231)

• Support ONNX export of cascade models (#5486)

• Support DropBlock with RetinaNet (#5544)

• Support MobileNetV2 SSD-Lite (#5526)

#### 32.5.3 Bug Fixes

• Fix the device of label in multiclass_nms (#5673)

• Fix error of backbone initialization from pre-trained checkpoint in config file (#5603, #5550)

• Fix download links of RegNet pretrained weights (#5655)

• Fix two-stage runtime error given empty proposal (#5559)

• Fix flops count error in DETR (#5654)

• Fix unittest for NumClassCheckHook when it is not used. (#5626)

• Fix description bug of using custom dataset (#5546)

• Fix bug of multiclass_nms that returns the global indices (#5592)

• Fix valid_mask logic error in RPNHead (#5562)

• Fix unit test error of pretrained configs (#5561)

• Fix typo error in anchor_head.py (#5555)