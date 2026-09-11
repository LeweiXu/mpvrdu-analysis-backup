Each item in result_list is 2-tuple. The first item is bboxes with shape  $ (n, 5) $, where 5 represent  $ (tl\_x, tl\_y, br\_x, br\_y, score) $. The shape of the second tensor in the tuple is labels with shape  $ (n) $, The length of list should always be 1.

## Return type list[tuple[Tensor, Tensor]]

## forward(feats)

Forward features from the upstream network.

Parameters feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

## Returns

A tuple of classification scores and bbox prediction.

• cls_scores (list[Tensor]): Classification scores for all scale levels, each is a 4D-tensor, the channels number is num_base_priors * num_classes.

• bbox_pred(list[Tensor]): Box energies / deltas for all scale levels, each is a 4D-tensor, the channels number is num_base_priors * 4.

## Return type tuple

## forward_single(x)

Forward feature of a single scale level.

Parameters x (Tensor) – Features of a single scale level.

Returns cls_score (Tensor): Cls scores for a single scale level the channels number is num_base_priors * num_classes. bbox_pred (Tensor): Box energies / deltas for a single scale level, the channels number is num_base_priors * 4.

## Return type tuple

## get_anchors(featmap_sizes, img_metas, device='cuda')

Get anchors according to feature map sizes.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• img_metas (list[dict]) – Image meta info.

• device (torch.device / str) – Device for returned tensors

Returns anchor_list (list[Tensor]): Anchors of each image. valid_flag_list (list[Tensor]): Valid flags of each image.

## Return type tuple

## get_targets(anchor_list, valid_flag_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None,

gt_labels_list=None, label_channels=1, unmap_outputs=True,

return sampling results=False)

Compute regression and classification targets for anchors in multiple images.

## Parameters

• anchor_list (list[list[Tensor]]) – Multi level anchors of each image. The outer list indicates images, and the inner list corresponds to feature levels of the image. Each element of the inner list is a tensor of shape (num_ర్చన, 4).

- valid_flag_list (list[list[Tensor]]) – Multi level valid flags of each image. The outer list indicates images, and the inner list corresponds to feature levels of the image. Each element of the inner list is a tensor of shape (num_anchors,)