### 2. Import the module

You can either add the following line to mmdet/models/backbones/_init_.py

from.mobilenet import MobileNet

or alternatively add

custom_imports = dict(
    imports=['mmdet.models.backbones.mobilenet'],
    allow_failed_imports=False)

to the config file to avoid modifying the original code.

3. Use the backbone in your config file

model = dict(
    backbone=dict(
        type='MobileNet',
        arg1=xxx,
        arg2=xxx),
   ...
)

#### 11.1.2 Add new necks

##### 1. Define a neck (e.g. PAFPN)

Create a new file mmdet/models/necks/pafpn.py.

from..builder import NECKS
@NECKS.register_module()
class PAFPN(nn.Module):
def __init__(self,
                  in_channels,
                  out_channels,
                  num_outs,
                  start_level=0,
                  end_level=-1,
                  add_extra_convs=False):
pass
def forward(self, inputs):
    # implementation is ignored
    pass