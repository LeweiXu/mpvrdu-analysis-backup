## Parameters

• num_classes (int) – Number of categories excluding the background category.

• in channels (int) – Number of channels in the input feature map.

• feat_channels (int) – Number of hidden channels. Used in child classes. Default: 256.

• stacked_convs (int) – Number of stacking convs of the head. Default: 4.

• strides (tuple) – Downsample factor of each feature map.

- scale_ranges (tuple[tuple[int, int]]) – Area range of multiple level masks, in the format [(min1, max1), (min2, max2),...]. A range of (16, 64) means the area range between (16, 64).

• pos_scale (float) – Constant scale factor to control the center region.

- num_grids (list[int]) – Divided image into a uniform grids, each feature map has a different grid value. The number of output channels is grid ** 2. Default: [40, 36, 24, 16, 12].

• cls_down_index (int) – The index of downsample operation in classification branch. Default: 0.

• loss mask (dict) – Config of mask loss.

• loss_cls (dict) – Config of classification loss.

• norm_cfg (dict) – dictionary to construct and config norm layer. Default: norm_cfg=dict(type='GN', num_groups=32,

requires_grad=True).

• train_cfg(dict) – Training config of head.

• test_cfg(dict) – Testing config of head.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

get_results(mlvl_mask_preds, mlvl_cls_scores, img_metas, **kwargs)

Get multi-image mask results.

## Parameters

- mlvl_mask_preds (list[Tensor]) – Multi-level mask prediction. Each element in the list has shape (batch_size, num_grids**2, h, w).

- mlv1_cls_scores (list[Tensor]) – Multi-level scores. Each element in the list has shape (batch_size, num_classes, num_grids, num_grids).

• img_metas (list[dict]) – Meta information of all images.

## Returns

Processed results of multiple images. Each InstanceData usually contains the following keys.