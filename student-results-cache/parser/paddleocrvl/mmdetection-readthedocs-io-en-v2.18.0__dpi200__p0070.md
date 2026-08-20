(continued from previous page)

dataset=dict(
    type='Dataset_A',
   ...
    pipeline=train_pipeline
)

dataset_A_val = dict(
   ...
    pipeline=test_pipeline
)

dataset_A_test = dict(
   ...
    pipeline=test_pipeline
)

dataset_B_train = dict(
    type='RepeatDataset',
    times=M,
    dataset=dict(
        type='Dataset_B',
       ...
        pipeline=train_pipeline
    )
)

data = dict(
    imgs_per_gpu=2,
    workers_per_gpu=2,
    train = [
        dataset_A_train,
        dataset_B_train
    ],
    val = dataset_A_val,
    test = dataset_A_test
)

### 9.3 Modify Dataset Classes

With existing dataset types, we can modify the class names of them to train subsets of the annotations. For example, if you want to train only three classes of the current dataset, you can modify the classes of the dataset. The dataset will filter out the ground truth boxes of other classes automatically.

classes = ('person', 'bicycle', 'car')
data = dict(
    train=dict(classes=classes),
    val=dict(classes=classes),
    test=dict(classes=classes))

MMDetection V2.0 also supports reading the classes from a file, which is common in real applications. For example, assume the classes.txt contains the name of classes as the following.