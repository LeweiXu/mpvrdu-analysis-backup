forward(x, res_feat=None, return_logits=True, return_feat=True)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.roi_heads.HybridTaskCascadeRoIHead(num_stages, stage_loss_weights,

(num_stages, stage_loss_weights,

semantic_roi_extractor=None,

semantic_head=None,

semantic_fusion=('bbox','mask'),

interleaved=True, mask_info_flow=True,

**kwargs)

Hybrid task cascade roi head including one bbox head and one mask head.

https://arxiv.org/abs/1901.07518

aug_test(img_feats, proposal_list, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

forward_dummy(x, proposals)

Dummy forward function.

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, gt_semantic_seg=None)

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposal_list (list[Tensors]) – list of region proposals.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None, list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None, Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

- gt_semantic_seg (None, list[Tensor]) – semantic segmentation masks used if the architecture supports semantic segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

simple_test(x, proposal_list, img_metas, rescale=False)

Test without augmentation.