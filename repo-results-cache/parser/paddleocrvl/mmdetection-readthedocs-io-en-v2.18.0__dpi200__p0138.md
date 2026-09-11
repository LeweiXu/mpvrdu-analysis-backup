## HYPER-PARAMETER OPTIMIZATION

### 28.1 YOLO Anchor Optimization

tools/analysis_tools/optimize_anchors.py provides two methods to optimize YOLO anchors.

One is k-means anchor cluster which refers from darknet.

python tools/analysis_tools/optimize_anchors.py ${CONFIG} --algorithm k-means --input-shape ${INPUT_SHAPE [WIDTH HEIGHT]} --output-dir ${OUTPUT_DIR}

Another is using differential evolution to optimize anchors.

python tools/analysis_tools/optimize_anchors.py ${CONFIG} --algorithm differential_evolution --input-shape ${INPUT_SHAPE [WIDTH HEIGHT]} --output-dir ${OUTPUT_DIR}

E.g.,

python tools/analysis_tools/optimize_anchors.py config/yolo/yolov3_d53_320_273e_coco.py --algorithm differential_evolution --input-shape 608 608 --device cuda --output-dir work_dir

You will get:

loading annotations into memory...
Done (t=9.70s)
creating index...
index created!
2021-07-19 19:37:20,951 - mmdet - INFO - Collecting bboxes from annotation...
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]] 117266/117266, 15874.5 task/s,
↔ elapsed: 7s, ETA: 0s
2021-07-19 19:37:28,753 - mmdet - INFO - Collected 849902 bboxes.
differential_evolution step 1: f(x)= 0.506055
differential_evolution step 2: f(x)= 0.506055
differential_evolution step 489: f(x)= 0.386625
2021-07-19 19:46:40,775 - mmdet - INFO Anchor evolution finish. Average IOU: 0.
↔ 6133754253387451
2021-07-19 19:46:40,776 - mmdet - INFO Anchor differential evolution result:[[10, 12],
↔ [15, 30], [32, 22], [29, 59], [61, 46], [57, 116], [112, 89], [154, 198], [349, 336]]
2021-07-19 19:46:40,798 - mmdet - INFO Result saved in work_dirs/anchor_optimize_result.
↔ json (continues on next page)