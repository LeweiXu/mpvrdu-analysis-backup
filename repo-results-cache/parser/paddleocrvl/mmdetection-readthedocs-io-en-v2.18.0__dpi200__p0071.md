person bicycle car

Users can set the classes as a file path, the dataset will load it and convert it to a list automatically.

classes = 'path/to/classes.txt'
data = dict(
    train=dict(classes=classes),
    val=dict(classes=classes),
    test=dict(classes=classes))

## Note:

• Before MMDetection v2.5.0, the dataset will filter out the empty GT images automatically if the classes are set and there is no way to disable that through config. This is an undesirable behavior and introduces confusion because if the classes are not set, the dataset only filters the empty GT images when filter_empty_gt=True and test_mode=False. After MMDetection v2.5.0, we decouple the image filtering process and the classes modification, i.e., the dataset will only filter empty GT images when filter_empty_gt=True and test_mode=False, no matter whether the classes are set. Thus, setting the classes only influences the annotations of classes used for training and users could decide whether to filter empty GT images by themselves.

• Since the middle format only has box labels and does not contain the class names, when using CustomDataset, users cannot filter out the empty GT images through config-but-only do this offline.

• Please remember to modify the num_classes in the head when specifying classes in dataset. We implemented NumClassCheckHook to check whether the numbers are consistent since v2.9.0(after PR#4508).

• The features for setting dataset classes and dataset filtering will be refactored to be more user-friendly in the future (depends on the progress).

### 9.4 COCO Panoptic Dataset

Now we support COCO Panoptic Dataset, the format of panoptic annotations is different from COCO format. Both the foreground and the background will exist in the annotation file. The annotation json files in COCO Panoptic format has the following necessary keys:

'images': [
    {
        'file_name': '000000001268.jpg',
        'height': 427,
        'width': 640,
        'id': 1268
    },
   ...
]
'annotations': [
    {
        'filename': '000000001268.jpg',
        'image_id': 1268,
       'segments_info': [
            {

(continues on next page)