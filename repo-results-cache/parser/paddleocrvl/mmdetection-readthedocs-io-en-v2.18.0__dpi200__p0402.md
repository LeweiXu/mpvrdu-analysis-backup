## Example

>>> from mmdet.models.roi_heads.mask_heads.fcn_mask_head import *  # NOQA
>>> N = 7  # N = number of extracted ROIs
>>> C, H, W = 11, 32, 32
>>> # Create example instance of FCN Mask Head.
>>> # There are lots of variations depending on the configuration
>>> self = FCNMaskHead(num_classes=C, num_convs=1)
>>> inputs = torch.rand(N, self.in_channels, H, W)
>>> mask_pred = self.forward(inputs)
>>> sf = self.scale_factor
>>> labels = torch.randint(0, C, size=(N,))
>>> # With the default properties the mask targets should indicate
>>> # a (potentially soft) single-class label
>>> mask_targets = torch.rand(N, H * sf, W * sf)
>>> loss = self.loss(mask_pred, mask_targets, labels)
>>> print('loss = {!r}'.format(loss))

## onnx_export(mask_pred, det_bboxes, det_labels, rcnn_test_cfg, ori_shape, **kwargs)

Get segmentation masks from mask_pred and bboxes.

## Parameters

• mask_pred (Tensor) – shape (n, #class, h, w).

• det_bboxes (Tensor) – shape (n, 4/5)

• det_labels (Tensor) – shape (n,)

• rcnn_test_cfg(dict) – rcnn testing config

• ori_shape (Tuple) – original image height and width, shape (2,)

Returns a mask of shape  $ (N, img\_h, img\_w) $.

Return type Tensor

class mmdet.models.roi_heads.FeatureRelayHead(in_channels=1024, out_conv_channels=256)

Feature Relay Head used in SCNet.

## Parameters

• in_channels (int, optional) – number of input channels. Default: 256.

• conv_out_channels (int, optional) – number of output channels before classification layer. Default: 256.

• roi_feat_size (int, optional) – roi feat size at box head. Default: 7.

- scale_factor (int, optional) – scale factor to match roi feat size at mask head. Default: 2.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(x)

Forward function.