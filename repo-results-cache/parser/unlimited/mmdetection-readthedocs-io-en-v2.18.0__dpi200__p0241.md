MMDetection, Release 2.18.0
load_annotations(ann_file)
Load annotation from annotation file.
load_proposals(proposal_file)
Load proposal from proposal file.
pre_ pipeline(results)
Prepare results dict for pipeline.
prepare_test_img(uk)
Get testing data after pipeline.
Parameters idx (int) – Index of data.
Returns Index data after pipeline with new keys introduced by pipeline.
Return testing dict
prepare_train_img(uk)
Get training data and annotations after pipeline.
Parameters idx (int) – Index of data.
Returns Training data and annotation after pipeline with new keys introduced by pipeline.
Return type dict
class mndet.datasets.DeepFashionDataset(_conn_file_pipeline, classes=None, data_nrots=None,
img_prefix=".seg_prefix=None, proposal_file=None,
test_mode=False, filter_empty_gs=True)
class mndet.datasets.DistributedGroupSampler(dataset, samples_per_gpu=1, num_replicas=None,
mkdir=None, seed=0)
Sampler that restricts data loading to a subset of the dataset.
It is especially useful in conjunction with torch.nn.parallel.DistributedDataParallel. In such case, each process can pass a DistributedSampler instance as a DataLoader sampler, and load a subset of the original dataset that is exclusive to it.
Note: Dataset is assumed to be of constant size.
Parameters
- dataset – Dataset used for sampling.
- num_replicas (optional) – Number of processes participating in distributed training.
- rank (optional) – Rank of the current process within num_replicas.
- seed(int, optional) – random seed used to shuffle the sampler if shuffle=True. This number should be identical across all processes in the distributed group. Default: 0.
class mmedt.datasets.DistributedSampler(dataset, num_replicas=None, rank=None, shuffle=True, seed=0)
class mmedt.datasets.GroupSampler(dataset, samples_per_gpu=1)
mmedt.datasets.LVISDataset
alias of mmedt.datasets.lvis.LVISVOSDataset
234
Chapter 38. mmedt.datasets