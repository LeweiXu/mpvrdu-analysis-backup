(continued from previous page)

}
},
...
]

evaluate(results, metric='PQ', logger=None, jsonfile_prefix=None, classwise=False, **kwargs)

Evaluation in COCO Panoptic protocol.

## Parameters

• results (list[dict]) – Testing results of the dataset.

• metric (str / list[str]) – Metrics to be evaluated. Only support ‘PQ’ at present. ‘pq’ will be regarded as ‘PQ.

- logger (logging.Logger | str | None) – Logger used for printing related information during evaluation. Default: None.

- jsonfile_prefix (str / None) – The prefix of json files. It includes the file path and the prefix of filename, e.g., “a/b/prefix”. If not specified, a temp file will be created. Default: None.

• classwise (bool) – Whether to print classwise evaluation results. Default: False.

Returns COCO Panoptic style evaluation metric.

Return type dict[str, float]

evaluate_pan_json(result_files, outfile_prefix, logger=None, classwise=False)

Evaluate PQ according to the panoptic results json file.

## get_ann_info(idx)

Get COCO annotation by index.

Parameters idx (int) – Index of data.

Returns Annotation info of specified index.

Return type dict

## load_annotations(ann_file)

Load annotation from COCO Panoptic style annotation file.

Parameters ann_file(str) – Path of annotation file.

Returns Annotation info from COCO api.

Return type list[dict]

results2json(results, outfile_prefix)

Dump the panoptic results to a COCO panoptic style json file.

## Parameters

• results (dict) – Testing results of the dataset.

• outfile_prefix (str) – The filename prefix of the json files. If the prefix is “somepath/xxx”, the json files will be named “somepath/xxx.panoptic.json”

## Returns

str]: The key is ‘panoptic’ and the value is corresponding filename.

Return type dict[str]