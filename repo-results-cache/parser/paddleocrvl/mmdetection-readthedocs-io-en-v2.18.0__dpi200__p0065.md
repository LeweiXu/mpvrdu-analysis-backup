(continued from previous page)

247.09,
...
219.03,
249.06], # if you have mask labels
'area': 1035.749,
'iscrowd': 0,
'image_id': 1268,
'bbox': [192.81, 224.8, 74.73, 33.43],
'category_id': 16,
'id': 42986
},
...
],
# MMDetection automatically maps the uncontinuous `id` to the continuous label indices.
'categories': [
{ 'id': 1, 'name': 'a'}, { 'id': 3, 'name': 'b'}, { 'id': 4, 'name': 'c'}, { 'id': 16, 'name': 'd'}, { 'id': 17, 'name': 'e' }
]

We use this way to support CityScapes dataset. The script is in cityscapes.py and we also provide the finetuning config.

## Note

1. For instance segmentation datasets, MMDetection only supports evaluating mask AP of dataset in COCO format for now.

2. It is recommended to convert the data offline before training, thus you can still use CocoDataset and only need to modify the path of annotations and the training classes.

#### 9.1.2 Reorganize new data format to middle format

It is also fine if you do not want to convert the annotation format to COCO or PASCAL format. Actually, we define a simple annotation format and all existing datasets are processed to be compatible with it, either online or offline.

The annotation of a dataset is a list of dict, each dict corresponds to an image. There are 3 field filename (relative path), width, height for testing, and an additional field ann for training. ann is also a dict containing at least 2 fields: bboxes and labels, both of which are numpy arrays. Some datasets may provide annotations like crowd/difficult/ignored bboxes, we use bboxes_ignore and labels_ignore to cover them.

Here is an example.

{
    'filename': 'a.jpg',
    'width': 1280,
    'height': 720,
    'ann': {
        'bboxes': <np.ndarray, float32>(n, 4),
        'labels': <np.ndarray, int64>(n, ),
        'bboxes_ignore': <np.ndarray, float32>(k, 4),
        'labels_ignore': <np.ndarray, int64>(k, ) (optional field)
    }
}

(continues on next page)