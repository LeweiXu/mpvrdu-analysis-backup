load_annotations(ann_file)
Load annotation from annotation file.

load_proposals(proposal_file)
Load proposal from proposal file.

pre_pipeline(results)
Prepare results dict for pipeline.

prepare_test_img(idx)
Get testing data after pipeline.

Parameters idx (int) – Index of data.
Returns Testing data after pipeline with new keys introduced by pipeline.

Return type dict

prepare_train_img(idx)
Get training data and annotations after pipeline.

Parameters idx (int) – Index of data.
Returns Training data and annotation after pipeline with new keys introduced by pipeline.

Return type dict

class mmdet.datasets.DeepFashionDataset(ann_file, pipeline, classes=None, data_root=None, img_prefix='', seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

class mmdet.datasets.DistributedGroupSampler(dataset, samples_per_gpu=1, num_replicas=None, rank=None, seed=0)

Sampler that restricts data loading to a subset of the dataset.

It is especially useful in conjunction with torch.nn.parallel.DistributedDataParallel. In such case, each process can pass a DistributedSampler instance as a DataLoader sampler, and load a subset of the original dataset that is exclusive to it.

Note: Dataset is assumed to be of constant size.

## Parameters

• dataset – Dataset used for sampling.

• num_replicas (optional) – Number of processes participating in distributed training.

• rank (optional) – Rank of the current process within num_replicas.

• seed (int, optional) – random seed used to shuffle the sampler if shuffle=True. This number should be identical across all processes in the distributed group. Default: 0.

class mmdet.datasets.DistributedSampler(dataset, num_replicas=None, rank=None, shuffle=True, seed=0)

class mmdet.datasets.GroupSampler(dataset, samples_per_gpu=1)

mmdet.datasets.LVISDataset

alias of mmdet.datasets.lvis.LVISV05Dataset