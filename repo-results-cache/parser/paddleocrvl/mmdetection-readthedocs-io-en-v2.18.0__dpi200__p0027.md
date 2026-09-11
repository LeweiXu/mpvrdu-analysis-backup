## Video demo

This script performs inference on a video.

python demo/video_demo.py \
${VIDEO_FILE} \
${CONFIG_FILE} \
${CHECKPOINT_FILE} \
[--device ${GPU_ID}] \
[--score-thr ${SCORE_THR}] \
[--out ${OUT_FILE}] \
[--show] \
[--wait-time ${WAIT_TIME}]
Examples:
python demo/video_demo.py demo/demo.mp4 \
config/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth \
--out result.mp4

### 5.2 Test existing models on standard datasets

To evaluate a model’s accuracy, one usually tests the model on some standard datasets. MMDetection supports multiple public datasets including COCO, Pascal VOC, CityScapes, and more. This section will show how to test existing models on supported datasets.

#### 5.2.1 Prepare datasets

Public datasets like Pascal VOC or mirror and COCO are available from official websites or mirrors. Note: In the detection task, Pascal VOC 2012 is an extension of Pascal VOC 2007 without overlap, and we usually use them together. It is recommended to download and extract the dataset somewhere outside the project directory and symlink the dataset root to $MMDETECTION/data as below. If your folder structure is different, you may need to change the corresponding paths in config files.

mmdetection
- mmdet
- tools
- configs
- data
  - coco
  - annotations
  - train2017
  - val2017
  - test2017
- cityscapes
  - annotations
  - leftImg8bit
  - train
  - val
  - gtFine

(continues on next page)