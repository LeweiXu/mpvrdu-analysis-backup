• num_branch (int) – Number of branches in TridentNet.

• test_branch_idx(int) – In inference, all 3 branches will be used if test_branch_idx=-1, otherwise only branch with index test_branch_idx will be used.

• trident_dilations (tuple[int]) – Dilations of different trident branch. len(trident_dilations) should be equal to num_branch.

### 39.3 necks

##### class mmdet.models.necks.BFP(Balanced Feature Pyramids)

BFP takes multi-level features as inputs and gather them into a single one, then refine the gathered feature and scatter the refined results to multi-level features. This module is used in Libra R-CNN (CVPR 2019), see the paper Libra R-CNN: Towards Balanced Learning for Object Detection for details.

## Parameters

• in_channels (int) – Number of input channels (feature maps of all levels should have the same channels).

• num_levels (int) – Number of input feature levels.

• conv_cfg(dict) – The config dict for convolution layers.

• norm_cfg(dict) – The config dict for normalization layers.

• refine_level (int) – Index of integration and refine level of BSF in multi-level features from bottom to top.

• refine_type(str) – Type of the refine op, currently support [None, ‘conv’, ‘non_local’].

• init_cfg(dict or list[dict], optional) – Initialization config dict.

forward(inputs)

Forward function.

class mmdet.models.necks.CTResNetNeck(in_channel, num_deconv_filters, num_deconv_kernels,

 $$ use\_{d}cn{=}True,init\_{c}fg{=}None) $$ 

The neck used in CenterNet for object classification and box regression.

## Parameters

• in channel (int) – Number of input channels.

• num_deconv_filters (tuple[int]) – Number of filters per stage.

• num_deconv_kernels (tuple[int]) – Number of kernels per stage.

• use_dcn(bool) – If True, use DCNv2. Default: True.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(inputs)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.