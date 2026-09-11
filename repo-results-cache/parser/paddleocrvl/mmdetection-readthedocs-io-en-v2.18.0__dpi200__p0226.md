class mmdet.core.evaluation.EvalHook(dataloader, start=None, interval=1, by_epoch=True, save_best=None, rule=None, test_fn=None, greater_keys=None, less_keys=None, out_dir=None, file_client_args=None, **eval_kwargs)

mmdet.core.mask.split_combined_polys(polys, poly_lens, polys_per_mask)

Split the combined 1-D polys into masks.

A mask is represented as a list of polys, and a poly is represented as a 1-D array. In dataset, all masks are concatenated into a single 1-D tensor. Here we need to split the tensor into original representations.

## Parameters

• polys (list) – a list (length = image num) of 1-D tensors

• poly_lens (list) – a list (length = image num) of poly length

• polys_per_mask (list) – a list (length = image num) of poly number of each mask

Returns a list (length = image num) of list (length = mask num) of list (length = poly num) of numpy array.

Return type list

### 37.5 evaluation

class mmdet.core.evaluation.DistEvalHook(dataloader, start=None, interval=1, by_epoch=True,

mmdet.core.evaluation.average_precision(recalls, precisions, mode='area')

Calculate average precision (for single or multiple scales).

## Parameters

• recalls (ndarray) – shape (num_scales, num_dets) or (num_dets,)

• precisions (ndarray) – shape (num_scales, num_dets) or (num_dets,)

• mode (str) – ‘area’ or ‘11points’, ‘area’ means calculating the area under precision-recall curve, ‘11points’ means calculating the average precision of recalls at  $ [0, 0.1, \ldots, 1] $

Returns calculated average precision

Return type float or ndarray

mmdet.core.evaluation.eval_map(det_results, annotations, scale_ranges=None, iou_thr=0.5, dataset=None,

Evaluate mAP of a dataset.

## Parameters

• det_results (list[list]) – [[cls1_det, cls2_det,...],...]. The outer list indicates images, and the inner list indicates per-class detected bboxes.

• annotations (list[dict]) – Ground truth annotations where each item of the list indicates an image. Keys of annotations are:

- bboxes: numpy array of shape  $ (n, 4) $

- labels: numpy array of shape  $ (n, $