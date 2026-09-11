property with_mask

whether the RoI head contains a mask_head

Type bool

property with_shared_head

whether the RoI head contains a shared_head

Type bool

class mmdet.models.roi_heads.CascadeRoIHead(num_stages, stage_loss_weights,

(num_stages, stage_loss_weights,

 $ bbox\_roi\_extractor=None $,  $ bbox\_head=None $,

 $ mask\_roi\_extractor=None $,  $ mask\_head=None $,

 $ shared\_head=None $,  $ train\_cfg=None $,  $ test\_cfg=None $,

 $ pretrained=None $,  $ init\_cfg=None $)

Cascade roi head including one bbox head and one mask head.

https://arxiv.org/abs/1712.00726

aug_test(features, proposal_list, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

forward_dummy(x, proposals)

Dummy forward function.

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None)

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet/datasets/pipelines/formatting.py:Collect.

• proposals (list [Tensors]) – list of region proposals.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

- gt_masks (None / Tensor) – true segmentation masks for each box used if the architecture supports a segmentation task.

Returns a dictionary of loss components

Return type dict[str, Tensor]

init_assigner_sampler()

Initialize assigner and sampler for each stage.

init_bbox_head(bbox_roi_extractor, bbox_head)

Initialize box head and box roi extractor.

Parameters