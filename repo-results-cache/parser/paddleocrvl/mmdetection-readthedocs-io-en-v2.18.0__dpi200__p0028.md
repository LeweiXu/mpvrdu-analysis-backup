train val
VOCdevkit
VOC2007
VOC2012

(continued from previous page)

Some models require additional COCO-stuff datasets, such as HTC, DetectoRS and SCNet, you can download and unzip them move to the coco folder. The directory should be like this.

mmdetection
| data
| coco
| annotations
| train2017
| val2017
| test2017
| stuffthingmaps

Panoptic segmentation models like PanopticFPN require additional COCO Panoptic datasets, you can download and unzip them move to the coco annotation folder. The directory should be like this.

mmdetection
data
coco
annotations
panoptic_train2017.json
panoptic_train2017
panoptic_val2017.json
panoptic_val2017
train2017
val2017
test2017

The cityscapes annotations need to be converted into the coco format using tools/dataset_converters/cityscapes.py:

pip install cityscapesscripts

python tools/dataset_converters/cityscapes.py \
./data/cityscapes \
--nproc 8 \
--out-dir./data/cityscapes/annotations

TODO: CHANGE TO THE NEW PATH