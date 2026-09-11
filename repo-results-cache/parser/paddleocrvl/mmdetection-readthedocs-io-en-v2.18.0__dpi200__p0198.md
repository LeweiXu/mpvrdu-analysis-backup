### Return type torch.Tensor

mmdet.core.anchor.anchor_inside_flags(flat_anchors, valid_flags, img_shape, allowed_border=0) Check whether the anchors are inside the border.

## Parameters

• flat_anchors (torch.Tensor) – Flatten anchors, shape (n, 4).

• valid_flags (torch.Tensor) – An existing valid flags of anchors.

• img_shape (tuple(int)) – Shape of current image.

• allowed_border (int, optional) – The border to allow the valid anchor. Defaults to 0.

Returns Flags indicating whether the anchors are inside a valid range.

Return type torch.Tensor

mmdet.core.anchor.calc_region(bbox, ratio, featmap_size=None)

Calculate a proportional bbox region.

The bbox center are fixed and the new h' and w' is h * ratio and w * ratio.

Parameters

• bbox (Tensor) – Bboxes to calculate regions, shape (n, 4).

• ratio (float) – Ratio of the output region.

• featmap_size (tuple) – Feature map size used for clipping the boundary.

Returns x1, y1, x2, y2

Return type tuple

mmdet.core.anchor.images_to_levels(target, num_levels)

Convert targets by image to targets by feature level.

[target_img0, target_img1] -> [target_level0, target_level1,...]

### 37.2 bbox

class mmdet.core.bbox.AssignResult(num_gts, gt_inds, max_overlaps, labels=None) Stores assignments between predicted and truth boxes.

## num_gts

the number of truth boxes considered when computing this assignment

Type int

## gt_inds

for each predicted box indicates the 1-based index of the assigned truth box. 0 means unassigned and -1 means ignore.

Type LongTensor

## max_overlaps

the iou between the predicted box and its assigned truth box.

Type FloatTensor

## labels

If specified, for each predicted box indicates the category label of the assigned truth box.