(continued from previous page)

asyncio.run(main())

#### 5.1.3 Demos

We also provide three demo scripts, implemented with high-level APIs and supporting functionality codes. Source codes are available here.

## Image demo

This script performs inference on a single image.

python demo/image_demo.py \
${IMAGE_FILE} \
${CONFIG_FILE} \
${CHECKPOINT_FILE} \
[--device ${GPU_ID}] \
[--score-thr ${SCORE_THR}]

Examples:

python demo/image_demo.py demo/demo.jpg \
config/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth \
--device cpu

## Webcam demo

This is a live demo from a webcam.

python demo/webcam_demo.py \
${CONFIG_FILE} \
${CHECKPOINT_FILE} \
[--device ${GPU_ID}] \
[--camera-id ${CAMERA-ID}] \
[--score-thr ${SCORE_THR}]

Examples:

python demo/webcam_demo.py \
config/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth