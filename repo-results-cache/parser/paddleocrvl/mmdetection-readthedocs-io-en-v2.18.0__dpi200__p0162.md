#### 32.12.2 New Features

• Support Cascade RPN (#1900)

• Support TridentNet (#3313)

#### 32.12.3 Bug Fixes

• Fix bug of show result in async_benchmark (#4367)

• Fix scale factor in MaskTestMixin (#4366)

• Fix but when returning indices in multiclass_nms (#4362)

• Fix bug of empirical attention in resnext backbone error (#4300)

• Fix bug of img_norm_cfg in FCOS-HRNet models with updated performance and models (#4250)

• Fix invalid checkpoint and log in Mask R-CNN models on Cityscapes dataset (#4287)

• Fix bug in distributed sampler when dataset is too small (#4257)

• Fix bug of ‘PAFPN has no attribute extra_convs_on_inputs’ (#4235)

#### 32.12.4 Improvements

• Update model url from aws to aliyun (#4349)

• Update ATSS for PyTorch 1.6+ (#4359)

• Update script to install ruby in pre-commit installation (#4360)

• Delete deprecated mmdet.ops (#4325)

• Refactor hungarian assigner for more general usage in Sparse R-CNN (#4259)

• Handle scipy import in DETR to reduce package dependencies (#4339)

• Update documentation of usages for config options after MMCV (1.2.3) supports overriding list in config (#4326)

• Update pre-train models of faster rcnn trained on COCO subsets (#4307)

• Avoid zero or too small value for beta in Dynamic R-CNN (#4303)

• Add documentation for Pytorch2ONNX (#4271)

• Add deprecated warning FPN arguments (#4264)

• Support returning indices of kept bboxes when using nms (#4251)

• Update type and device requirements when creating tensors GFLHead (#4210)

• Update device requirements when creating tensors in CrossEntropyLoss (#4224)