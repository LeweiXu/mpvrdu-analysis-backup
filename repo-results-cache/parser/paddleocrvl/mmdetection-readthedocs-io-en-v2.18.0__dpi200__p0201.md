(continued from previous page)

>>> add_gt_as_proposals=False)
>>> self = self.sample(assign_result, bboxes, gt_bboxes, gt_labels)

class mmdet.core.bbox.BboxOverlaps2D(scale=1.0, dtype=None)

2D Overlaps (e.g. IoUs, GIoUs) Calculator.

class mmdet.core.bbox.CenterRegionAssigner(pos_scale, neg_scale, min_pos_iof=0.01, ignore_gt_scale=0.5, foreground_dominate=False, iou_calculator='type': 'BoxOverlaps2D')

Assign pixels at the center region of a bbox as positive.

Each proposals will be assigned with -1, 0, or a positive integer indicating the ground truth index. --1: negative samples - semi-positive numbers: positive sample, index (0-based) of assigned gt

## Parameters

• pos_scale (float) – Threshold within which pixels are labelled as positive.

• neg_scale (float) – Threshold above which pixels are labelled as positive.

• min_pos_iof (float) – Minimum iof of a pixel with a gt to be labelled as positive. Default: 1e-2

• ignore_gt_scale (float) – Threshold within which the pixels are ignored when the gt is labelled as shadowed. Default: 0.5

• foreground_dominate (bool) – If True, the bbox will be assigned as positive when a gt's kernel region overlaps with another's shadowed (ignored) region, otherwise it is set as ignored. Default to False.

assign(bboxes, gt_bboxes, gt_bboxes_ignore=None, gt_labels=None)

Assign gt to bboxes.

This method assigns gts to every bbox (proposal/anchor), each bbox will be assigned with -1, or a semi-positive number. -1 means negative sample, semi-positive number is the index (0-based) of assigned gt.

## Parameters

• bboxes (Tensor) – Bounding boxes to be assigned, shape(n, 4).

• gt_bboxes (Tensor) – Groundtruth boxes, shape (k, 4).

- gt_bboxes_ignore (tensor, optional) – Ground truth bboxes that are labelled as ignored, e.g., crowd boxes in COCO.

• gt_labels (tensor, optional) – Label of gt_bboxes, shape (num_gts,).

Returns The assigned result. Note that shadowed_labels of shape  $ (N, 2) $ is also added as an assign_result attribute. shadowed_labels is a tensor composed of N pairs of anchor_ind, class_label, where N is the number of anchors that lie in the outer region of a gt, anchor_ind is the shadowed anchor index and class_label is the shadowed class label.

Return type AssignResult