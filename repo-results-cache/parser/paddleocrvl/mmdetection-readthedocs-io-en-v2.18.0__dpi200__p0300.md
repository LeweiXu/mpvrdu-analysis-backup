• the dilated residual block

## Parameters

• in channels (int) – The number of input channels.

• out channels (int) – The number of output channels.

• block_mid_channels (int) – The number of middle block output channels

• num_residual_blocks (int) – The number of residual blocks.

## forward(feature)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

class mmdet.models.necks.FPG(in_channels, out_channels, num_outs, stack_times, paths,

inter_channels=None, same_down_trans=None,

same_up_trans={'kernel_size': 3, 'padding': 1,'stride': 2, 'type': 'conv'},

across_lateral_trans={'kernel_size': 1, 'type': 'conv'},

across_down_trans={'kernel_size': 3, 'type': 'conv'},

across_up_trans=None,

across_skip_trans={'type': 'identity'},

output_trans={'kernel_size': 3, 'type': 'last_conv'},

start_level=0,

end_level=-1,

add_extra_convs=False,

norm_cfg=None, skip_inds=None, init_cfg={['type': 'Caffe2Xavier', 'layer': 'Conv2d'}, {'type': 'Constant', 'layer': ['BatchNorm', 'InstanceNorm', 'GroupNorm', 'LayerNorm'], 'val': 1.0}]})

## FPG

Implementation of Feature Pyramid Grids (FPG). This implementation only gives the basic structure stated in the paper. But users can implement different types of transitions to fully explore the potential power of the structure of FPG.

## Parameters

• in_channels (int) – Number of input channels (feature maps of all levels should have the same channels).

• out_channels (int) – Number of output channels (used at each scale)

• num_outs (int) – Number of output scales.

• stack_times (int) – The number of times the pyramid architecture will be stacked.

• paths (list[str]) – Specify the path order of each stack level. Each element in the list should be either ‘bu’ (bottom-up) or ‘td’ (top-down).

• inter channels (int) – Number of inter channels.

• same_up_trans(dict) – Transition that goes down at the same stage.

• same_down_trans (dict) – Transition that goes up at the same stage.

• across_lateral_trans(dict) – Across-pathway same-stage

• across_down_trans(dict) – Across-pathway bottom-up connection.

• across_up_trans(dict) – Across-pathway top-down connection.