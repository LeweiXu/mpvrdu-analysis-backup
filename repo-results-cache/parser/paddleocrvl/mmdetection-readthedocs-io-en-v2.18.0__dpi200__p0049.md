If you are building an entirely new method that does not share the structure with any of the existing methods, you may create a folder xxx_rcnn under config.

Please refer to mmcv for detailed documentation.

### 8.3 Config Name Style

We follow the below style to name config files. Contributors are advised to follow the same style.

{model}_[model setting]_[backbone]_[neck]_[norm setting]_[misc]_[gpu x batch_per_gpu]_→[schedule]_[dataset}

{xxx} is required field and [yyy] is optional.

• {model}: model type like faster_rcnn, mask_rcnn, etc.

• [model setting]: specific setting for some model, like without_semantic for htc, moment for reppoints, etc.

• {backbone}: backbone type like r50 (ResNet-50), x101 (ResNeXt-101).

• {neck}: neck type like fpn, pafpn, nasfpn, c4.

• [norm_setting]: bn (Batch Normalization) is used unless specified, other norm layer type could be gn (Group Normalization), syncbn (Synchronized Batch Normalization). gn-head/gn-neck indicates GN is applied in head/neck only, while gn-all means GN is applied in the entire model, e.g. backbone, neck, head.

• [misc]: miscellaneous setting/plugins of model, e.g. dconv, gcb, attention, albu, mstrain.

• [gpu x batch_per_gpu]: GPUs and samples per GPU, 8x2 is used by default.

• {schedule}: training schedule, options are 1x, 2x, 20e, etc. 1x and 2x means 12 epochs and 24 epochs respectively. 20e is adopted in cascade models, which denotes 20 epochs. For 1x/2x, initial learning rate decays by a factor of 10 at the 8/16th and 11/22th epochs. For 20e, initial learning rate decays by a factor of 10 at the 16th and 19th epochs.

• {dataset}: dataset like coco, cityscapes, voc_0712, wider_face.

### 8.4 Deprecated train_cfg/test_cfg

The train_cfg and test_cfg are deprecated in config file, please specify them in the model config. The original config structure is as below.

# deprecated
model = dict(
    type=...,
)
train_cfg=dict(
   ...
)
test_cfg=dict(
   ...
)

The migration example is as below.