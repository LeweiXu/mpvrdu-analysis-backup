## Parameters

• mask_pred (Tensor or ndarray) – shape (n, #class, h, w). For single-scale testing, mask_pred is the direct output of model, whose type is Tensor, while for multi-scale testing, it will be converted to numpy array outside of this method.

• det_bboxes (Tensor) – shape (n, 4/5)

• det_labels (Tensor) – shape (n, )

• rcnn_test_cfg(dict) – rcnn testing config

• ori_shape (Tuple) – original image height and width, shape (2,)

- scale_factor (ndarray / Tensor) – If rescale is True, box coordinates are divided by this scale factor to fit ori_shape.

• rescale (bool) – If True, the resulting masks will be rescaled to ori_shape.

## Returns

encoded masks. The c-th item in the outer list corresponds to the c-th class. Given the c-th outer list, the i-th item in that inner list is the mask for the i-th box with class label c.

Return type list[list]

## Example

>>> import mmcv

>>> from mmdet.models.roi_heads.mask_heads.fcn_mask_head import *  # NOQA
>>> N = 7  # N = number of extracted ROIs
>>> C, H, W = 11, 32, 32

>>> # Create example instance of FCN Mask Head.
>>> self = FCNMaskHead(num_classes=C, num_convs=0)
>>> inputs = torch.rand(N, self.in_channels, H, W)
>>> mask_pred = self.forward(inputs)

>>> # Each input is associated with some bounding box
>>> det_bboxes = torch.Tensor([[1, 1, 42, 42]] * N)
>>> det_labels = torch.randint(0, C, size=(N,))
>>> rcnn_test_cfg = mmcv.Config({'mask_thr_binary': 0, })
>>> ori_shape = (H * 4, W * 4)

>>> scale_factor = torch.FloatTensor((1, 1))

>>> rescale = False

>>> # Encoded masks are a list for each category.
>>> encoded_masks = self.get_seg_masks(
>>>     mask_pred, det_bboxes, det_labels, rcnn_test_cfg, ori_shape,
>>>     scale_factor, rescale

>>> )

>>> assert len(encoded_masks) == C

>>> assert sum(list(map(len, encoded_masks))) == N

init_weights()

Initialize the weights.

loss(mask_pred, mask_targets, labels)