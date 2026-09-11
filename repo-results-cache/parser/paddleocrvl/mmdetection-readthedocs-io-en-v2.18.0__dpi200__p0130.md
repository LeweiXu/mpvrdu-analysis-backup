## MODEL CONVERSION

### 24.1 MMDetection model to ONNX (experimental)

We provide a script to convert model to ONNX format. We also support comparing the output results between Pytorch and ONNX model for verification.

python tools/deployment/pytorch2onnx.py ${CONFIG_FILE} ${CHECKPOINT_FILE} --output_file ${ONNX_FILE} [--shape ${INPUT_SHAPE} --verify]

Note: This tool is still experimental. Some customized operators are not supported for now. For a detailed description of the usage and the list of supported models, please refer to pytorch2onnx.

##### 24.2 MMDetection 1.x model to MMDetection 2.x

tools/model_converters/upgrade_model_version.py upgrades a previous MMDetection checkpoint to the new version. Note that this script is not guaranteed to work as some breaking changes are introduced in the new version. It is recommended to directly use the new checkpoints.

python tools/model_converters/upgrade_model_version.py ${IN_FILE} ${OUT_FILE} [-h] [--num-classes NUM_CLASSES]

### 24.3 RegNet model to MMDetection

tools/model_converters/regnet2mmdet.py convert keys in pycls pretrained RegNet models to MMDetection style.

python tools/model_converters/regnet2mmdet.py ${SRC} ${DST} [-h]