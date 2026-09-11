## Parameters

• dataset (CustomDataset) – The dataset to be mixed.

• pipeline (Sequence $$ dict $$ ) – Sequence of transform object or config dict to be composed.

• dynamic_scale (tuple[int], optional) – The image scale can be changed dynamically. Default to None.

- skip_type_keys (list[str], optional) – Sequence of type string to be skip pipeline. Default to None.

update_dynamic_scale(dynamic_scale)

Update dynamic_scale. It is called by an external hook.

Parameters dynamic_scale (tuple[int]) – The image scale can be changed dynamically.

update_skip_type_keys(skip_type_keys)

Update skip_type_keys. It is called by an external hook.

Parameters skip_type_keys (list[str], optional) – Sequence of type string to be skip pipeline.

#### class mmdet.datasets.RepeatDataset(dataset, times)

A wrapper of repeated dataset.

The length of repeated dataset will be times larger than the original dataset. This is useful when the data loading time is long but the dataset is small. Using RepeatDataset can reduce the data loading time between epochs.

## Parameters

• dataset (Dataset) – The dataset to be repeated.

• times (int) – Repeat times.

get_cat_ids(idx)

Get category ids of repeat dataset by index.

Parameters idx (int) – Index of data.

Returns All categories in the image of specified index.

Return type list[int]

class mmdet.datasets.VOCDataset(**kwargs)

evaluate(results, metric='mAP', logger=None, proposal_nums=(100, 300, 1000), iou_thr=0.5)

scale_ranges=None)

Evaluate in VOC protocol.

## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

• metric (str / list[str]) – Metrics to be evaluated. Options are'mAP','recall'.

• logger (logging.Logger | str, optional) – Logger used for printing related information during evaluation. Default: None.

• proposal_nums (Sequence[int]) – Proposal number used for evaluating recalls, such as recall@100, recall@1000. Default: (100, 300, 1000).

• iou_thr (float / list[float]) – IoU threshold. Default: 0.5.