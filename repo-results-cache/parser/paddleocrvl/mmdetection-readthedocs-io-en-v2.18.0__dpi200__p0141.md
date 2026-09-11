(continued from previous page)

for _ in range(self.bbox_head[-1].num_classes)
    [] * num_imgs

if self.with_mask:
    mask_classes = self.mask_head[-1].num_classes
    segm_results = [[]] for _ in range(mask_classes)]
    for _ in range(num_imgs)]
    results = list(zip(bbox_results, segm_results))
else:
    results = bbox_results

return results

# There is no proposal in the single image
for i in range(self.num_stages):
   ...
    if i < self.num_stages - 1:
        for j in range(num_imgs):
            # Handle empty proposal
            if rois[j].shape[0] > 0:
                bbox_label = cls_score[j][:, -1].argmax(dim=1)
                refine_roi = self.bbox_head[i].regress_by_class(
                    rois[j], bbox_label, bbox_pred[j], img_metas[j])
                refine_roi_list.append(refine_roi)

If you have customized RoIHead, you can refer to the above method to deal with empty proposals.

### 29.3 Coco Panoptic Dataset

In MMDetection, we have supported COCO Panoptic dataset. We clarify a few conventions about the implementation of CocoPanopticDataset here.

1. For mmdet $ \leq $2.16.0, the range of foreground and background labels in semantic segmentation are different from the default setting of MMDetection. The label 0 stands for VOID label and the category labels start from 1. Since mmdet=2.17.0, the category labels of semantic segmentation start from 0 and label 255 stands for VOID for consistency with labels of bounding boxes. To achieve that, the Pad pipeline supports setting the padding value for seg.

2. In the evaluation, the panoptic result is a map with the same shape as the original image. Each value in the result map has the format of instance_id * INSTANCE_OFFSET + category_id.