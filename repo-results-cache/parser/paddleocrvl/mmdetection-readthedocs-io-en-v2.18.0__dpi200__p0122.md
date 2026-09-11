## ERROR ANALYSIS

tools/analysis_tools/coco_error_analysis.py analyzes COCO results per category and by different criterion. It can also make a plot to provide useful information.

python tools/analysis_tools/coco_error_analysis.py ${RESULT} ${OUT_DIR} [-h] [--ann} →{ANN}] [--types ${TYPES[TYPES...]}]

## Example:

Assume that you have got Mask R-CNN checkpoint file in the path 'checkpoint'. For other checkpoints, please refer to our model zoo. You can use the following command to get the results bbox and segmentation json file.

# out: results.bbox.json and results.segm.json
python tools/test.py \
config/mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py \
checkpoint/mask_rcnn_r50_fpn_1x_coco_20200205-d4b0c5d6.pth \
--format-only \
--options "jsonfile_prefix=.results"

1. Get COCO bbox error results per category, save analyze result images to the directory results/

python tools/analysis_tools/coco_error_analysis.py \
results.bbox.json \
results \
--ann=data/coco/annotations/instances_val2017.json \

1. Get COCO segmentation error results per category, save analyze result images to the directory results/

python tools/analysis_tools/coco_error_analysis.py \
results.segm.json \
results \
--ann=data/coco/annotations/instances_val2017.json \
--types='segm'