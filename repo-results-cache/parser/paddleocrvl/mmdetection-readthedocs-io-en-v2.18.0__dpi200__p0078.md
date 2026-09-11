## TUTORIAL 4: CUSTOMIZE MODELS

We basically categorize model components into 5 types.

• backbone: usually an FCN network to extract feature maps, e.g., ResNet, MobileNet.

• neck: the component between backbones and heads, e.g., FPN, PAFPN.

• head: the component for specific tasks, e.g., bbox prediction and mask prediction.

• roi extractor: the part for extracting RoI features from feature maps, e.g., RoI Align.

• loss: the component in head for calculating losses, e.g., FocalLoss, L1Loss, and GHMLoss.

### 11.1 Develop new components

#### 11.1.1 Add a new backbone

Here we show how to develop new components with an example of MobileNet.

##### 1. Define a new backbone (e.g. MobileNet)

Create a new file mmdet/models/backbones/mobilenet.py.

import torch.nn as nn
from..builder import BACKBONES
@BACKBONES.register_module()
class MobileNet(nn.Module):
def __init__(self, arg1, arg2):
    pass
def forward(self, x):  # should return a tuple
    pass