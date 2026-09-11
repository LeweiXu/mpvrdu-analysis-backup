},
]

(continued from previous page)

There are two ways to work with custom datasets.

• online conversion

You can write a new Dataset class inherited from CustomDataset, and overwrite two methods load_annotations(self, ann_file) and get_ann_info(self, idx), like CocoDataset and VOCDataset.

## • offline conversion

You can convert the annotation format to the expected format above and save it to a pickle or json file, like pascal_voc.py. Then you can simply use CustomDataset.

#### 9.1.3 An example of customized dataset

Assume the annotation is in a new format in text files. The bounding boxes annotations are stored in text file annotation.txt as the following

#
000001.jpg
1280 720
2
10 20 40 60 1
20 40 50 60 2
#
000002.jpg
1280 720
3
50 20 40 60 2
20 40 30 45 2
30 40 50 60 3

We can create a new dataset in mmdet/datasets/my_dataset.py to load the data.

import mmcv
import numpy as np
from.builder import DATASETS
from.custom import CustomDataset
@DATASETS.register_module()
class MyDataset(CustomDataset):
    CLASSES = ('person', 'bicycle', 'car','motorcycle')
    def load_annotations(self, ann_file):
        ann_list = mmcv.list_from_file(ann_file)

(continues on next page)