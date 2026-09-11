'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposal_list (list[Tensors]) – list of region proposals.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None, list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None, Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

- gt_semantic_seg (None, list[Tensor]) – semantic segmentation masks used if the architecture supports semantic segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

init_mask_head(mask_roi_extractor, mask_head)

Initialize mask_head

simple_test(x, proposal_list, img_metas, rescale=False)

Test without augmentation.

## Parameters

• x(tuple[Tensor]) – Features from upstream network. Each has shape (batch_size, c, h, w).

• proposal_list (list(Tensor)) – Proposals from rpn head. Each has shape (num_proposals, 5), last dimension 5 represent (x1, y1, x2, y2, score).

• img_metas (list[dict]) – Meta information of images.

• rescale (bool) – Whether to rescale the results to the original image. Default: True.

Returns When no mask branch, it is bbox results of each image and classes with type list[list[np.ndarray]]. The outer list corresponds to each image. The inner list corresponds to each class. When the model has mask branch, it contains bbox results and mask results. The outer list corresponds to each image, and first element of tuple is bbox results, second element is mask results.

Return type list[list[np.ndarray]] or list[tuple]

property with_feat_relay

whether the head has feature relay head

Type bool

property with_glbctx

whether the head has global context head

Type bool

property with\_semantic

whether the head has semantic head

Type bool

class mmdet.models.roi_heads.SCNetSemanticHead(conv_to_res=True, **kwargs) Mask head for SCNet.