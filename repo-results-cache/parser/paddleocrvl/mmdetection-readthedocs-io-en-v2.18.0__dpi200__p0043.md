VOC2007 VOC2012

(continued from previous page)

The cityscapes annotations have to be converted into the coco format using tools/dataset_converters/cityscapes.py:

pip install cityscapesscripts
python tools/dataset_converters/cityscapes.py./data/cityscapes --nproc 8 --out-dir./
→data/cityscapes/annotations

Currently the config files in cityscapes use COCO pre-trained weights to initialize. You could download the pre-trained models in advance if network is unavailable or slow, otherwise it would cause errors at the beginning of training.

### 7.2 Prepare your own customized model

The second step is to use your own module or training setting. Assume that we want to implement a new neck called AugFPN to replace with the default FPN under the existing detector Cascade Mask R-CNN R50. The following implementsAugFPN under MMDetection.

####### 7.2.1 1. Define a new neck (e.g. AugFPN)

Firstly create a new file mmdet/models/necks/augfpn.py.

from..builder import NECKS
@NECKS.register_module()
class AugFPN(nn.Module):
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