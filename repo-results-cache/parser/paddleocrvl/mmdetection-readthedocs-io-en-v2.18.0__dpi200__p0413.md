class mmdet.models.roi_heads.SCNetBBoxHead(num_shared_convs=0, num_shared_fcs=0,

num_cls_convs=0, num_cls_fcs=0, num_reg_convs=0, num_reg_fcs=0, conv_out_channels=256, fc_out_channels=1024, conv_cfg=None, norm_cfg=None, init_cfg=None, *args, **kwargs)

BBox head for SCNet.

This inherits ConvFCBBoxHead with modified forward() function, allows us to get intermediate shared features.

forward(x, return_shared_feat=False)

Forward function.

Parameters

• x (Tensor) – input features

• return_shared_feat (bool) – If True, return cls-reg-shared feature.

## Returns

contain cls_score and bbox_pred, if return_shared_feat is True, append x_shared to the returned tuple.

Return type out (tuple[Tensor])

class mmdet.models.roi_heads.SCNetMaskHead(conv_to_res=True, **kwargs)

Mask head for SCNet.

Parameters conv_to_res (bool, optional) – if True, change the conv layers to SimplifiedBasicBlock.

class mmdet.models.roi_heads.SCNetRoIHead(num_stages, stage_loss_weights, semantic_roi_extractor=None, semantic_head=None, feat_relay_head=None, glbctx_head=None, **kwargs)

RoIHead for SCNet.

## Parameters

• num_stages (int) – number of cascade stages.

• stage_loss_weights(list) – loss weight of cascade stages.

• semantic_roi_extractor(dict) – config to init semantic roi extractor.

• semantic_head(dict) – config to init semantic head.

• feat_relay_head(dict) – config to init feature_relay_head.

• glbctx_head(dict) – config to init global context head.

aug_test(img_feats, proposal_list, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

forward_train(x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None,

gt_masks=None, gt_semantic_seg=None

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• img_metas (list[dict]) – list of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape',