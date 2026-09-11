2. IoU calculation. This affects the matching process between ground truth and bounding box and the NMS process. The effect to compatibility is very negligible, though.

3. The corners of bounding box is in float type and no longer quantized. This should provide more accurate bounding box results. This also makes the bounding box and RoIs not required to have minimum size of 1, whose effect is small, though.

• The anchors are center-aligned to feature grid points and in float type. In MMDetection 1.x and previous version, the anchors are in int type and not center-aligned. This affects the anchor generation in RPN and all the anchor-based methods.

• ROIAlign is better aligned with the image coordinate system. The new implementation is adopted from Detectron2. The RoIs are shifted by half a pixel by default when they are used to cropping RoI features, compared to MMDetection 1.x. The old behavior is still available by setting aligned=False instead of aligned=True.

• Mask cropping and pasting are more accurate.

1. We use the new RoIAlign to crop mask targets. In MMDetection 1.x, the bounding box is quantized before it is used to crop mask target, and the crop process is implemented by numpy. In new implementation, the bounding box for crop is not quantized and sent to RoIAlign. This implementation accelerates the training speed by a large margin ( $ \sim $0.1s per iter,  $ \sim $2 hour when training Mask R50 for 1x schedule) and should be more accurate.

2. In MMDetection 2.0, the “paste_mask()” function is different and should be more accurate than those in previous versions. This change follows the modification in Detectron2 and can improve mask AP on COCO by  $ \sim0.5\% $ absolute.

#### 30.4.2 Codebase Conventions

• MMDetection 2.0 changes the order of class labels to reduce unused parameters in regression and mask branch more naturally (without +1 and -1). This effect all the classification layers of the model to have a different ordering of class labels. The final layers of regression branch and mask head no longer keep  $ K+1 $ channels for K categories, and their class orders are consistent with the classification branch.

– In MMDetection 2.0, label “K” means background, and labels [0, K-1] correspond to the K = num_categories object categories.

– In MMDetection 1.x and previous version, label “0” means background, and labels [1, K] correspond to the K categories.

– Note: The class order of softmax RPN is still the same as that in 1.x in versions $ \leq $2.4.0 while sigmoid RPN is not affected. The class orders in all heads are unified since MMDetection v2.5.0.

• Low quality matching in R-CNN is not used. In MMDetection 1.x and previous versions, the max_iou_assigner will match low quality boxes for each ground truth box in both RPN and R-CNN training. We observe this sometimes does not assign the most perfect GT box to some bounding boxes, thus MMDetection 2.0 do not allow low quality matching by default in R-CNN training in the new system. This sometimes may slightly improve the box AP ( $ \sim $0.1% absolute).

- Separate scale factors for width and height. In MMDetection 1.x and previous versions, the scale factor is a single float in mode keep_ratio=True. This is slightly inaccurate because the scale factors for width and height have slight difference. MMDetection 2.0 adopts separate scale factors for width and height, the improvement on AP  $ \sim0.1\% $ absolute.

• Configs name conventions are changed. MMDetection V2.0 adopts the new name convention to maintain the gradually growing model zoo as the following:

[model]_(model setting)_[backbone]_[neck]_(norm setting)__(misc)__(gpu x batch)__→[schedule]_[dataset].py,