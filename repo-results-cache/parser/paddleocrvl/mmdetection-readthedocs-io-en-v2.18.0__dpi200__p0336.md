- mlv1_cls_preds (list[Tensor]) – Multi-level scores. Each element in the list has shape (batch_size, num_classes, num_grids, num_grids).

• gt_labels (list [Tensor]) – Labels of multiple images.

- gt_masks (list[Tensor]) – Ground truth masks of multiple images. Each has shape (num_instances, h, w).

• img_metas (list[dict]) – Meta information of multiple images.

• gt_bboxes (list[Tensor]) – Ground truth bboxes of multiple images. Default: None.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.DecoupledSOLOLightHead(*args, dcn_cfg=None, init_cfg=['type':

(*args, dcn_cfg=None, init_cfg=['type': 'Normal', 'layer': 'Conv2d','std': 0.01}, {'type': 'Normal','std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_mask_list_x'}}, {'type': 'Normal','std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_mask_list_y'}}, {'type': 'Normal','std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_cls'}}], **kwargs)

Decoupled Light SOLO mask head used in SOLO: Segmenting Objects by Locations

## Parameters

• with_dcn(bool) – Whether use dcn in mask_convs and cls_convs, default: False.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(feats)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.dense_heads.DeformableDETRHead(*args, with_box_refine=False,

as_two_stage=False, transformer=None,

**kwargs)

Head of DeformDETR: Deformable DETR: Deformable Transformers for End-to-End Object Detection.

Code is modified from the official github repo.

More details can be found in the paper.

## Parameters

• with_box_refine (bool) – Whether to refine the reference points in the decoder. Defaults to False.

• as_two_stage (bool) – Whether to generate the proposal from the outputs of encoder.

• (obj (transformer) – ConfigDict): ConfigDict is used for building the Encoder and Decoder.