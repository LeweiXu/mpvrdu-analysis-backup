init_point_head(point_head)

Initialize point_head

mask_onnx_export(x, img_metas, det_bboxes, det_labels, **kwargs)

Export mask branch to onnx which supports batch inference.

## Parameters

• x (tuple[Tensor]) – Feature maps of all scale level.

• img_metas (list[dict]) – Image meta info.

• det_bboxes (Tensor) – Bboxes and corresponding scores. has shape [N, num_bboxes, 5].

• det_labels (Tensor) – class labels of shape [N, num_bboxes].

## Returns

The segmentation results of shape [N, num_bboxes, image_height, image_width].

Return type Tensor

simple_test_mask(x, img_metas, det_bboxes, det_labels, rescale=False)

Obtain mask prediction without augmentation.

class mmdet.models.roi_heads.ResLayer(depth, stage=3, stride=2, dilation=1, style='pytorch', norm_cfg='requires_grad': True, 'type': 'BN'}, norm_eval=True, with_cp=False, dcn=None, pretrained=None, init_cfg=None)

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## train(mode=True)

Sets the module in training mode.

This has any effect only on certain modules. See documentations of particular modules for details of their behaviors in training/evaluation mode, if they are affected, e.g. Dropout, BatchNorm, etc.

Parameters mode (bool) – whether to set training mode (True) or evaluation mode (False). Default: True.

Returns self

Return type Module