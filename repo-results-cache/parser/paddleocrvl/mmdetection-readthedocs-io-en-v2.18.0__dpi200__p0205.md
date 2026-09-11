class mmdet.core.bbox.MaxIoUAssigner(pos_iou_thr, neg_iou_thr, min_pos_iou=0.0,

gt_max_assign_all=True, ignore_iof_thr=-1,

ignore_wrt_candidates=True, match_low_quality=True,

gpu_assign_thr=-1, iou_calculator={'type': 'BboxOverlaps2D'}

Assign a corresponding gt bbox or background to each bbox.

Each proposals will be assigned with -1, or a semi-positive integer indicating the ground truth index.

• -1: negative sample, no assigned gt

• semi-positive integer: positive sample, index (0-based) of assigned gt

## Parameters

• pos_iou_thr (float) – IoU threshold for positive bboxes.

• neg_iou_thr (float or tuple) – IoU threshold for negative bboxes.

• min_pos_iou (float) – Minimum iou for a bbox to be considered as a positive bbox. Positive samples can have smaller IoU than pos_iou_thr due to the 4th step (assign max IoU sample to each gt).

- gt_max_assign_all (bool) – Whether to assign all bboxes with the same highest overlap with some gt to that gt.

• ignore_iof_thr (float) – IoF threshold for ignoring bboxes (if gt_bboxes_ignore is specified). Negative values mean not ignoring any bboxes.

• ignore_wrt_candidates (bool) – Whether to compute the iof between bboxes and gt_bboxes_ignore, or the contrary.

• match_low_quality (bool) – Whether to allow low quality matches. This is usually allowed for RPN and single stage detectors, but not allowed in the second stage. Details are demonstrated in Step 4.

- gpu_assign_thr(int) – The upper bound of the number of GT for GPU assign. When the number of gt is above this threshold, will assign on CPU device. Negative values mean not assign on CPU.

## assign(bboxes, gt_bboxes, gt_bboxes_ignore=None, gt_labels=None)

Assign gt to bboxes.

This method assigns a gt bbox to every bbox (proposal/anchor), each bbox will be assigned with -1, or a semi-positive number. -1 means negative sample, semi-positive number is the index (0-based) of assigned gt. The assignment is done in following steps, the order matters.

1. assign every bbox to the background

2. assign proposals whose iou with all gts < neg_iou_thr to 0

3. for each bbox, if the iou with its nearest gt >= pos_iou_thr, assign it to that bbox

4. for each gt bbox, assign its nearest proposals (may be more than one) to itself

## Parameters

• bboxes (Tensor) – Bounding boxes to be assigned, shape(n, 4).

• gt_bboxes (Tensor) – Groundtruth boxes, shape (k, 4).

- gt_bboxes_ignore (Tensor, optional) – Ground truth bboxes that are labelled as ignored, e.g., crowd boxes in COCO.

• gt_labels (Tensor, optional) – Label of gt_bboxes, shape (k, ).