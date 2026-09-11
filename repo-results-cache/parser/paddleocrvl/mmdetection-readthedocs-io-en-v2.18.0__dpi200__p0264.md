The implementation logic is referred to https://github.com/facebookresearch/detectron2/blob/main/detectron2/data/samplers/grouped_batch_sampler.py

## Parameters

• dataset (object) – The dataset.

• batch_size (int) – When model is DistributedDataParallel, it is the number of training samples on each GPU. When model is DataParallel, it is num_gpus * samples_per_gpu. Default: 1.

• world_size(int, optional) – Number of processes participating in distributed training. Default: None.

• rank (int, optional) – Rank of current process. Default: None.

• seed (int) – Random seed. Default: 0.

- shuffle (bool) – Whether shuffle the indices of a dummy epoch, it should be noted that shuffle can not guarantee that you can generate sequential indices because it needs to ensure that all indices in a batch are in a group. Default: True.

set_epoch(epoch)

Not supported in IterationBased runner.

### 38.4 api_wrappers

class mmdet.datasets.api_wrappers.COCO(*args: Any, **kwargs: Any)

This class is almost the same as official pycocotools package.

It implements some snake case function aliases. So that the COCO class has the same interface as LVIS class.