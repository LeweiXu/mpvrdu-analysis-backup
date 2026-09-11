separate_eval=False,
pipeline=train_pipeline

(continued from previous page)

2. In case the dataset you want to concatenate is different, you can concatenate the dataset config like the following.

dataset_A_train = dict()
dataset_B_train = dict()

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

If the concatenated dataset is used for test or evaluation, this manner also supports evaluating each dataset separately.

3. We also support the define ConcatDataset explicitly as the following.

dataset_A_val = dict()
dataset_B_val = dict()

data = dict(
    imgs_per_gpu=2,
    workers_per_gpu=2,
    train=dataset_A_train,
    val=dict(
        type='ConcatDataset',
        datasets=[dataset_A_val, dataset_B_val],
        separate_eval=False)
)

This manner allows users to evaluate all the datasets as a single one by setting separate_eval=False.

## Note:

1. The option separate_eval=False assumes the datasets use self.data_Infos during evaluation. Therefore, COCO datasets do not support this behavior since COCO datasets do not fully rely on self.data_Infos for evaluation. Combining different types of datasets and evaluating them as a whole is not tested thus is not suggested.

2. Evaluating ClassBalancedDataset and RepeatDataset is not supported thus evaluating concatenated datasets of these types is also not supported.

A more complex example that repeats Dataset_A and Dataset_B by N and M times, respectively, and then concatenates the repeated datasets is as the following.

dataset_A_train = dict(
    type='RepeatDataset',
    times=N,
)

(continues on next page)