• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## get_anchors(featmap_sizes, img_metas, device='cuda')

Get squares according to feature map sizes and guided anchors.

## Parameters

• featmap sizes (list[tuple]) – Multi-level feature map sizes.

• img_metas (list[dict]) – Image meta info.

• device (torch.device / str) – device for returned tensors

Returns square approx of each image

Return type tuple

get_bboxes(cls_scores, bbox_preds, img_metas, cfg=None, rescale=False)

Transform network outputs of a batch into bbox results.

Note: When score_factors is not None, the cls_scores are usually multiplied by it then obtain the real score used in NMS, such as CenterNess in FCOS, IoU branch in ATSS.

## Parameters

• cls_scores (list[Tensor]) – Classification scores for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * num_classes, H, W).

• bbox_preds (list[Tensor]) – Box energies / deltas for all scale levels, each is a 4D-tensor, has shape (batch_size, num_priors * 4, H, W).

- score_factors (list[Tensor], Optional) – Score factor for all scale level, each is a 4D-tensor, has shape (batch_size, num_priors * 1, H, W). Default None.

• img_metas (list[dict], Optional) – Image meta info. Default None.

•cfg (mmcv.Config, Optional) – Test / postprocessing configuration, if None, test_cfg would be used. Default None.

• rescale (bool) – If True, return boxes in original image space. Default False.

• with_nms (bool) – If True, do nms before return boxes. Default True.

## Returns

Each item in result_list is 2-tuple. The first item is an  $ (n, 5) $ tensor, where the first 4 columns are bounding box positions  $ (tl\_x, tl\_y, br\_x, br\_y) $ and the 5-th column is a score between 0 and 1. The second item is a  $ (n,) $ tensor where each item is the predicted class label of the corresponding box.

Return type list[list[Tensor, Tensor]]