• cls_score (Tensor) – Classification prediction results of all class, has shape (batch_size * num_proposals_single_image, num_classes)

• bbox_pred (Tensor) – Regression prediction results, has shape (batch_size * num_proposals_single_image, 4), the last dimension 4 represents [tl_x, tl_y, br_x, br_y].

• labels (Tensor) – Label of each proposals, has shape (batch_size * num_proposals_single_image

• label_weights (Tensor) – Classification loss weight of each proposals, has shape (batch_size * num_proposals_single_image

• bbox_targets (Tensor) – Regression targets of each proposals, has shape (batch_size * num_proposals_single_image, 4), the last dimension 4 represents [tl_x, tl_y, br_x, br_y].

• bbox_weights (Tensor) – Regression loss weight of each proposals’s coordinate, has shape (batch_size * num_proposals_single_image, 4),

• imgs_whwh (Tensor) – imgs_whwh (Tensor): Tensor with shape (batch_size, num_proposals, 4), the last dimension means [img_width, img_height, img_width, img_height].

• reduction_override (str, optional) – The reduction method used to override the original reduction method of the loss. Options are “none”, “mean” and “sum”. Defaults to None.

• Returns – dict[str, Tensor]: Dictionary of loss components

class mmdet.models.roi_heads.DoubleConvFCBBoxHead(num_convs=0, num_fcs=0,

conv_out_channels=1024, fc_out_channels=1024, conv_cfg=None, norm_cfg={'type': 'BN'}, init_cfg={'override': [{'type': 'Normal', 'name': 'fc_cls','std': 0.01}, {'type': 'Normal', 'name': 'fc_reg','std': 0.001}, {'type': 'Xavier', 'name': 'fc_branch', 'distribution': 'uniform'}], 'type': 'Normal'}, **kwargs)

Bbox head used in Double-Head R-CNN

/-> shared convs ->

roi features

\\-> shared fc

## forward( $ x_{cls}, x_{reg} $)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

##### class mmdet.models.roi_heads.DoubleHeadRoIHead(reg_roi_scale_factor, **kwargs) RoI head for Double Head RCNN

https://arxiv.org/abs/1904.06493