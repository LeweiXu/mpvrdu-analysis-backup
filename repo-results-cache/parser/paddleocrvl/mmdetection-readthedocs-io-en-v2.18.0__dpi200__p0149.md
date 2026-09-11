#### 32.1.4 Improvements

• Unify the interface of stuff head and panoptic head (#6308)

• Polish readme (#6243)

• Add code-spell pre-commit hook and fix a typo (#6306)

• Fix typo (\#6245, \#6190)

• Fix sampler unit test (#6284)

• Fix forward_dummy of YOLACT to enable get_flops (#6079)

• Fix link error in the config documentation (#6252)

• Adjust the order to beautify the document (#6195)

#### 32.1.5 Refactors

• Refactor one-stage get_bboxes logic (#5317)

• Refactor ONNX export of One-Stage models ( $ #6003 $,  $ #6369 $)

• Refactor dense_head and speedup (#6268)

• Migrate to use prior_generator in training of dense heads (#6315)

#### 32.1.6 Contributors

A total of 18 developers contributed to this release. Thanks @Boyden, @onnkeat, @st9007a, @vealocia, @yhcao6, @DapangpangX, @yellowdolphin, @cclauss, @kennymckormick, @pingguokiller, @collinzrj, @AndreaPi, @AronLin, @BIGWangYuDong, @hhaAndroid, @jshilong, @RangiLyu, @ZwwWayne

##### 32.2 v2.17.0 (28/9/2021)

#### 32.2.1 Highlights

• Support PVT and PVTv2

• Support SOLO

• Support large scale jittering and New Mask R-CNN baselines

• Speed up YOLOv3 inference

#### 32.2.2 New Features

• Support PVT and PVTv2 (#5780)

• Support SOLO (#5832)

• Support large scale jittering and New Mask R-CNN baselines (#6132)

• Add a general data structure for the results of models (#5508)

• Added a base class for one-stage instance segmentation (#5904)