#### 32.10.4 Improvements

• Refactor unit test file structures (#4600)

• Refactor nms config (#4636)

• Get loading pipeline by checking the class directly rather than through config strings (#4619)

• Add doctests for mask target generation and mask structures (#4614)

• Use deep copy when copying pipeline arguments (#4621)

• Update documentations (#4642, #4650, #4620, #4630)

• Remove redundant code calling import_modules_from_strings (#4601)

• Clean deprecated FP16 API (#4571)

• Check whether CLASSES is correctly initialized in the initialization of XMLDataset (#4555)

• Support batch inference in the inference API (#4462, #4526)

• Clean deprecated warning and fix ‘meta’ error (#4695)

##### 32.11 v2.9.0 (01/02/2021)

#### 32.11.1 Highlights

• Support new methods: SCNet, Sparse R-CNN

• Move train_cfg and test_cfg into model in config

• Support to visualize results based on prediction quality

#### 32.11.2 New Features

• Support SCNet (#4356)

• Support Sparse R-CNN (#4219)

• Support evaluate mAP by multiple IoUs (#4398)

• Support concatenate dataset for testing (#4452)

• Support to visualize results based on prediction quality (#4441)

• Add ONNX simplify option to Pytorch2ONNX script (#4468)

• Add hook for checking compatibility of class numbers in heads and datasets (#4508)