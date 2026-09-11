• classes(str / Sequence[str], optional)−Specify classes to load. If is None, cls.CLASSES will be used. Default: None.

• data_root (str, optional) – Data root for ann_file, img_prefix, seg_prefix, proposal_file if specified.

• test_mode (bool, optional) – If set True, annotation will not be loaded.

• filter_empty_gt (bool, optional) – If set true, images without bounding boxes of the dataset’s classes will be filtered out. This option only works when test_mode=False, i.e., we never filter images during tests.

evaluate(results, metric='mAP', logger=None, proposal_nums=(100, 300, 1000), iou_thr=0.5)

scale_ranges=None)

Evaluate the dataset.

## Parameters

• results (list) – Testing results of the dataset.

• metric (str / list[str]) – Metrics to be evaluated.

- logger (logging.Logger | None | str) – Logger used for printing related information during evaluation. Default: None.

• proposal_nums (Sequence[int]) – Proposal number used for evaluating recalls, such as recall@100, recall@1000. Default: (100, 300, 1000).

• iou_thr (float / list[float]) – IoU threshold. Default: 0.5.

- scale_ranges (list[tuple] / None) – Scale ranges for evaluating mAP. Default: None.

## format_results(results, **kwargs)

Place holder to format result to dataset specific output.

## get_ann_info(idx)

Get annotation by index.

Parameters idx (int) – Index of data.

Returns Annotation info of specified index.

Return type dict

## get_cat_ids(idx)

Get category ids by index.

Parameters idx (int) – Index of data.

Returns All categories in the image of specified index.

Return type list[int]

## classmethod get_classes(classes=None)

Get class names of current dataset.

Parameters classes (Sequence $$ str $$  | str | None) – If classes is None, use default CLASSES defined by builtin dataset. If classes is a string, take it as a file name. The file contains the name of classes where each line contains one class name. If classes is a tuple or list, override the CLASSES defined by the dataset.

Returns Names of categories of the dataset.

Return type tuple[str] or list[str]