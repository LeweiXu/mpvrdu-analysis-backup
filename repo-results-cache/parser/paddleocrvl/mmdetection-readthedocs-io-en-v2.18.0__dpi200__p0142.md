# COMPATIBILITY OF MMDETECTION 2.X

##### 30.1 MMDetection 2.18.0

#### 30.1.1 DIIHead compatibility

In order to support QueryInst, attn_feats is added into the returned tuple of DIIHead.

##### 30.2 MMDetection 2.14.0

#### 30.2.1 MMCV Version

In order to fix the problem that the priority of EvalHook is too low, all hook priorities have been re-adjusted in 1.3.8, so MMDetection 2.14.0 needs to rely on the latest MMCV 1.3.8 version. For related information, please refer to #1120, for related issues, please refer to #5343.

#### 30.2.2 SSD compatibility

In v2.14.0, to make SSD more flexible to use, PR5291 refactored its backbone, neck and head. The users can use the script tools/model_converters/upgrade_ssd_version.py to convert their models.

python tools/model_converters/upgrade_ssd_version.py ${OLD_MODEL_PATH} ${NEW_MODEL_PATH}

• OLD_MODEL_PATH: the path to load the old version SSD model.

• NEW MODEL PATH: the path to save the converted model weights.

##### 30.3 MMDetection 2.12.0

MMDetection is going through big refactoring for more general and convenient usages during the releases from v2.12.0 to v2.18.0 (maybe longer). In v2.12.0 MMDetection inevitably brings some BC-breakings, including the MMCV dependency, model initialization, model registry, and mask AP evaluation.