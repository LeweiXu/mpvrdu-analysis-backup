#### 9.2.1 Repeat dataset

We use RepeatDataset as wrapper to repeat the dataset. For example, suppose the original dataset is Dataset_A, to repeat it, the config looks like the following

dataset_A_train = dict(
    type='RepeatDataset',
    times=N,
    dataset=dict(  # This is the original config of Dataset_A
        type='Dataset_A',
       ...
        pipeline=train_pipeline
    )
)

#### 9.2.2 Class balanced dataset

We use ClassBalancedDataset as wrapper to repeat the dataset based on category frequency. The dataset to repeat needs to instantiate function self.get_cat_ids(idx) to support ClassBalancedDataset. For example, to repeat Dataset_A with oversample_thr=1e-3, the config looks like the following

dataset_A_train = dict(
    type='ClassBalancedDataset',
    oversample_thr=1e-3,
    dataset=dict(  # This is the original config of Dataset_A
        type='Dataset_A',
       ...
        pipeline=train_pipeline
    )
)

You may refer to source code for details.

#### 9.2.3 Concatenate dataset

There are three ways to concatenate the dataset.

1. If the datasets you want to concatenate are in the same type with different annotation files, you can concatenate the dataset config like the following.

dataset_A_train = dict(
    type='Dataset_A',
    ann_file = ['anno_file_1', 'anno_file_2'],
    pipeline=train_pipeline
)

If the concatenated dataset is used for test or evaluation, this manner supports to evaluate each dataset separately. To test the concatenated datasets as a whole, you can set separate_eval=False as below.

dataset_A_train = dict(
    type='Dataset_A',
    ann_file = ['anno_file_1', 'anno_file_2'],

(continues on next page)