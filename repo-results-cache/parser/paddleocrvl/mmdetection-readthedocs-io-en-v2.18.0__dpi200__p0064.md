(continued from previous page)

ann_file='path/to/your/val/annotation_data',
img_prefix='path/to/your/val/image_data'),
test=dict(
    type=dataset_type,
    # explicitly add your class names to the field `classes`
    classes=classes,
    ann_file='path/to/your/test/annotation_data',
    img_prefix='path/to/your/test/image_data')
)

# 2. model settings

# explicitly over-write all the `num_classes` field from default 80 to 5.
model = dict(
    roi_head=dict(
        bbox_head=[
            dict(
                type='Shared2FCBBoxHead',
                # explicitly over-write all the `num_classes` field from default 80 to 5.
                num_classes=5),
                dict(
                    type='Shared2FCBBoxHead',
                    # explicitly over-write all the `num_classes` field from default 80 to 5.
                    num_classes=5),
                    dict(
                        type='Shared2FCBBoxHead',
                        # explicitly over-write all the `num_classes` field from default 80 to 5.
                        num_classes=5)
                    ),
                    # explicitly over-write all the `num_classes` field from default 80 to 5.
                    mask_head=dict(num_classes=5)))

### 2. Check the annotations of the customized dataset

Assuming your customized dataset is COCO format, make sure you have the correct annotations in the customized dataset:

1. The length for categories field in annotations should exactly equal the tuple length of classes fields in your config, meaning the number of classes (e.g. 5 in this example).

2. The classes fields in your config file should have exactly the same elements and the same order with the name in categories of annotations. MMDetection automatically maps the uncontinuous id in categories to the continuous label indices, so the string order of name in categories field affects the order of label indices. Meanwhile, the string order of classes in config affects the label text during visualization of predicted bounding boxes.

3. The category_id in annotations field should be valid, i.e., all values in category_id should belong to id in categories.

Here is a valid example of annotations:

'annotations': [
{
'segmentation': [[192.81],

(continues on next page)