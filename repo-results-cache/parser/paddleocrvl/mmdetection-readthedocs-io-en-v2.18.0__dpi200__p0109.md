• config : The path of a model config file.

• model : The path of an ONNX model file.

• --trt-file: The Path of output TensorRT engine file. If not specified, it will be set to tmp.trt.

• --input-img : The path of an input image for tracing and conversion. By default, it will be set to demo/demo.jpg.

• --shape: The height and width of model input. If not specified, it will be set to 400 600.

--min-shape: The minimum height and width of model input. If not specified, it will be set to the same as --shape.

--max-shape: The maximum height and width of model input. If not specified, it will be set to the same as --shape.

• --workspace-size : The required GPU workspace size in GiB to build TensorRT engine. If not specified, it will be set to 1 GiB.

• --show: Determines whether to show the outputs of the model. If not specified, it will be set to False.

• --verify: Determines whether to verify the correctness of models between ONNXRuntime and TensorRT. If not specified, it will be set to False.

• --verbose: Determines whether to print logging messages. It’s useful for debugging. If not specified, it will be set to False.

## Example:

python tools/deployment/onnx2tensorrt.py \
configs/retinanet/retinanet_r50_fpn_1x_coco.py \
checkpoints/retinanet_r50_fpn_1x_coco.onnx \
--trt-file checkpoints/retinanet_r50_fpn_1x_coco.trt \
--input-img demo/demo.jpg \
--shape 400 600 \
--show \
--verify \

### 16.2 How to evaluate the exported models

We prepare a tool tools/deployment/test.py to evaluate TensorRT models.

Please refer to the following links for more information.

• how-to-evaluate-the-exported-models

• results-and-models