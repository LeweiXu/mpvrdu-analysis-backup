• upsample_cfg(dict) – Dictionary to construct and configure upsample layer.

• init_cfg(dict or list[dict], optional) – Initialization config dict. Default: None

forward(inputs)
Forward function.

Initialize the weights of module.

slice_as(src, dst)
Slice src as dst

Note: src should have the same or larger size than dst.

## Parameters

• src (torch.Tensor) – Tensors to be sliced.

• dst (torch.Tensor) – src will be sliced to have the same size as dst.

Returns Sliced tensor.

Return type torch.Tensor

## tensor_add(a, b)

Add tensors a and b that might have different sizes.

class mmdet.models.necks.HRFPN(High Resolution Feature Pyramids)

paper: High-Resolution Representations for Labeling Pixels and Regions.

## Parameters

• in channels (list) – number of channels for each branch.

• out channels (int) – output channels of feature pyramids.

• num_outs (int) – number of output stages.

• pooling_type(str) – pooling for generating feature pyramids from {MAX, AVG}.

• conv_cfg(dict) – dictionary to construct and configure conv layer.

• norm_cfg(dict) – dictionary to construct and configure norm layer.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed.

• stride (int) – stride of 3x3 convolutional layers

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(inputs)

Forward function.

class mmdet.models.necks.NASFCOS_FPN(in_channels, out_channels, num_outs, start_level=1, end_level=-1, add_extra_convs=False, conv_cfg=None, norm_cfg=None, init_cfg=None)

FPN structure in NASFPN.

Implementation of paper NAS-FCOS: Fast Neural Architecture Search for Object Detection

## Parameters