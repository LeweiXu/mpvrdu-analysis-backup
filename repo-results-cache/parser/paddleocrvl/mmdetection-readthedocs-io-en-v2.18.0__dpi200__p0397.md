the latter silently ignores them.

## init_weights()

Initialize the weights.

More general bbox head, with shared conv and fc layers and two optional separated branches.

shared convs -> shared fcs

/-> cls convs -> cls fcs -> cls

\-> reg convs -> reg fcs -> reg

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.roi_heads.DIIHead(num_classes=80, num_ffn_fcs=2, num_heads=8, num_cls_fcs=1,

num_reg_fcs=3, feedforward_channels=2048, in_channels=256, dropout=0.0, ffn_act_cfg='{inplace': True, 'type': 'ReLU'}, dynamic_conv_cfg='{act_cfg': {'inplace': True, 'type': 'ReLU'}, 'feat_channels': 64, 'in_channels': 256, 'input_feat_shape': 7, 'norm_cfg': {'type': 'LN'}, 'out_channels': 256, 'type': 'DynamicConv'}, 'loss_iou': {'loss_weight': 2.0, 'type': 'GIoULoss'}, 'init_cfg': None, **kwargs)

Dynamic Instance Interactive Head for Sparse R-CNN: End-to-End Object Detection with Learnable Proposals

## Parameters

• num_classes (int) – Number of class in dataset. Defaults to 80.

• num_ffn_fcs (int) – The number of fully-connected layers in FFNs. Defaults to 2.

• num heads (int) – The hidden dimension of FFNs. Defaults to 8.

- num_cls_fcs (int) – The number of fully-connected layers in classification subnet. Defaults to 1.

• num_reg_fcs (int) – The number of fully-connected layers in regression subnet. Defaults to 3.

• feedforward channels (int) – The hidden dimension of FFNs. Defaults to 2048

• in channels (int) – Hidden channels of MultiheadAttention. Defaults to 256.

• dropout (float) – Probability of drop the channel. Defaults to 0.0

• ffn_act_cfg(dict) – The activation config for FFNs.

• dynamic_conv_cfg(dict) – The convolution config for DynamicConv.

• loss_iou(dict) – The config for iou or giou loss.