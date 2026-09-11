##### 32.15 v2.5.0 (5/10/2020)

#### 32.15.1 Highlights

• Support new methods: YOLACT, CentripetalNet.

• Add more documentations for easier and more clear usage.

#### 32.15.2 Backwards Incompatible Changes

FP16 related methods are imported from mmcv instead of mmdet. (#3766, #3822) Mixed precision training utilised in mmdet.core.fp16 are moved to mmcv.runner, including force_fp32, auto_fp16, wrap_fp16_model, and Fp16OptimizerHook. A deprecation warning will be raised if users attempt to import those methods from mmdet.core.fp16, and will be finally removed in V2.10.0.

[0, N-1] represents foreground classes and N indicates background classes for all models. (#3221) Before v2.5.0, the background label for RPN is 0, and N for other heads. Now the behavior is consistent for all models. Thus self.background_labels in dense_heads is removed and all heads use self.num_classes to indicate the class index of background labels. This change has no effect on the pre-trained models in the v2.x model zoo, but will affect the training of all models with RPN heads. Two-stage detectors whose RPN head uses softmax will be affected because the order of categories is changed.

Only call get_subset_by_classes when test_mode=True and self.filter_empty_gt=True (#3695) Function get_subset_by_classes in dataset is refactored and only filters out images when test_mode=True and self.filter_empty_gt=True. In the original implementation, get_subset_by_classes is not related to the flag self.filter_empty_gt and will only be called when the classes is set during initialization no matter test_mode is True or False. This brings ambiguous behavior and potential bugs in many cases. After v2.5.0, if filter_empty_gt=False, no matter whether the classes are specified in a dataset, the dataset will use all the images in the annotations. If filter_empty_gt=True and test_mode=True, no matter whether the classes are specified, the dataset will call `get_subset_by_classes` to check the images and filter out images containing no GT boxes. Therefore, the users should be responsible for the data filtering/cleaning process for the test dataset.

#### 32.15.3 New Features

• Test time augmentation for single stage detectors (#3844, #3638)

• Support to show the name of experiments during training (#3764)

• Add Shear, Rotate, Translate Augmentation (#3656, #3619, #3687)

• Add image-only transformations including Constrast, Equalize, Color, and Brightness. (#3643)

• Support YOLACT (#3456)

• Support CentripetalNet (#3390)

• Support PyTorch 1.6 in docker (#3905)