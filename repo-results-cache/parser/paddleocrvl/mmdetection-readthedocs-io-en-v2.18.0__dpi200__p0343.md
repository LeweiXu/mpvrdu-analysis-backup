- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

reweight_loss_single(cls_loss, reg_loss, assigned_gt_inds, labels, level, min_levels)

Reweight loss values at each level.

Reassign loss values at each level by masking those where the pre-calculated loss is too large. Then return the reduced losses.

## Parameters

• cls_loss (Tensor) – Element-wise classification loss. Shape: (num_anchors, num_classes)

• reg_loss (Tensor) – Element-wise regression loss. Shape: (num_anchors, 4)

• assigned_gt_inds (Tensor) – The gt indices that each anchor bbox is assigned to. -1 denotes a negative anchor, otherwise it is the gt index (0-based). Shape: (num_anchors,),

• labels (Tensor) – Label assigned to anchors. Shape: (num_anchors, ).

• level (int) – The current level index in the pyramid (0-4 for RetinaNet)

• min_levels (Tensor) – The best-matching level for each gt. Shape: (num_gts, ),

## Returns

• cls_loss: Reduced corrected classification loss. Scalar.

• reg_loss: Reduced corrected regression loss. Scalar.

• pos_flags (Tensor): Corrected bool tensor indicating the final positive anchors. Shape: (num_anchors, ).

Return type tuple

class mmdet.models.dense_heads.FeatureAdaption(in_channels, out_channels, kernel_size=3,

deform_groups=4, init_cfg='layer': 'Conv2d',
'override': {'name': 'conv_adaption','std': 0.01, 'type': 'Normal'},'std': 0.1, 'type': 'Normal'}

Feature Adaption Module.

Feature Adaption Module is implemented based on DCN v1. It uses anchor shape prediction rather than feature map to predict offsets of deform conv layer.

## Parameters

• in channels (int) – Number of channels in the input feature map.

• out channels (int) – Number of channels in the output feature map.

• kernel_size (int) – Deformable conv kernel size.

• deform groups (int) – Deformable conv group size.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(x, shape)

Defines the computation performed at every call.

Should be overridden by all subclasses.