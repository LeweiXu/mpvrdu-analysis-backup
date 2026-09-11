(continued from previous page)

for gid in range(n_img)

>>> pos_is_gts = [
...     torch.randint(0, 2, (npos,)).byte().sort()
...     descending=True)[0]
...     for npos in pos_per_img
... ]
... bboxes_list = self.refine_bboxes(rois, labels, bbox_preds,
...         pos_is_gts, img_metas)
... print(bboxes_list)

## regress_by_class(rois, label, bbox_pred, img_meta)

Regress the bbox for the predicted class. Used in Cascade R-CNN.

## Parameters

• rois (Tensor) – Rois from  $ rpn\_head $ or last stage  $ bbox\_head $, has shape (num_proposals, 4) or (num_proposals, 5).

• label (Tensor) – Only used when self.reg_class_agnostic is False, has shape (num_proposals, ).

• bbox_pred (Tensor) – Regression prediction of current stage bbox_head. When self.reg_class_agnostic is False, it has shape (n, num_classes * 4), otherwise it has shape (n, 4).

• img_meta(dict) – Image meta info.

Returns Regressed bboxes, the same shape as input rois.

Return type Tensor

class mmdet.models.roi_heads.BaseRoIExtractor(roi_layer, out_channels, featmap_strides,

 $$ init_{-}cfg=None) $$ 

Base class for RoI extractor.

## Parameters

• roi_layer(dict) – Specify RoI layer type and arguments.

• out channels (int) – Output channels of RoI layers.

• featmap_strides(int) – Strides of input feature maps.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

## build_roi_layers(layer_cfg, featmap_strides)

Build RoI operator to extract feature from each level feature map.

## Parameters

• layer_cfg(dict) – Dictionary to construct and config RoI layer operation. Options are modules under mmcv/ops such as RoIAlign.

• featmap_strides (List[int]) – The stride of input feature map w.r.t to the original image size, which would be used to scale RoI coordinate (original image coordinate system) to feature coordinate system.

## Returns

The RoI extractor modules for each level feature map.

Return type nn.ModuleList