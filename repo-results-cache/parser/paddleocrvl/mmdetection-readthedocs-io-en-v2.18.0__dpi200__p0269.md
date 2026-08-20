aug_test(imgs, img_metas, rescale=True)

Augment testing of CenterNet. Aug test must have flipped image pair, and unlike CornerNet, it will perform an averaging operation on the feature map instead of detecting bbox.

## Parameters

• imgs (list[Tensor]) – Augmented images.

• img_metas (list[list[dict]]) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If True, return boxes in original image space. Default: True.

Note: imgs must include flipped image pairs.

## Returns

BBox results of each image and classes. The outer list corresponds to each image. The inner list corresponds to each class.

Return type list[list[np.ndarray]]

merge_aug_results(aug_results, with_nms)

Merge augmented detection bboxes and score.

## Parameters

• aug_results (list[list[Tensor]]) – Det_bboxes and det_labels of each image.

• with_nms (bool) – If True, do nms before return boxes.

Returns (out_bboxes, out_labels)

Return type tuple

class mmdet.models.detectors.CornerNet(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

CornerNet.

This detector is the implementation of the paper CornerNet: Detecting Objects as Paired Keypoints.

aug_test(imgs, img_metas, rescale=False)

Augment testing of CornerNet.

## Parameters

• imgs (list[Tensor]) – Augmented images.

• img_metas (list[list[dict]]) – Meta information of each image, e.g., image size, scaling factor, etc.

• rescale (bool) – If True, return boxes in original image space. Default: False.

Note: imgs must include flipped image pairs.

## Returns

BBox results of each image and classes. The outer list corresponds to each image. The inner list corresponds to each class.

Return type list[list[np.ndarray]]