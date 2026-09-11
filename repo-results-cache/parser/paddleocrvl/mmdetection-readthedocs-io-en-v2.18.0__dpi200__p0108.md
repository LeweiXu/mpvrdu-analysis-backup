# TUTORIAL 9: ONNX TO TENSORRT (EXPERIMENTAL)

• Tutorial 9: ONNX to TensorRT (Experimental)

– How to convert models from ONNX to TensorRT

 $ ^{*} $ Prerequisite

 $ ^{*} $ Usage

– How to evaluate the exported models

– List of supported models convertible to TensorRT

- Reminders

- FAQs

### 16.1 How to convert models from ONNX to TensorRT

#### 16.1.1 Prerequisite

1. Please refer to get started.md for installation of MMCV and MMDetection from source.

2. Please refer to ONNXRuntime in mmcv and TensorRT plugin in mmcv to install mmcv-full with ONNXRuntime custom ops and TensorRT plugins.

3. Use our tool pytorch2onnx to convert the model from PyTorch to ONNX.

#### 16.1.2 Usage

python tools/deployment/onnx2tensorrt.py \
${CONFIG} \
${MODEL} \
--trt-file ${TRT_FILE} \
--input-img ${INPUT_IMAGE_PATH} \
--shape ${INPUT_IMAGE_SHAPE} \
--min-shape ${MIN_IMAGE_SHAPE} \
--max-shape ${MAX_IMAGE_SHAPE} \
--workspace-size {WORKSPACE_SIZE} \
--show \
--verify \

Description of all arguments: