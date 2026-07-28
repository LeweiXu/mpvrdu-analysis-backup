python tools/analysis_tools/analyze_logs.py plot_curve log.json --keys loss_cls_loss_bbox --out losses.pdf

• Compare the bbox mAP of two runs in the same figure.

python tools/analysis_tools/analyze_logs.py plot_curve log1.json log2.json --keys_→bbox_mAP --legend run1 run2

• Compute the average training speed.

python tools/analysis_tools/analyze_logs.py cal_train_time log.json [--include-outliers]

The output is expected to be like the following.

-----Analyze train time of work_dirs/some_exp/20190611_192040.log.json-----
slowest epoch 11, average time is 1.2024
fastest epoch 1, average time is 1.1909
time std over epochs is 0.0028
average iter time: 1.1959 s/iter