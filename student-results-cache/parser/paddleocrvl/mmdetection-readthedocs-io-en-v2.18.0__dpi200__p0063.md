],
'categories': [
    {'id': 0, 'name': 'car'},
]

(continued from previous page)

There are three necessary keys in the json file:

• images: contains a list of images with their information like file_name, height, width, and id.

• annotations: contains the list of instance annotations.

• categories: contains the list of categories names and their ID.

After the data pre-processing, there are two steps for users to train the customized new dataset with existing format (e.g. COCO format):

1. Modify the config file for using the customized dataset.

2. Check the annotations of the customized dataset.

Here we give an example to show the above two steps, which uses a customized dataset of 5 classes with COCO format to train an existing Cascade Mask R-CNN R50-FPN detector.

### 1. Modify the config file for using the customized dataset

There are two aspects involved in the modification of config file:

1. The data field. Specifically, you need to explicitly add the classes fields in data.train, data.val and data.test.

2. The num_classes field in the model part. Explicitly over-write all the num_classes from default value (e.g., 80 in COCO) to your classes number.

In config/my_custom_config.py:

# the new config inherits the base config to highlight the necessary modification
_base_ = './cascade_mask_rcnn_r50_fpn_1x_coco.py'

# 1. dataset settings
dataset_type = 'CocoDataset'
classes = ('a', 'b', 'c', 'd', 'e')
data = dict(
    samples_per_gpu=2,
    workers_per_gpu=2,
    train=dict(
        type=dataset_type,
        # explicitly add your class names to the field `classes`
        classes=classes,
        ann_file='path/to/your/train/annotation_data',
        img_prefix='path/to/your/train/image_data'),
        val=dict(
            type=dataset_type,
            # explicitly add your class names to the field `classes`
            classes=classes,

(continues on next page)