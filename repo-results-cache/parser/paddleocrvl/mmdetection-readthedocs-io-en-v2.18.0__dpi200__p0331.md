• all_bbox_preds_list (list[Tensor]): Sigmoid regression outputs for each scale level. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

Return type tuple[list[Tensor], list[Tensor]]

## forward_onnx(feats, img_metas)

Forward function for exporting to ONNX.

Over-write forward because: masks is directly created with zero (valid position tag) and has the same spatial size as x. Thus the construction of masks is different from that in forward.

## Parameters

• feats (tuple[Tensor]) – Features from the upstream network, each is a 4D-tensor.

• img_metas (list[dict]) – List of image information.

## Returns

Outputs for all scale levels.

• all_cls_scores_list (list[Tensor]): Classification scores for each scale level. Each is a 4D-tensor with shape [nb_dec, bs, num_query, cls_out_channels]. Note  $ cls\_out\_channels $ should include background.

• all_bbox_preds_list (list[Tensor]): Sigmoid regression outputs for each scale level. Each is a 4D-tensor with normalized coordinate format (cx, cy, w, h) and shape [nb_dec, bs, num_query, 4].

Return type tuple[list[Tensor], list[Tensor]]

## forward_single(x, img_metas)

“Forward function for a single feature level.”

## Parameters

• x (Tensor) – Input feature from backbone’s single stage, shape [bs, c, h, w].

• img_metas (list[dict]) – List of image information.

## Returns

Outputs from the classification head, shape [nb_dec, bs, num_query, cls_out_channels]. Note cls_out_channels should include background.

all_bbox_pred(Tensor): Sigmoid outputs from the regression head with normalized coordinate format (cx, cy, w, h). Shape [nb_dec, bs, num_query, 4].

Return type all_cls_scores (Tensor)

## forward_single_onnx(x, img_metas)

“Forward function for a single feature level with ONNX exportation.”

## Parameters

• x (Tensor) – Input feature from backbone’s single stage, shape [bs, c, h, w].

• img_metas (list[dict]) – List of image information.

## Returns

Outputs from the classification head, shape [nb_dec, bs, num_query, cls_out_channels]. Note cls_out_channels should include background.

all_bbox_preds (Tensor): Sigmoid outputs from the regression head with normalized coordinate format (cx, cy, w, h). Shape [nb_dec, bs, num_query, 4].