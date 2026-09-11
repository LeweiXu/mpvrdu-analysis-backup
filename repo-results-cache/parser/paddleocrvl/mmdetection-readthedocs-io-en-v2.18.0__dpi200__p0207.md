• num (int) – Number of samples

• pos_fraction (float) – Fraction of positive samples

• neg_pos_up (int, optional) – Upper bound number of negative and positive samples. Defaults to -1.

• add_gt_as_proposals (bool, optional) – Whether to add ground truth boxes as proposals. Defaults to True.

## random_choice(gallery, num)

Random select some elements from the gallery.

If gallery is a Tensor, the returned indices will be a Tensor; If gallery is a ndarray or list, the returned indices will be a ndarray.

## Parameters

• gallery (Tensor / ndarray / list) – indices pool.

• num (int) – expected sample num.

Returns sampled indices.

Return type Tensor or ndarray

####### class mmdet.core.bbox.RegionAssigner(center_ratio=0.2, ignore_ratio=0.5)

Assign a corresponding gt bbox or background to each bbox.

Each proposals will be assigned with -1, 0, or a positive integer indicating the ground truth index.

• -1: don't care

• 0: negative sample, no assigned gt

• positive integer: positive sample, index (1-based) of assigned gt

## Parameters

• center_ratio – ratio of the region in the center of the bbox to define positive sample.

• ignore_ratio – ratio of the region to define ignore samples.

## assign(mlvl_anchors, mlvl_valid_flags, gt_bboxes, img_meta, featmap_sizes, anchor_scale, anchor_strides, gt_bboxes_ignore=None, gt_labels=None, allowed_border=0)

Assign gt to anchors.

This method assigns a gt bbox to every bbox (proposal/anchor), each bbox will be assigned with -1, 0, or a positive number. -1 means don’t care, 0 means negative sample, positive number is the index (1-based) of assigned gt.

The assignment is done in following steps, and the order matters.

1. Assign every anchor to 0 (negative)

2. (For each gt_bboxes) Compute ignore flags based on ignore_region then assign -1 to anchors w.r.t. ignore flags

3. (For each gt_bboxes) Compute pos flags based on center_region then assign gt_bboxes to anchors w.r.t. pos flags

4. (For each gt_bboxes) Compute ignore flags based on adjacent anchor level then assign -1 to anchors w.r.t. ignore flags

5. Assign anchor outside of image to -1