## Turn 1 — document page 229 (rank 1 of 20)

mmdet.core.post_processing.fast_nms(multi_bboxes, multi_scores, multi_coeffs, score_thr, iou_thr, top_k, max_num=-1)
Fast NMS in YOLACT.
Fast NMS allows already-removed detections to suppress other detections so that every instance can be decided to be kept or discarded in parallel, which is not possible in traditional NMS. This relaxation allows us to implement Fast NMS entirely in standard GPU-accelerated matrix operations.
Parameters
- multi_bboxes (Tensor) - shape (n, #class*4) or (n, 4)

## Turn 2 — document page 454 (rank 2 of 20)

This page is an index of MMDetection, Release 2.18.0. It lists functions, classes, and methods with their locations in the code. The entry for `fast_nms()` is found at line 221 in the module `mmdet.core.post_processing`. This confirms the existence of the `fast_nms` function in MMDetection, but does not specify which paper or model uses it.

## Turn 3 — document page 270 (rank 3 of 20)

This page describes the `aug_test` and `merge_aug_results` functions for CenterNet and CornerNet detectors in MMDetection. It also defines the `CornerNet` class, stating that it is the implementation of the paper "CornerNet: Detecting Objects as Paired Keypoints". However, this page does not mention Fast NMS or any other NMS variant being used by CenterNet or CornerNet. The Fast NMS function was previously identified as being used by YOLACT.

## Turn 4 — document page 273 (rank 4 of 20)

This page lists various detector classes in MMDetection, including Mask R-CNN, Mask Scoring RCNN, NAS-FCOS, PAA, PanopticFPN, PointRend, QueryInst, and RPN. None of these classes or their descriptions mention Fast NMS or any NMS variant. The page does not provide any new information contradicting or supporting the previous answer that YOLACT uses Fast NMS.

## Turn 5 — document page 304 (rank 5 of 20)

This page describes the `HRFPN` and `NASFCOS_FPN` classes in MMDetection, Release 2.18.0. It explicitly links the `HRFPN` class to the paper "High-Resolution Representations for Labeling Pixels and Regions" and the `NASFCOS_FPN` class to the paper "NAS-FCOS: Fast Neural Architecture Search for Object Detection". However, neither of these classes nor their descriptions mention Fast NMS or any NMS variant. The page does not provide any new information contradicting or supporting the previous answer that YOLACT uses Fast NMS.

## Turn 6 — document page 18 (rank 6 of 20)

This page lists various baseline models in MMDetection, including RPN, Faster R-CNN, Mask R-CNN, Fast R-CNN, RetinaNet, Cascade R-CNN, HTC, and SSD. It mentions YOLOv3 in the context of image normalization configuration but does not mention Fast NMS or any NMS variant being used by these models. The page does not contradict or add new information about which paper uses Fast NMS.
