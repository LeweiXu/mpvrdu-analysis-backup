#### 5.2.2 Test existing models

We provide testing scripts for evaluating an existing model on the whole dataset (COCO, PASCAL VOC, Cityscapes, etc.). The following testing environments are supported:

• single GPU

• single node multiple GPUs

• multiple nodes

Choose the proper script to perform testing depending on the testing environment.

# single-gpu testing
python tools/test.py \
    ${CONFIG_FILE} \
    ${CHECKPOINT_FILE} \
    [--out ${RESULT_FILE}] \
    [--eval ${EVAL_METRICS}] \
    [--show]

# multi-gpu testing
bash tools/dist_test.sh \
    ${CONFIG_FILE} \
    ${CHECKPOINT_FILE} \
    ${GPU_NUM} \
    [--out ${RESULT_FILE}] \
    [--eval ${EVAL_METRICS}]

tools/dist_test.sh also supports multi-node testing, but relies on PyTorch’s launch utility.

## Optional arguments:

- RESULT_FILE: Filename of the output results in pickle format. If not specified, the results will not be saved to a file.

• EVAL_METRICS: Items to be evaluated on the results. Allowed values depend on the dataset, e.g., proposal_fast, proposal, bbox, segm are available for COCO, mAP, recall for PASCAL VOC. Cityscapes could be evaluated by cityscapes as well as all COCO metrics.

• --show: If specified, detection results will be plotted on the images and shown in a new window. It is only applicable to single GPU testing and used for debugging and visualization. Please make sure that GUI is available in your environment. Otherwise, you may encounter an error like cannot connect to X server.

• --show-dir: If specified, detection results will be plotted on the images and saved to the specified directory. It is only applicable to single GPU testing and used for debugging and visualization. You do NOT need a GUI available in your environment for using this option.

• --show-score-thr: If specified, detections with scores below this threshold will be removed.

• --cfg-options: if specified, the key-value pair optionalcfg will be merged into config file

• --eval-options: if specified, the key-value pair optional eval cfg will be kwargs for dataset.evaluate() function, it's only for evaluation