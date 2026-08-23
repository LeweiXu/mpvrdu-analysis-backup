MMDetection, Release 2.18.0
- iou_thrs (ndarray or list) – same shape as recalls
mmdet.core.evaluation.plot_num_recall(recalls, proposal_nums)
Plot Proposal_num-Recalls curve.
Parameters
- recalls (ndarray or list) – shape (k,)
- proposal_nums (ndarray or list) – same shape as recalls
mmdet.core.evaluation.print_map_summary(mean_ap, results, dataset=None, scale_ranges=None, logger=None)
Print mAP and results of each class.
A table will be printed to show the gts/dets/recall/AP of each class and the mAP.
Parameters
- mean_ap (float) – Calculated from eval_map().
- results (list[dict]) – Calculated from eval_map().
- dataset (list[str] / str / None) – Dataset name or dataset classes.
- scale_ranges (list[tuple] / None) – Range of scales to be evaluated.
- logger (logging.Logger / str / None) – The way to print the mAP summary. See mmcv.utils.print_log() for details. Default: None.
mmdet.core.evaluation.print_recall_summary(recalls, proposal_nums, iou_thrs, row_idxs=None, col_idxs=None, logger=None)
Print recalls in a table.
Parameters
- recalls (ndarray) – calculated from bbox_recalls
- proposal_nums (ndarray or list) – top N proposals
- iou_thrs (ndarray or list) – iou thresholds
- row_idxs (ndarray) – which rows(proposal nums) to print
- col_idxs (ndarray) – which cols(iou thresholds) to print
- logger (logging.Logger / str / None) – The way to print the recall summary. See mmcv.utils.print_log() for details. Default: None.
37.6 post_processing
mmdet.core.post_processing.fast_nms(multi_bboxes, multi_scores, multi_coeffs, score_thr, iou_thr, top_k, max_num=-1)
Fast NMS in YOLACT.
Fast NMS allows already-removed detections to suppress other detections so that every instance can be decided to be kept or discarded in parallel, which is not possible in traditional NMS. This relaxation allows us to implement Fast NMS entirely in standard GPU-accelerated matrix operations.
Parameters
- multi_bboxes (Tensor) - shape (n, #class*4) or (n, 4)
37.6. post_processing
221