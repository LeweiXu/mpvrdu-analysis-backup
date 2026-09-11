# MMDET.DATASETS

### 38.1 datasets

class mmdet.datasets.CityscapesDataset(ann_file, pipeline, classes=None, data_root=None, img_prefix="", seg_prefix=None, proposal_file=None, test_mode=False, filter_empty_gt=True)

evaluate(results, metric='bbox', logger=None, outfile_prefix=None, classwise=False, proposal_nums=(100, 300, 1000), iou_thrs=array([0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95]))

Evaluation in Cityscapes/COCO protocol.

## Parameters

• results (list[list / tuple]) – Testing results of the dataset.

• metric(str / list[str]) – Metrics to be evaluated. Options are 'bbox','segm', 'proposal', 'proposal_fast'.

- logger (logging.Logger | str | None) – Logger used for printing related information during evaluation. Default: None.

• outfile_prefix (str / None) – The prefix of output file. It includes the file path and the prefix of filename, e.g., “a/b/prefix”. If results are evaluated with COCO protocol, it would be the prefix of output json file. For example, the metric is ‘bbox’ and ‘segm’, then json files would be “a/b/prefix.bbox.json” and “a/b/prefix.segm.json”. If results are evaluated with cityscapes protocol, it would be the prefix of output txt/png files. The output files would be png images under folder “a/b/prefix/xxx/” and the file name of images would be written into a txt file “a/b/prefix/xxx_pred.txt”, where “xxx” is the video name of cityscapes. If not specified, a temp file will be created. Default: None.

• classwise (bool) – Whether to evaluate the AP for each class.

• proposal_nums (Sequence[int]) – Proposal number used for evaluating recalls, such as recall@100, recall@1000. Default: (100, 300, 1000).

• iou_thrs (Sequence[float]) – IoU threshold used for evaluating recalls. If set to a list, the average recall of all IoUs will also be computed. Default: 0.5.

Returns COCO style evaluation metric or cityscapes mAP and AP@50.

Return type dict[str, float]

format_results(results, txtfile_prefix=None)

Format the results to txt (standard format for Cityscapes evaluation).

## Parameters