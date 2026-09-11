Return type list[np.ndarray]

extract_feat(img)

Extract features.

Parameters img (torch.Tensor) – Image tensor with shape (n, c, h, w).

Returns

Multi-level features that may have different resolutions.

Return type list[torch.Tensor]

forward_dummy(img)

Dummy forward function.

forward_train(img, img_metas, gt_bboxes=None, gt_bboxes_ignore=None)

## Parameters

• img (Tensor) – Input images of shape (N, C, H, W). Typically these should be mean centered and std scaled.

• img_metas (list[dict]) – A List of image info dict where each dict has: 'img_shape','scale_factor', 'flip', and may also contain 'filename', 'ori_shape', 'pad_shape', and 'img_norm_cfg'. For details on the values of these keys see mmdet.datasets.pipelines.Collect.

- gt_bboxes (list[Tensor]) – Each item are the truth boxes for each image in [tl_x, tl_y, br_x, br_y] format.

- gt_bboxes_ignore (None / list[Tensor]) – Specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

show_result(data, result, top_k=20, **kwargs)

Show RPN proposals on the image.

Parameters

• data (str or np.ndarray) – Image filename or loaded image.

• result (Tensor or tuple) – The results to draw over img bbox_result or (bbox_result, segm_result).

• top_k(int) – Plot the first k bboxes only if set positive. Default: 20

Returns The image with bboxes drawn on it.

Return type np.ndarray

simple_test(img, img_metas, rescale=False)

Test function without test time augmentation.

Parameters

• imgs (list[torch.Tensor]) – List of multiple images

• img_metas (list[dict]) – List of image information.

• rescale (bool, optional) – Whether to rescale the results. Defaults to False.

Returns proposals