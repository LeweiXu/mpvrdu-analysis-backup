## BENCHMARK

### 26.1 Robust Detection Benchmark

tools/analysis_tools/test_robustness.py and tools/analysis_tools/robustness_eval.py helps users to evaluate model robustness. The core idea comes from Benchmarking Robustness in Object Detection: Autonomous Driving when Winter is Coming. For more information how to evaluate models on corrupted images and results for a set of standard models please refer to robustness_benchmarking.md.

### 26.2 FPS Benchmark

tools/analysis_tools/benchmark.py helps users to calculate FPS. The FPS value includes model forward and post-processing. In order to get a more accurate value, currently only supports single GPU distributed startup mode.

python -m torch.distributed.launch --nproc_per_node=1 --master_port=${{PORT}} tools/ analysis_tools/benchmark.py \
${CONFIG} \
${CHECKPOINT} \
[--repeat-num ${REPEAT_NUM}] \
[--max-iter ${MAX_ITER}] \
[--log-interval ${LOG_INTERVAL}] \
--launcher pytorch

Examples: Assuming that you have already downloaded the Faster R-CNN model checkpoint to the directory checkpoints/.

python -m torch.distributed.launch --nproc_per_node=1 --master_port=29500 tools/analysis_tools/benchmark.py \
config/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py \
checkpoints/faster_rcnn_r50_fpn_1x_coco_20200130-047c8118.pth \
--launcher pytorch