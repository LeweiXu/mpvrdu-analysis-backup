## RESULT ANALYSIS

tools/analysis_tools/analyze_results.py calculates single image mAP and saves or shows the topk images with the highest and lowest scores based on prediction results.

Usage

python tools/analysis_tools/analyze_results.py \
${CONFIG} \
${PREDICTION_PATH} \
${SHOW_DIR} \
[--show] \
[--wait-time ${WAIT_TIME}] \
[--topk ${TOPK}] \
[--show-score-thr ${SHOW_SCORE_THR}] \
[--cfg-options ${CFG_OPTIONS}]

Description of all arguments:

• config : The path of a model config file.

• prediction_path: Output result file in pickle format from tools/test.py

• show_dir: Directory where painted GT and detection images will be saved

• --showDetermines whether to show painted images. If not specified, it will be set to False.

• --wait-time: The interval of show (s), 0 is block

• --topk: The number of saved images that have the highest and lowest topk scores after sorting. If not specified, it will be set to 20.

• --show-score-thr: Show score threshold. If not specified, it will be set to 0.

• --cfg-options: If specified, the key-value pair optionalcfg will be merged into config file

## Examples:

Assume that you have got result file in pickle format from tools/test.py in the path ‘./result.pkl’.

1. Test Faster R-CNN and visualize the results, save images to the directory results/

python tools/analysis_tools/analyze_results.py \
configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
result.pkl \
results \
--show

1. Test Faster R-CNN and specified topk to 50, save images to the directory results/