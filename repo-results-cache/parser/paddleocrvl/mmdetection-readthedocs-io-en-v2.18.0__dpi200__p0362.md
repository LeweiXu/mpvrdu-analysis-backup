## forward_single(x)

Forward feature map of a single FPN level.

## gen_grid_from_reg(reg, previous_boxes)

Base on the previous bboxes and regression values, we compute the regressed bboxes and generate the grids on the bboxes.

## Parameters

• reg – the regression value to previous bboxes.

• previous_boxes – previous bboxes.

Returns generate grids on the regressed bboxes.

get_points(featmap_sizes, img_metas, device)

Get points according to feature map sizes.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• img_metas (list[dict]) – Image meta info.

Returns points of each image, valid flags of each image

## Return type tuple

get_targets(proposals_list, valid_flag_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None, gt_labels_list=None, stage='init', label_channels=1, unmap_outputs=True)

Compute corresponding GT box and classification targets for proposals.

## Parameters

• proposals_list (list[list]) – Multi level points/bboxes of each image.

• valid_flag_list (list[list]) – Multi level valid flags of each image.

• gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.

• img_metas (list[dict]) – Meta info of each image.

• gt_bboxes_ignore_list (list[Tensor]) – Ground truth bboxes to be ignored.

• gt_bboxes_list – Ground truth labels of each box.

• stage (str) – init or refine. Generate target for init stage or refine stage

• label channels (int) – Channel of label.

• unmap outputs (bool) – Whether to map outputs back to the original set of anchors.

## Returns

• labels_list (list[Tensor]): Labels of each level.

• label_weights_list (list[Tensor]): Label weights of each level. # noqa: E501

• bbox_gt_list (list[Tensor]): Ground truth bbox of each level.

• proposal_list (list[Tensor]): Proposals(points/bboxes) of each level. # noqa: E501

• proposal_weights_list (list[Tensor]): Proposal weights of each level. # noqa: E501

• num_total_pos (int): Number of positive samples in all images. #noqa: E501

• num_total_neg (int): Number of negative samples in all images. #noqa: E501

## Return type tuple