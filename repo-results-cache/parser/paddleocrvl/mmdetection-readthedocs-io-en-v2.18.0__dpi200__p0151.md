#### 32.2.5 Contributors

A total of 24 developers contributed to this release. Thanks @morkovka1337, @HarborYuan, @guillaumefrd, @guigarfr, @www516717402, @gaotongxiao, @ypwhs, @MartaYang, @shinya7y, @justiceeem, @zhaojinjian0000, @VVsssssk, @aravind-anantha, @wangbo-zhao, @czczup, @whai362, @czczup, @marijnl, @AronLin, @BIG-WangYuDong, @hhaAndroid, @jshilong, @RangiLyu, @ZwwWayne

##### 32.3 v2.16.0 (30/8/2021)

#### 32.3.1 Highlights

• Support Panoptic FPN and Swin Transformer

#### 32.3.2 New Features

• Support Panoptic FPN and release models (#5577, #5902)

• Support Swin Transformer backbone (#5748)

• Release RetinaNet models pre-trained with multi-scale 3x schedule (#5636)

• Add script to convert unlabeled image list to coco format (#5643)

• Add hook to check whether the loss value is valid (#5674)

• Add YOLO anchor optimizing tool (#5644)

• Support export onnx models without post process. (#5851)

• Support classwise evaluation in CocoPanopticDataset (#5896)

• Adapt browse dataset for concatenated datasets. (#5935)

• Add PatchEmbed and PatchMerging with AdaptivePadding (#5952)

#### 32.3.3 Bug Fixes

• Fix unit tests of YOLOX (#5859)

• Fix lose randomness in imshow_det_bboxes (#5845)

• Make output result of ImageToTensor contiguous (#5756)

• Fix inference bug when calling regress_by_class in RoIHead in some cases (#5884)

• Fix bug in CIoU loss where alpha should not have gradient. (#5835)

• Fix the bug that multiscale_output is defined but not used in HRNet (#5887)

• Set the priority of EvalHook to LOW. (#5882)

• Fix a YOLOX bug when applying bbox rescaling in test mode (#5899)

• Fix mosaic coordinate error (#5947)

• Fix dtype of bbox in RandomAffine. (#5930)