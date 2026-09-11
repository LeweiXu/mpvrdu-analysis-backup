- bboxes_ignore (optional): numpy array of shape  $ (k, 4) $

– labels_ignore (optional): numpy array of shape (k, )

- scale_ranges (list[tuple] | None) – Range of scales to be evaluated, in the format [(min1, max1), (min2, max2),...]. A range of (32, 64) means the area range between (32**2, 64**2). Default: None.

• iou_thr (float) – IoU threshold to be considered as matched. Default: 0.5.

• dataset (list[str] | str | None) – Dataset name or dataset classes, there are minor differences in metrics for different datasets, e.g. “voc07”, “imagenet_det”, etc. Default: None.

- logger (logging.Logger | str | None) – The way to print the mAP summary. See mmcv.utils.print_log() for details. Default: None.

• tpfp_fn (Callable / None) – The function used to determine true/false positives. If None, tpfp_default() is used as default unless dataset is 'det' or 'vid' (tpfp_imagenet() in this case). If it is given as a function, then this function is used to evaluate tp & fp. Default None.

• nproc (int) – Processes used for computing TP and FP. Default: 4.

• use_legacy_coordinate (bool) – Whether to use coordinate system in mmdet v1.x, which means width, height should be calculated as 'x2 - x1 + 1' and 'y2 - y1 + 1' respectively. Default: False.

Returns (mAP, [dict, dict,...])

Return type tuple

mmdet.core.evaluation.eval_recalls(gts, proposals, proposal_nums=None, iou_thrs=0.5, logger=None, use_legacy_coordinate=False)

Calculate recalls.

## Parameters

• gts (list [ndarray]) – a list of arrays of shape (n, 4)

• proposals (list [ndarray]) – a list of arrays of shape (k, 4) or (k, 5)

• proposal_nums (int / Sequence[int]) – Top N proposals to be evaluated.

• iou_thrs (float / Sequence[float]) – IoU thresholds. Default: 0.5.

- logger (logging.Logger | str | None) – The way to print the recall summary. See mmcv.utils.print_log() for details. Default: None.

• use_legacy_coordinate (bool) – Whether use coordinate system in mmdet v1.x. “1” was added to both height and width which means w, h should be computed as ‘x2 - x1 + 1’ and ‘y2 - y1 + 1’. Default: False.

Returns recalls of different ious and proposal nums

Return type ndarray

mmdet.core.evaluation.get_classes(dataset)

Get class names of a dataset.

mmdet.core.evaluation.plot_iou_recall(recalls, iou_thrs)

Plot IoU-Recalls curve.

Parameters

• recalls (ndarray or list) – shape (k,)