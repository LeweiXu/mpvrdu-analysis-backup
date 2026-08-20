loss(segm_pred, gt_masks, gt_labels)

Compute loss of the head.

## Parameters

- segm_pred (list[Tensor]) – Predicted semantic segmentation map with shape (N, num_classes, H, W).

- gt_masks (list[Tensor]) – Ground truth masks for each image with the same shape of the input image.

• gt_labels (list[Tensor]) – Class indices corresponding to each box.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

simple_test(feats, img_metas, rescale=False)

Test function without test-time augmentation.

class mmdet.models.dense_heads.YOLOFHead(num_classes, in_channels, num_cls_convs=2,

num_reg_convs=4, norm_cfg={'requires_grad': True, 'type': 'BN'}, **kwargs)

YOLOFHead Paper link: https://arxiv.org/abs/2103.09460.

## Parameters

• num_classes (int) – The number of object classes (w/o background)

• in channels (List[int]) – The number of input channels per scale.

• cls_num_convs (int) – The number of convolutions of cls branch. Default 2.

• reg_num_convs (int) – The number of convolutions of reg branch. Default 4.

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

## forward_single(feature)

Forward feature of a single scale level.

Parameters x (Tensor) – Features of a single scale level.

Returns cls_score (Tensor): Cls scores for a single scale level the channels number is num_base_priors * num_classes. bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_base_priors * 4.

## Return type tuple

get_targets(cls_scores_list, bbox_preds_list, anchor_list, valid_flag_list, gt_bboxes_list, img_metas,

gt_bboxes_ignore_list=None, gt_labels_list=None, label_channels=1, unmap_outputs=True) Compute regression and classification targets for anchors in multiple images.

## Parameters

• cls_scores_list (list[Tensor]) – each image. each is a 4D-tensor, the shape is (h * w, num_anchors * num_classes).

• bbox_preds_list (list[Tensor]) – each is a 4D-tensor, the shape is (h * w, num_anchors * 4).

• anchor_list (list[Tensor]) – Anchors of each image. Each element of is a tensor of shape  $ (h * w * \text{num\_archors}, 4) $.

- valid_flag_list (list[Tensor]) – Valid flags of each image. Each element of is a tensor of shape (h * w * num_anchors,)