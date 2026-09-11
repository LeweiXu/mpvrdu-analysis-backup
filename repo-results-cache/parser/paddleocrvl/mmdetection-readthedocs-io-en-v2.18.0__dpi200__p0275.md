'img_norm_cfg'. For details on the values of these keys see mmdet.datasets.pipelines.Collect.

- gt_bboxes (list[Tensor]) – Each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – Class indices corresponding to each box

- gt_bboxes_ignore (None / list[Tensor]) – Specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

onnx_export(img, img_metas, with_nms=True)

Test function without test time augmentation.

Parameters

• img (torch.Tensor) – input images.

• img_metas (list[dict]) – List of image information.

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].

Return type tuple[Tensor, Tensor]

simple_test(img, img_metas, rescale=False)

Test function without test-time augmentation.

## Parameters

• img (torch.Tensor) – Images with shape (N, C, H, W).

• img_metas (list[dict]) – List of image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

## Returns

BBox results of each image and classes. The outer list corresponds to each image. The inner list corresponds to each class.

Return type list[list[np.ndarray]]

class mmdet.models.detectors.SparseRCNN(*args, **kwargs)

Implementation of Sparse R-CNN: End-to-End Object Detection with Learnable Proposals

forward_dummy(img)

Used for computing network flops.

See mmdetection/tools/analysis_tools/get_flops.py

forward_train(img, img_metas, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, proposals=None, **kwargs)

Forward function of SparseR-CNN and QueryInst in train stage.

Parameters

• img (Tensor) – of shape (N, C, H, W) encoding input images. Typically these should be mean centered and std scaled.