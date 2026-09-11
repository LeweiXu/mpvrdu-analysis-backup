mmdet.core.bbox.bbox_flip(bboxes, img_shape, direction='horizontal')

Flip bboxes horizontally or vertically.

Parameters

• bboxes (Tensor) – Shape (..., 4*k)

• img_shape (tuple) – Image shape.

• direction(str) – Flip direction, options are “horizontal”, “vertical”, “diagonal”. Default: “horizontal”

Returns Flipped bboxes.

Return type Tensor

mmdet.core.bbox.bbox_mapping(bboxes, img_shape, scale_factor, flip, flip_direction='horizontal')

Map bboxes from the original image scale to testing scale.

mmdet.core.bbox.bbox_mapping_back(bboxes, img_shape, scale_factor, flip, flip_direction='horizontal')

Map bboxes from testing scale to original image scale.

mmdet.core.bbox.bbox_overlaps(bboxes1, bboxes2, mode='iou', is_aligned=False, eps=1e-06) Calculate overlap between two sets of bboxes.

FP16 Contributed by https://github.com/open-mmlab/mmdetection/pull/4889.. note:

Assume bboxes1 is M x 4, bboxes2 is N x 4, when mode is 'iou', there are some new generated variable when calculating IOU using bbox_overlaps function:
1) is_aligned is False
    area1: M x 1
    area2: N x 1
    lt: M x N x 2
    rb: M x N x 2
    wh: M x N x 2
    overlap: M x N x 1
    union: M x N x 1
    ious: M x N x 1
Total memory:
    S = (9 x N x M + N + M) * 4 Byte,
When using FP16, we can reduce:
    R = (9 x N x M + N + M) * 4 / 2 Byte
    R large than (N + M) * 4 * 2 is always true when N and M >= 1.
    Obviously, N + M <= N * M < 3 * N * M, when N >= 2 and M >= 2,
        N + 1 < 3 * N, when N or M is 1.
Given M = 40 (ground truth), N = 400000 (three anchor boxes in per grid, FPN, R-CNNs),
    R = 275 MB (one times)
A special case (dense detection), M = 512 (ground truth),
    R = 3516 MB = 3.43 GB
When the batch size is B, reduce:

(continues on next page)