#### 32.3.4 Improvements

• Add Chinese version of data_pipeline and (#5662)

• Support to remove state dicts of EMA when publishing models. (#5858)

• Refactor the loss function in HTC and SCNet (#5881)

• Use warnings instead of logger.warning (#5540)

• Use legacy coordinate in metric of VOC (#5627)

• Add Chinese version of customize_losses (#5826)

• Add Chinese version of model_zoo (#5827)

#### 32.3.5 Contributors

A total of 19 developers contributed to this release. Thanks @ypwhs, @zywvvd, @collinzrj, @OceanPang, @ddonatien, @@haotian-liu, @viibridges, @Muyun99, @guigarfr, @zhaojinjian0000, @jbwang1997, @wangbo-zhao, @xvjiarui, @RangiLyu, @jshilong, @AronLin, @BIGWangYuDong, @hhaAndroid, @ZwwWayne

##### 32.4 v2.15.1 (11/8/2021)

#### 32.4.1 Highlights

• Support YOLOX

#### 32.4.2 New Features

• Support YOLOX(#5756, #5758, #5760, #5767, #5770, #5774, #5777, #5808, #5828, #5848)

#### 32.4.3 Bug Fixes

• Update correct SSD models. (#5789)

• Fix casting error in mask structure (#5820)

• Fix MMCV deployment documentation links. (#5790)

#### 32.4.4 Improvements

• Use dynamic MMCV download link in TorchServe dockerfile (#5779)

• Rename the function upsample_like to interpolate_as for more general usage (#5788)