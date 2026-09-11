(continued from previous page)

8 \
--format-only \
--options "jsonfile_prefix=/mask_rcnn_test-dev_results"

This command generates two JSON files mask_rcnn_test-dev_results.bbox.json and mask_rcnn_test-dev_results.segm.json.

7. Test Mask R-CNN on Cityscapes test with 8 GPUs, and generate txt and png files for submitting to the official evaluation server. Config and checkpoint files are available here.

./tools/dist_test.sh \
configs/cityscapes/mask_rcnn_r50_fpn_1x_cityscapes.py \
checkpoints/mask_rcnn_r50_fpn_1x_cityscapes_20200227-afe51d5a.pth \
8 \
--format-only \
--options "txtfile_prefix=.mask_rcnn_cityscapes_test_results"

The generated png and txt would be under./mask_rcnn_cityscapes_test_results directory.

#### 5.2.4 Test without Ground Truth Annotations

MMDetection supports to test models without ground-truth annotations using CocoDataset. If your dataset format is not in COCO format, please convert them to COCO format. For example, if your dataset format is VOC, you can directly convert it to COCO format by the script in tools. If your dataset format is Cityscapes, you can directly convert it to COCO format by the script in tools. The rest of the formats can be converted using this script.

python tools/dataset_converters/images2coco.py \
${IMG_PATH} \
${CLASSES} \
${OUT} \
[--exclude-extensions]

## arguments

• IMG_PATH: The root path of images.

• CLASSES: The text file with a list of categories.

• OUT: The output annotation json file name. The save dir is in the same directory as IMG_PATH.

• exclude-extensions: The suffix of images to be excluded, such as 'png' and 'bmp'.

After the conversion is complete, you can use the following command to test

# single-gpu testing
python tools/test.py \
${CONFIG_FILE} \
${CHECKPOINT_FILE} \
--format-only \
--options ${JSONFILE_PREFIX} \
[--show]
# multi-gpu testing
bash tools/dist_test.sh \
${CONFIG_FILE} \

(continues on next page)