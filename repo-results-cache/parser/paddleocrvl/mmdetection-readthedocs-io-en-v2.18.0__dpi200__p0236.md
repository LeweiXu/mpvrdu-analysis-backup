## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

• metric(str / list[str]) – Metrics to be evaluated. Options are 'bbox','segm', 'proposal', 'proposal_fast'.

- logger (logging.Logger | str | None) – Logger used for printing related information during evaluation. Default: None.

- jsonfile_prefix (str / None) – The prefix of json files. It includes the file path and the prefix of filename, e.g., “a/b/prefix”. If not specified, a temp file will be created. Default: None.

• classwise (bool) – Whether to evaluate the AP for each class.

• proposal_nums (Sequence[int]) – Proposal number used for evaluating recalls, such as recall@100, recall@1000. Default: (100, 300, 1000).

• iou_thrs (Sequence[float], optional) – IoU threshold used for evaluating recalls/mAPs. If set to a list, the average of all IoUs will also be computed. If not specified, [0.50, 0.55, 0.60, 0.65, 0.70, 0.75, 0.80, 0.85, 0.90, 0.95] will be used. Default: None.

• metric_items (list[str] | str, optional) – Metric items that will be returned. If not specified, ['AR@100', 'AR@300', 'AR@1000', 'AR_s@1000', 'AR_m@1000', 'AR_l@1000'] will be used when metric == 'proposal', ['mAP','mAP_50','mAP_75','mAP_s','mAP_m','mAP_l'] will be used when metric == 'box' or metric =='segm'.

Returns COCO style evaluation metric.

Return type dict[str, float]

format_results(results, jsonfile_prefix=None, **kwargs)

Format the results to json (standard format for COCO evaluation).

## Parameters

• results (list[tuple | numpy.ndarray]) – Testing results of the dataset.

- jsonfile_prefix (str / None) – The prefix of json files. It includes the file path and the prefix of filename, e.g., “a/b/prefix”. If not specified, a temp file will be created. Default: None.

Returns (result_files, tmp_dir), result_files is a dict containing the json filepaths, tmp_dir is the temporal directory created for saving json files when jsonfile_prefix is not specified.

Return type tuple

## get_ann_info(idx)

Get COCO annotation by index.

Parameters idx (int) – Index of data.

Returns Annotation info of specified index.

Return type dict

get_cat_ids(idx)

Get COCO category ids by index.

Parameters idx (int) – Index of data.

Returns All categories in the image of specified index.

Return type list[int]