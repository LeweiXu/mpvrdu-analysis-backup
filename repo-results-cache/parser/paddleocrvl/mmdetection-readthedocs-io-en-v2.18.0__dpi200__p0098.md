## TUTORIAL 7: FINETUNING MODELS

Detectors pre-trained on the COCO dataset can serve as a good pre-trained model for other datasets, e.g., CityScapes and KITTI Dataset. This tutorial provides instruction for users to use the models provided in the Model Zoo for other datasets to obtain better performance.

There are two steps to finetune a model on a new dataset.

• Add support for the new dataset following Tutorial 2: Customize Datasets.

• Modify the config as will be discussed in this tutorial.

Take the finetuning process on Cityscapes Dataset as an example, the users need to modify five parts in the config.

### 14.1 Inherit base config

To release the burden and reduce bugs in writing the whole configs, MMDetection V2.0 supports inheriting configs from multiple existing configs. To finetune a Mask RCNN model, the new config needs to inherit _base_/models/mask_rcnn_r50_fpn.py to build the basic structure of the model. To use the Cityscapes Dataset, the new config can also simply inherit _base_/datasets/cityscapes_instance.py. For runtime settings such as training schedules, the new config needs to inherit _base_/default_runtime.py. This config is in the config directory and the users can also choose to write the whole contents rather than use inheritance.

_base_ = [
    '.../_base_/models/mask_rcnn_r50_fpn.py',
    '.../_base_/datasets/cityscapes_instance.py',
    '.../_base_/default_runtime.py'
]

### 14.2 Modify head

Then the new config needs to modify the head according to the class numbers of the new datasets. By only changing num_classes in the roi_head, the weights of the pre-trained models are mostly reused except the final prediction head.

model = dict(
    pretrained=None,
    roi_head=dict(
        bbox_head=dict(
            type='Shared2FCBBoxHead',
            in_channels=256,
            fc_out_channels=1024,
            roi_feat_size=7,
        )
)

(continues on next page)