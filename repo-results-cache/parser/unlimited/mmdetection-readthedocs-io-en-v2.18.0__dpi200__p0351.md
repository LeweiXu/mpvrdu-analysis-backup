MMDetection, Release 2.18.0
ga_loc_targets(gt_bboxes_list, featmap_sizes)
Compute location targets for guided anchoring.
Each feature map is divided into positive, negative and ignore regions. - positive regions: target 1, weight 1 - ignore regions: target 0, weight 0 - negative regions: target 0, weight 0.1
Parameters
- gt_bboxes_list (list[Tensor]) – Gt bboxes of each image.
- featmap_sizes (list[tuple]) – Multi level sizes of each feature maps.
Returns tuple
ga_shape_targets(approx_list, inside_flag_list, square_list, gt_bboxes_list, img_metas, gt_bboxes_ignore_list=None, unmap_outputs=True)
Compute guided anchoring targets.
Parameters
- approx_list (list[list]) – Multi level approx of each image.
- inside_flag_list (list[list]) – Multi level inside flags of each image.
- square_list (list[list]) – Multi level squares of each image.
- gt_bboxes_list (list[Tensor]) – Ground truth bboxes of each image.
- img_metas (list[dict]) – Meta info of each image.
- gt_bboxes_ignore_list (list[Tensor]) – ignore list of gt bboxes.
- unmap_outputs (bool) – unmap outputs or not.
Returns tuple
get_anchors(featmap_sizes, shape_preds, loc_preds, img_metas, use_loc_filter=False, device='cuda')
Get squares according to feature map sizes and guided anchors.
Parameters
- featmap_sizes (list[tuple]) – Multi-level feature map sizes.
- shape_preds (list[tensor]) – Multi-level shape predictions.
- loc_preds (list[tensor]) – Multi-level location predictions.
- img_metas (list[dict]) – Image meta info.
- use_loc_filter(bool) – Use loc filter or not.
- device (torch.device / str) – device for returned tensors
Returns
square approx of each image, guided anchors of each image, loc masks of each image
Return type tuple
get_bboxes(cls_scores, bbox_preds, shape_preds, loc_preds, img_metas, cfg=None, rescale=False) Transform network outputs of a batch into bbox results.
Note: When score_factors is not None, the cls_scores are usually multiplied by it then obtain the real score used in NMS, such as CenterNess in FCOS, IoU branch in ATSS.
Parameters
- cls_scores (list[Tensor]) – Classification scores for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * num_classes, H, W).
344
Chapter 39. mmdet.models