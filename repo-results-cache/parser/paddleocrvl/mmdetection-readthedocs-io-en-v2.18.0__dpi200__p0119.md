python tools/analysis_tools/analyze_results.py \
configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
result.pkl \
results \
--topk 50

1. If you want to filter the low score prediction results, you can specify the show-score-thr parameter

python tools/analysis_tools/analyze_results.py \
configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
result.pkl \
results \
--show-score-thr 0.3