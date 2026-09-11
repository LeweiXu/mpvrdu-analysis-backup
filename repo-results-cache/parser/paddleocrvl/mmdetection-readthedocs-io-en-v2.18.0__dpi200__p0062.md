## TUTORIAL 2: CUSTOMIZE DATASETS

### 9.1 Support new data format

To support a new data format, you can either convert them to existing formats (COCO format or PASCAL format) or directly convert them to the middle format. You could also choose to convert them offline (before training by a script) or online (implement a new dataset and do the conversion at training). In MMDetection, we recommend to convert the data into COCO formats and do the conversion offline, thus you only need to modify the config's data annotation paths and classes after the conversion of your data.

#### 9.1.1 Reorganize new data formats to existing format

The simplest way is to convert your dataset to existing dataset formats (COCO or PASCAL VOC).

The annotation json files in COCO format has the following necessary keys:

{
    'images': [
        {
            'file_name': 'COCO_val2014_000000001268.jpg',
            'height': 427,
            'width': 640,
            'id': 1268
        },
       ...
    ],
    'annotations': [
        {
           'segmentation': [[192.81, 247.09,...
                219.03, 249.06]], # if you have mask labels
            'area': 1035.749,
            'iscrowd': 0,
            'image_id': 1268,
            'bbox': [192.81, 224.8, 74.73, 33.43],
            'category_id': 16,
            'id': 42986
        }
    ]
}

(continues on next page)