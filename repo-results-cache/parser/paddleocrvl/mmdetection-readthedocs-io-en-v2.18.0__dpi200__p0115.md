# It is invalid that override don't have name key
init_cfg = dict(type='Constant', layer ['Conv1d', 'Conv2d'], val=1, bias=2, override=dict(type='Constant', val=3, bias=4))
# It is also invalid that override has name and other args except type
init_cfg = dict(type='Constant', layer ['Conv1d', 'Conv2d'], val=1, bias=2, override=dict(name='reg', val=3, bias=4))

1. Initialize model with the pretrained model

init_cfg = dict(type='Pretrained', checkpoint='torchvision://resnet50')

More details can refer to the documentation in MMCV and MMCV PR #780

Apart from training/testing scripts, We provide lots of useful tools under the tools/ directory.