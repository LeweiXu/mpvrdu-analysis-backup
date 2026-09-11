• Speed up YOLOv3 inference (#5991)

• Release Swin Transformer pre-trained models (#6100)

• Support mixed precision training in YOLOX (#5983)

• Support val workflow in YOLACT (#5986)

• Add script to test torchserve (#5936)

• Support onnxsim with dynamic input shape (#6117)

#### 32.2.3 Bug Fixes

• Fix the function naming errors in model_wrappers (#5975)

• Fix regression loss bug when the input is an empty tensor (#5976)

• Fix scores not contiguous error in centernet_head (#6016)

• Fix missing parameters bug in imshow_bboxes (#6034)

• Fix bug in aug_test of HTC when the length of det_bboxes is 0 (#6088)

• Fix empty proposal errors in the training of some two-stage models (#5941)

• Fix dynamic_axes parameter error in ONNX dynamic shape export (#6104)

• Fix dynamic_shape bug of SyncRandomSizeHook (#6144)

• Fix the Swin Transformer config link error in the configuration (#6172)

#### 32.2.4 Improvements

• Add filter rules in Mosaic transform (#5897)

• Add size divisor in get flops to avoid some potential bugs (#6076)

• Add Chinese translation of docs_zh-CN/tutorials/customize_dataset.md (#5915)

• Add Chinese translation of conventions.md (#5825)

• Add description of the output of data pipeline (#5886)

• Add dataset information in the README file for PanopticFPN (#5996)

• Add extra_repr for DropBlock layer to get details in the model printing (#6140)

• Fix CI out of memory and add PyTorch1.9 Python3.9 unit tests (#5862)

• Fix download links error of some model (#6069)

• Improve the generalization of XML dataset (#5943)

• Polish assertion error messages (#6017)

• Remove opencv-python-headless dependency by albumentations (#5868)

• Check dtype in transform unit tests (#5969)

• Replace the default theme of documentation with PyTorch Sphinx Theme (#6146)

• Update the paper and code fields in the metafile (#6043)

• Support to customize padding value of segmentation map (#6152)

• Support to resize multiple segmentation maps (#5747)