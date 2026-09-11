#### 5.2.3 Examples

Assuming that you have already downloaded the checkpoints to the directory checkpoints/.

1. Test Faster R-CNN and visualize the results. Press any key for the next image. Config and checkpoint files are available here.

python tools/test.py \
config/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth \
--show

2. Test Faster R-CNN and save the painted images for future visualization. Config and checkpoint files are available here.

python tools/test.py \
config/faster_rcnn/faster_rcnn_r50_fpn_1x.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth \
--show-dir faster_rcnn_r50_fpn_1x_results

3. Test Faster R-CNN on PASCAL VOC (without saving the test results) and evaluate the mAP. Config and checkpoint files are available here.

python tools/test.py \
config/pascal_voc/faster_rcnn_r50_fpn_1x_voc.py \
checkpoints/faster_rcnn_r50_fpn_1x_voc0712_20200624-c9895d40.pth \
--eval mAP

4. Test Mask R-CNN with 8 GPUs, and evaluate the bbox and mask AP. Config and checkpoint files are available here.

./tools/dist_test.sh \
configs/mask_rcnn_r50_fpn_1x_coco.py \
checkpoints/mask_rcnn_r50_fpn_1x_coco_20200205-d4b0c5d6.pth \
8 \
--out results.pkl \
--eval bbox segm

5. Test Mask R-CNN with 8 GPUs, and evaluate the classwise bbox and mask AP. Config and checkpoint files are available here.

./tools/dist_test.sh \
configs/mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py \
checkpoints/mask_rcnn_r50_fpn_1x_coco_20200205-d4b0c5d6.pth \
8 \
--out results.pkl \
--eval bbox segm \
--options "classwise=True"

6. Test Mask R-CNN on COCO test-dev with 8 GPUs, and generate JSON files for submitting to the official evaluation server. Config and checkpoint files are available here.

./tools/dist_test.sh \
configs/mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py \
checkpoints/mask_rcnn_r50_fpn_1x_coco_20200205-d4b0c5d6.pth \

(continues on next page)