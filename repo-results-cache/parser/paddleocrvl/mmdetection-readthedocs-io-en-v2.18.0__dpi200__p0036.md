# 2: TRAIN WITH CUSTOMIZED DATASETS

In this note, you will know how to inference, test, and train predefined models with customized datasets. We use the balloon dataset as an example to describe the whole process.

The basic steps are as below:

1. Prepare the customized dataset

2. Prepare a config

3. Train, test, inference models on the customized dataset.

### 6.1 Prepare the customized dataset

There are three ways to support a new dataset in MMDetection:

1. reorganize the dataset into COCO format.

2. reorganize the dataset into a middle format.

3. implement a new dataset.

Usually we recommend to use the first two methods which are usually easier than the third.

In this note, we give an example for converting the data into COCO format.

Note: MMDetection only supports evaluating mask AP of dataset in COCO format for now. So for instance segmentation task users should convert the data into coco format.

#### 6.1.1 COCO annotation format

The necessary keys of COCO format for instance segmentation is as below, for the complete details, please refer here.

{
    "images": [image],
    "annotations": [annotation],
    "categories": [category]
}

image = {
    "id": int,
    "width": int,
    "height": int,
}

(continues on next page)