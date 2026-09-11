class mmdet.models.backbones.DetectoRS_ResNeXt(groups=1, base_width=4, **kwargs) ResNeXt backbone for DetectoRS.

## Parameters

• groups (int) – The number of groups in ResNeXt.

• base_width(int) – The base width of ResNeXt.

## make_res_layer(**kwargs)

Pack all blocks in a stage into a ResLayer for DetectoRS.

class mmdet.models.backbones.DetectoRS_ResNet(sac=None, stage_with_sac=(False, False, False, False), rfp_inplanes=None, output_img=False, pretrained=None, init_cfg=None, **kwargs)

ResNet backbone for DetectoRS.

## Parameters

• sac (dict, optional) – Dictionary to construct SAC (Switchable Atrous Convolution). Default: None.

• stage_with_sac(list) – Which stage to use sac. Default: (False, False, False, False).

• rfp_inplanes (int, optional) – The number of channels from RFP. Default: None. If specified, an additional conv layer will be added for rfp_feat. Otherwise, the structure is the same as base class.

• output_img (bool) – If True, the input image will be inserted into the starting position of output. Default: False.

## forward(x)

Forward function.

## init_weights()

Initialize the weights.

## make_res_layer(**kwargs)

Pack all blocks in a stage into a ResLayer for DetectoRS.

## rfp_forward(x, rfp_feats)

Forward function for RFP.

class mmdet.models.backbones.HRNet(extra, in_channels=3, conv_cfg=None, norm_cfg='type': 'BN'),

norm_eval=True, with_cp=False, zero_init_residual=False,

multiscale_output=True, pretrained=None, init_cfg=None)

HRNet backbone.

High-Resolution Representations for Labeling Pixels and Regions arXiv:.

## Parameters

• extra(dict) – Detailed configuration for each stage of HRNet. There must be 4 stages, the configuration for each stage must have 5 keys:

– num_modules(int): The number of HRModules in this stage.

– num_branches(int): The number of branches in the HRModule.

– block(str): The type of convolution block.

– num_blocks(tuple): The number of blocks in each branch. The length must be equal to num_branches.