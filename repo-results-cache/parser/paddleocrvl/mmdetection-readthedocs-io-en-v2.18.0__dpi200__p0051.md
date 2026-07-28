scales=[8], # Basic scale of the anchor, the area of the anchor in one_
position of a feature map will be scale * base_sizes

ratios=[0.5, 1.0, 2.0], # The ratio between height and width.
strides=[4, 8, 16, 32, 64], # The strides of the anchor generator. This is_
consistent with the FPN feature strides. The strides will be taken as base_sizes if_
base_sizes is not set.

bbox_coder=dict( # Config of box coder to encode and decode the boxes during_
training and testing

type='DeltaXYWHBBoxCoder', # Type of box coder. 'DeltaXYWHBBoxCoder' is_
applied for most of methods. Refer to https://github.com/open-mmlab/mmdetection/blob/
master/mmdet/core/bbox/coder/delta_xywh_bbox_coder.py#L9 for more details.
target_means=[0.0, 0.0, 0.0, 0.0, 0.0], # The target means used to encode and_
decode boxes

target_stds=[1.0, 1.0, 1.0, 1.0, 1.0]), # The standard variance used to encode_
and decode boxes

loss_cls=dict( # Config of loss function for the classification branch
type='CrossEntropyLoss', # Type of loss for classification branch, we also_
support FocalLoss etc.

use_sigmoid=True, # RPN usually perform two-class classification, so it_
usually uses sigmoid function.

loss_weight=1.0, # Loss weight of the classification branch.

loss_bbox=dict( # Config of loss function for the regression branch.
type='L1Loss', # Type of loss, we also support many IoU Losses and smooth_
L1-loss, etc. Refer to https://github.com/open-mmlab/mmdetection/blob/master/mmdet/
models/losses/smooth_l1_loss.py#L56 for implementation.

loss_weight=1.0), # Loss weight of the regression branch.

roi_head=dict( # RoIHead encapsulates the second stage of two-stage/cascade_
detectors.

type='StandardRoIHead', # Type of the RoI head. Refer to https://github.com/
open-mmlab/mmdetection/blob/master/mmdet/models/roi_heads/standard_roi_head.py#L10 for_
implementation.

bbox_roi_extractor=dict( # RoI feature extractor for bbox regression.
type='SingleRoIExtractor', # Type of the RoI feature extractor, most of_
methods uses SingleRoIExtractor. Refer to https://github.com/open-mmlab/mmdetection/
blob/master/mmdet/models/roi_heads/roi_extractors/single_level.py#L10 for details.
roi_layer=dict( # Config of RoI Layer
type='RoIAlign', # Type of RoI Layer, DeformRoIPoolingPack and_
ModulatedDeformRoIPoolingPack are also supported. Refer to https://github.com/open-
mmlab/mmdetection/blob/master/mmdet/ops/roi_align/roi_align.py#L79 for details.
output_size=7, # The output size of feature maps.

sampling_ratio=0), # Sampling ratio when extracting the RoI features. 0_
means adaptive ratio.

out_channels=256, # output channels of the extracted feature.

featmap_strides=[4, 8, 16, 32], # Strides of multi-scale feature maps. It_
should be consistent to the architecture of the backbone.

bbox_head=dict( # Config of box head in the RoIHead.
type='Shared2FCBBoxHead', # Type of the bbox head, Refer to https://github.
com/open-mmlab/mmdetection/blob/master/mmdet/models/roi_heads/bbox_heads/convfc_bbox_
head.py#L177 for implementation details.

in_channels=256, # Input channels for bbox head. This is consistent with_
the out_channels in roi_extractor

fc_out_channels=1024, # Output feature channels of FC layers.

(continues on next page)