shuffle=True, seed=0

rank=None, seed=0, shuffle=True

### 38.3 samplers

class mmdet.datasets.samplers.DistributedGroupSampler(dataset, samples_per_gpu=1,

num_replicas=None, rank=None, seed=0

Sampler that restricts data loading to a subset of the dataset.

It is especially useful in conjunction with torch.nn.parallel.DistributedDataParallel. In such case, each process can pass a DistributedSampler instance as a DataLoader sampler, and load a subset of the original dataset that is exclusive to it.

Note: Dataset is assumed to be of constant size.

## Parameters

• dataset – Dataset used for sampling.

• num_replicas (optional) – Number of processes participating in distributed training.

• rank (optional) – Rank of the current process within num_replicas.

• seed (int, optional) – random seed used to shuffle the sampler if shuffle=True. This number should be identical across all processes in the distributed group. Default: 0.

class mmdet.datasets.samplers.DistributedSampler(dataset, num_replicas=None, rank=None,

class mmdet.datasets.samplers.GroupSampler(dataset, samples_per_gpu=1)

class mmdet.datasets.samplers.InfiniteBatchSampler(dataset, batch_size=1, world_size=None,

Similar to BatchSampler warping a DistributedSampler. It is designed iteration-based runners like IterBase-dRunner and yields a mini-batch indices each time.

The implementation logic is referred to https://github.com/facebookresearch/detectron2/blob/main/detectron2/data/samplers/grouped_batch_sampler.py

## Parameters

• dataset (object) – The dataset.

• batch_size (int) – When model is DistributedDataParallel, it is the number of training samples on each GPU. When model is DataParallel, it is num_gpus * samples_per_gpu. Default: 1.

• world_size(int, optional) – Number of processes participating in distributed training. Default: None.

• rank (int, optional) – Rank of current process. Default: None.

• seed (int) – Random seed. Default: 0.

• shuffle (bool) – Whether shuffle the dataset or not. Default: True.

set_epoch(epoch)

Not supported in IterationBased runner.

class mmdet.datasets.samplers.InfiniteGroupBatchSampler(dataset, batch_size=1, world_size=None, rank=None, seed=0, shuffle=True)

Similar to BatchSampler warping a GroupSampler. It is designed for iteration-based runners like  $ \`IterBase-dRunner $ and yields a mini-batch indices each time, all indices in a batch should be in the same group.