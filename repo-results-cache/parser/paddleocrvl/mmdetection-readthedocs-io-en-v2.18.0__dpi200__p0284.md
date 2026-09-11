– num_channels(tuple): The number of channels in each branch. The length must be equal to num_branches.

• in channels (int) – Number of input image channels. Default: 3.

• conv_cfg(dict) – Dictionary to construct and configure conv layer.

• norm_cfg(dict) – Dictionary to construct and configure norm layer.

• norm_eval (bool) – Whether to set norm layers to eval mode, namely, freeze running stats (mean and var). Note: Effect on Batch Norm and its variants only. Default: True.

• with_cp (bool) – Use checkpoint or not. Using checkpoint will save some memory while slowing down the training speed. Default: False.

• zero_init_residual (bool) – Whether to use zero init for last norm layer in resblocks to let them behave as identity. Default: False.

• multiscale_output (bool) – Whether to output multi-level features produced by multiple branches. If False, only the first level feature will be output. Default: True.

• pretrained(str, optional) – Model pretrained path. Default: None.

• init_cfg (dict or list[dict], optional) – Initialization config dict. Default: None.

## Example

>>> from mmdet.models import HRNet

>>> import torch

>>> extra = dict(
    stage1=dict(
        num_modules=1,
        num_branches=1,
        block='BOTTLENECK',
        num_blocks=(4, ),
        num_channels=(64, )),
        stage2=dict(
            num_modules=1,
            num_branches=2,
            block='BASIC',
            num_blocks=(4, 4),
            num_channels=(32, 64)),
            stage3=dict(
                num_modules=4,
                num_branches=3,
                block='BASIC',
                num_blocks=(4, 4, 4),
                num_channels=(32, 64, 128)),
                stage4=dict(
                    num_modules=3,
                    num_branches=4,
                    block='BASIC',
                    num_blocks=(4, 4, 4, 4),
                    num_channels=(32, 64, 128, 256)))
        self = HRNet(extra, in_channels=1)

>>> self.eval()

(continues on next page)