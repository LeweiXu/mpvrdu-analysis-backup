class mmdet.datasets.LVISV05Dataset(ann_file, pipeline, classes=None, data_root=None, img_prefix="", seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

evaluate(results, metric='bbox', logger=None, jsonfile_prefix=None, classwise=False, proposal_nums=(100, 300, 1000), iou_thrs=array([0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95]))

Evaluation in LVIS protocol.

## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

• metric (str / list[str]) – Metrics to be evaluated. Options are 'bbox','segm', 'proposal', 'proposal_fast'.

- logger (logging.Logger | str | None) – Logger used for printing related information during evaluation. Default: None.

• jsonfile_prefix (str / None) –

• classwise (bool) – Whether to evaluate the AP for each class.

• proposal_nums (Sequence[int]) – Proposal number used for evaluating recalls, such as recall@100, recall@1000. Default: (100, 300, 1000).

• iou_thrs (Sequence[float]) – IoU threshold used for evaluating recalls. If set to a list, the average recall of all IoUs will also be computed. Default: 0.5.

Returns LVIS style metrics.

Return type dict[str, float]

load_annotations(ann_file)

Load annotation from lvis style annotation file.

Parameters ann_file(str) – Path of annotation file.

Returns Annotation info from LVIS api.

Return type list[dict]

class mmdet.datasets.LVISV1Dataset(ann_file, pipeline, classes=None, data_root=None, img_prefix='', seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

## load_annotations(ann_file)

Load annotation from lvis style annotation file.

Parameters ann_file(str) – Path of annotation file.

Returns Annotation info from LVIS api.

Return type list[dict]

class mmdet.datasets.MultiImageMixDataset(dataset, pipeline, dynamic_scale=None,

skip_type_keys=None)

A wrapper of multiple images mixed dataset.

Suitable for training on multiple images mixed data augmentation like mosaic and mixup. For the augmentation pipeline of mixed image data, the get_indexes method needs to be provided to obtain the image indexes, and you can set skip_flags to change the pipeline running process. At the same time, we provide the dynamic_scale parameter to dynamically change the output image size.