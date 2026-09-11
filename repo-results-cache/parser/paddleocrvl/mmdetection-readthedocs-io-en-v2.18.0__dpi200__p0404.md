• in channels (int, optional) – number of input channels. Default: 256.

• conv_out_channels (int, optional) – number of output channels before classification layer. Default: 256.

• num_classes (int, optional) – number of classes. Default: 80.

• loss_weight (float, optional) – global context loss weight. Default: 1.

• conv_cfg(dict, optional) – config to init conv layer. Default: None.

• norm_cfg(dict, optional) – config to init norm layer. Default: None.

• conv_to_res (bool, optional) – if True, 2 convs will be grouped into 1 SimplifiedBasicBlock using a skip connection. Default: False.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Forward function.

loss(pred, labels)

Loss function.

class mmdet.models.roi_heads.GridHead(grid_points=9, num_convs=8, roi_feat_size=14, in_channels=256,

(grid_points=9, num_convs=8, roi_feat_size=14, in_channels=256, conv_kernel_size=3, point_feat_channels=64, deconv_kernel_size=4, class_agnostic=False, loss_grid={'loss_weight': 15, 'type': 'CrossEntropyLoss', 'use_sigmoid': True}, conv_cfg=None, norm_cfg={'num_groups': 36, 'type': 'GN'}, init_cfg=[{'type': 'Kaiming', 'layer': ['Conv2d', 'Linear'], {'type': 'Normal', 'layer': 'ConvTranspose2d','std': 0.001, 'override': {'type': 'Normal', 'name': 'deconv2','std': 0.001, 'bias': -4.59511985013459}]}]})

## calc_sub_regions()

Compute point specific representation regions.

See Grid R-CNN Plus (https://arxiv.org/abs/1906.05688) for details.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.roi_heads.GridRoIHead(grid_roi_extractor, grid_head, **kwargs)

    Grid roi head for Grid R-CNN.

    https://arxiv.org/abs/1811.12030

    forward_dummy(x, proposals)

        Dummy forward function.

    simple_test(x, proposal_list, img_metas, proposals=None, rescale=False)

    Test without augmentation.

class mmdet.models.roi_heads.HTCMaskHead(with_conv_res=True, *args, **kwargs)