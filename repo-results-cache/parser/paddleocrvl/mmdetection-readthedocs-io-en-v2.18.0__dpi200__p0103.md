#### 15.1.2 Usage

python tools/deployment/pytorch2onnx.py \
${CONFIG_FILE} \
${CHECKPOINT_FILE} \
--output-file ${OUTPUT_FILE} \
--input-img ${INPUT_IMAGE_PATH} \
--shape ${IMAGE_SHAPE} \
--test-img ${TEST_IMAGE_PATH} \
--opset-version ${OPSET_VERSION} \
--cfg-options ${CFG_OPTIONS} \
--dynamic-export \
--show \
--verify \
--simplify \

#### 15.1.3 Description of all arguments

• config : The path of a model config file.

• checkpoint : The path of a model checkpoint file.

• --output-file: The path of output ONNX model. If not specified, it will be set to tmp.onnx.

• --input-img: The path of an input image for tracing and conversion. By default, it will be set to tests/data/color.jpg.

• --shape: The height and width of input tensor to the model. If not specified, it will be set to 800 1216.

• --test-img : The path of an image to verify the exported ONNX model. By default, it will be set to None, meaning it will use --input-img for verification.

• --opset-version: The opset version of ONNX. If not specified, it will be set to 11.

• --dynamic-export: Determines whether to export ONNX model with dynamic input and output shapes. If not specified, it will be set to False.

• --show: Determines whether to print the architecture of the exported model and whether to show detection outputs when --verify is set to True. If not specified, it will be set to False.

• --verify: Determines whether to verify the correctness of an exported model. If not specified, it will be set to False.

• --simplify: Determines whether to simplify the exported ONNX model. If not specified, it will be set to False.

• --cfg-options: Override some settings in the used config file, the key-value pair in xxx=yyyy format will be merged into config file.

• --skip-postprocess: Determines whether export model without post process. If not specified, it will be set to False. Notice: This is an experimental option. Only work for some single stage models. Users need to implement the post-process by themselves. We do not guarantee the correctness of the exported model.

Example:

python tools/deployment/pytorch2onnx.py \
configs/yolo/yolov3_d53_mstrain-608_273e_coco.py \
checkpoints/yolo/yolov3_d53_mstrain-608_273e_coco.pth \

(continues on next page)