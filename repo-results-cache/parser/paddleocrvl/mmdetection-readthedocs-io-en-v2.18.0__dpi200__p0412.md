## attention_pool(reg_x)

Extract direction-specific features fx and fy with attention mechanism.

bbox_pred_split(bbox_pred, num_proposals_per_img)

Split batch bbox prediction back to each image.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## refine_bboxes(rois, labels, bbox_preds, pos_is_gts, img_metas)

Refine bboxes during training.

## Parameters

• rois (Tensor) – Shape (n*bs, 5), where n is image number per GPU, and bs is the sampled RoIs per image.

• labels (Tensor) – Shape (n*bs, ).

• bbox_preds (list[Tensor]) - Shape [(n*bs, num_ buckets*2), (n*bs, num_ buckets*2)].

• pos_is_gts (list [Tensor]) – Flags indicating if each positive bbox is a gt bbox.

• img_metas (list[dict]) – Meta info of each image.

Returns Refined bboxes of each image in a mini-batch.

Return type list[Tensor]

reg_pred(x, offset_fcs, cls_fcs)

Predict bucketing estimation (cls_pred) and fine regression (offset pred) with side-aware features.

regress_by_class(rois, label, bbox_pred, img_meta)

Regress the bbox for the predicted class. Used in Cascade R-CNN.

## Parameters

• rois (Tensor) – shape (n, 4) or (n, 5)

• label (Tensor) – shape (n,)

• bbox_pred (list[Tensor]) – shape [(n, num_ buckets *2), (n, num_ buckets *2)]

• img_meta(dict) – Image meta info.

Returns Regressed bboxes, the same shape as input rois.

Return type Tensor

side_aware_feature_extractor(reg_x)

Refine and extract side-aware features without split them.

side_aware_split(feat)

Split side-aware features aligned with orders of bucketing targets.