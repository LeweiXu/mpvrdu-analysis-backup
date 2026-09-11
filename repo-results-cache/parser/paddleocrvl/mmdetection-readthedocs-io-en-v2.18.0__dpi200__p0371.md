• bbox_pred (Tensor) – Box energies / deltas for each image level with shape (num_total_anchors, 4).

• anchors (Tensor) – Box reference for each scale level with shape (num_total_anchors, 4).

• labels (Tensor) – Labels of each anchor with shape (num_total_anchors,).

• label_weights (Tensor) – Label weights of each anchor with shape (num_total_anchors,)

• bbox_targets (Tensor) – BBox regression targets of each anchor weight shape (num_total_anchors, 4).

• bbox_weights (Tensor) – BBox regression loss weights of each anchor with shape (num_total_anchors, 4).

• num_total_samples (int) – If sampling, num total samples equal to the number of total anchors; Otherwise, it is the number of positive anchors.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

## property num_anchors

Returns: list[int]: Number of base_anchors on each point of each level.

(in_channels, anchor_generator={'ratios': [1.0],'scales': [8],'strides': [4, 8, 16, 32, 64], 'type': 'AnchorGenerator'}, adapt_cfg={'dilation': 3, 'type': 'dilation'}, bridged_feature=False, with_cls=True, sampling=True, init_cfg=None, **kwargs)

Stage of CascadeRPNHead.

## Parameters

• in channels (int) – Number of channels in the input feature map.

• anchor_generator(dict) – anchor generator config.

• adapt_cfg(dict) – adaptation config.

• bridged_feature (bool, optional) – whether update rpn feature. Default: False.

• with_cls (bool, optional) – whether use classification branch. Default: True.

• sampling (bool, optional) – whether use sampling. Default: True.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## anchor offset(anchor list, anchor strides, featmap sizes)

Get offset for deformable conv based on anchor shape NOTE: currently support deformable kernel_size=3 and dilation=1

## Parameters

• anchor_list (list[list[tensor]]) – [NI, NLVL, NA, 4] list of multi-level anchors

• anchor_strides (list[int]) – anchor stride of each level

## Returns

[NLVL, NA, 2, 18]: offset of DeformConv kernel.

Return type offset list (list[tensor])