• iou\_thrs (ndarray or list) – same shape as *recalls*

mmdet.core.evaluation.plot\_num\_recall(*recalls*, *proposal\_nums*) Plot Proposal\_num-Recalls curve.

## **Parameters**

- recalls (ndarray or list) shape (k,)
- proposal\_nums (ndarray or list) same shape as *recalls*

mmdet.core.evaluation.print\_map\_summary(*mean\_ap*, *results*, *dataset=None*, *scale\_ranges=None*, *logger=None*)

Print mAP and results of each class.

A table will be printed to show the gts/dets/recall/AP of each class and the mAP.

#### **Parameters**

- mean\_ap (float) Calculated from *eval\_map()*.
- results (list[dict]) Calculated from *eval\_map()*.
- dataset (list[str] | str | None) Dataset name or dataset classes.
- scale\_ranges (list[tuple] | None) Range of scales to be evaluated.
- logger (logging.Logger | str | None) The way to print the mAP summary. See *mmcv.utils.print\_log()* for details. Default: None.

mmdet.core.evaluation.print\_recall\_summary(*recalls*, *proposal\_nums*, *iou\_thrs*, *row\_idxs=None*, *col\_idxs=None*, *logger=None*)

Print recalls in a table.

## **Parameters**

- recalls (ndarray) calculated from *bbox\_recalls*
- proposal\_nums (ndarray or list) top N proposals
- iou\_thrs (ndarray or list) iou thresholds
- row\_idxs (ndarray) which rows(proposal nums) to print
- col\_idxs (ndarray) which cols(iou thresholds) to print
- logger (logging.Logger | str | None) The way to print the recall summary. See *mmcv.utils.print\_log()* for details. Default: None.

# **37.6 post\_processing**

mmdet.core.post\_processing.fast\_nms(*multi\_bboxes*, *multi\_scores*, *multi\_coeffs*, *score\_thr*, *iou\_thr*, *top\_k*, *max\_num=- 1*)

Fast NMS in [YOLACT.](https://arxiv.org/abs/1904.02689)

Fast NMS allows already-removed detections to suppress other detections so that every instance can be decided to be kept or discarded in parallel, which is not possible in traditional NMS. This relaxation allows us to implement Fast NMS entirely in standard GPU-accelerated matrix operations.

## **Parameters**

• multi\_bboxes (Tensor) – shape (n, #class\*4) or (n, 4)