# MODEL COMPLEXITY

tools/analysis_tools/get_flops.py is a script adapted from flops-counter.pytorch to compute the FLOPs and params of a given model.

python tools/analysis_tools/get_flops.py ${CONFIG_FILE} [--shape ${INPUT_SHAPE}]

You will get the results like this.

Input shape: (3, 1280, 800)
Flops: 239.32 GFLOPs
Params: 37.74 M

___

Note: This tool is still experimental and we do not guarantee that the number is absolutely correct. You may well use the result for simple comparisons, but double check it before you adopt it in technical reports or papers.

1. FLOPs are related to the input shape while parameters are not. The default input shape is  $ (1, 3, 1280, 800) $.

2. Some operators are not counted into FLOPs like GN and custom operators. Refer to mmcv.cnn.get_model_complexity_info() for details.

3. The FLOPs of two-stage detectors is dependent on the number of proposals.