## 3 : TRAIN WITH CUSTOMIZED MODELS AND STANDARD DATASETS

In this note, you will know how to train, test and inference your own customized models under standard datasets. We use the cityscapes dataset to train a customized Cascade Mask R-CNN R50 model as an example to demonstrate the whole process, which using AugFPN to replace the default FPN as neck, and add Rotate or Translate as training-time auto augmentation.

The basic steps are as below:

1. Prepare the standard dataset

2. Prepare your own customized model

3. Prepare a config

4. Train, test, and inference models on the standard dataset.

### 7.1 Prepare the standard dataset

In this note, as we use the standard cityscapes dataset as an example.

It is recommended to symlink the dataset root to $MMDETECTION/data. If your folder structure is different, you may need to change the corresponding paths in config files.

mmdetection
mmdet
tools
configs
data
coco
annotations
train2017
val2017
test2017
cityscapes
annotations
leftImg8bit
train
val
gtFine
train
val
VOCdevkit

(continues on next page)