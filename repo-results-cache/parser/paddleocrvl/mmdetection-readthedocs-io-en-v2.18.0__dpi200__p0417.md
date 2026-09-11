Returns a dictionary of loss components of all stage.

Return type dict[str, Tensor]

simple_test(x, proposal_boxes, proposal_features, img_metas, imgs_whwh, rescale=False)

Test without augmentation.

## Parameters

• x (list[Tensor]) – list of multi-level img features.

• proposal_boxes (Tensor) – Decoded proposal bboxes, has shape (batch_size, num_proposals, 4)

• proposal_features (Tensor) – Expanded proposal features, has shape (batch_size, num_proposals, proposal_feature_channel)

• img_metas(dict) – meta information of images.

• imgs_whwh (Tensor) – Tensor with shape (batch_size, 4), the dimension means [img_width, img_height, img_width, img_height].

• rescale (bool) – If True, return boxes in original image space. Defaults to False.

Returns When no mask branch, it is bbox results of each image and classes with type list[list[np.ndarray]]. The outer list corresponds to each image. The inner list corresponds to each class. When the model has a mask branch, it is a list[tuple] that contains bbox results and mask results. The outer list corresponds to each image, and first element of tuple is bbox results, second element is mask results.

Return type list[list[np.ndarray]] or list[tuple]

class mmdet.models.roi_heads.StandardRoIHead(bbox_roi_extractor=None, bbox_head=None,

mask_roi_extractor=None, mask_head=None,

shared_head=None, train_cfg=None, test_cfg=None,

pretrained=None, init_cfg=None

Simplest base roi head including one bbox head and one mask head.

async async_simple_test(x, proposal_list, img_metas, proposals=None, rescale=False)

Async test without augmentation.

aug_test(x, proposal_list, img_metas, rescale=False)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

bbox_onnx_export(x, img_metas, proposals, rcnn_test_cfg, **kwargs)

Export bbox branch to onnx which supports batch inference.

## Parameters

• x (tuple[Tensor]) – Feature maps of all scale level.

• img_metas (list[dict]) – Image meta info.

• proposals (Tensor) – Region proposals with batch dimension, has shape [N, num_boxes, 5].

• (obj (rcnn_test_cfg) – ConfigDict): test_cfg of R-CNN.

## Returns

bboxes of shape [N, num_bboxes, 5] and class labels of shape [N, num_bboxes].

Return type tuple[Tensor, Tensor]