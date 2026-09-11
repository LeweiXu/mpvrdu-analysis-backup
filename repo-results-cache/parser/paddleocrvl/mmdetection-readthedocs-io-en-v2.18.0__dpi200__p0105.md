#### 15.2.3 Description of all arguments

• config: The path of a model config file.

• model: The path of an input model file.

• --out: The path of output result file in pickle format.

• --backend: Backend for input model to run and should be onnxruntime or tensorrt.

• --format-only : Format the output results without perform evaluation. It is useful when you want to format the result to a specific format and submit it to the test server. If not specified, it will be set to False.

--eval: Evaluation metrics, which depends on the dataset, e.g., “bbox”, “segm”, “proposal” for COCO, and “mAP”, “recall” for PASCAL VOC.

• --show-dir: Directory where painted images will be saved

• --show-score-thr: Score threshold. Default is set to 0.3.

• --cfg-options: Override some settings in the used config file, the key-value pair in xxx=yyyy format will be merged into config file.

• --eval-options: Custom options for evaluation, the key-value pair in xxx=yyyy format will be kwargs for dataset.evaluate() function

Notes:

• If the deployed backend platform is TensorRT, please add environment variables before running the file:

export ONNX_BACKEND=MMCVTensorRT

• If you want to use the --dynamic-export parameter in the TensorRT backend to export ONNX, please remove the --simplify parameter, and vice versa.

#### 15.2.4 Results and Models

Notes:

• All ONNX models are evaluated with dynamic shape on coco dataset and images are preprocessed according to the original config file. Note that CornerNet is evaluated without test-time flip, since currently only single-scale evaluation is supported with ONNX Runtime.

• Mask AP of Mask R-CNN drops by 1% for ONNXRuntime. The main reason is that the predicted masks are directly interpolated to original image in PyTorch, while they are at first interpolated to the preprocessed input image of the model and then to original image in other backend.

### 15.3 List of supported models exportable to ONNX

The table below lists the models that are guaranteed to be exportable to ONNX and runnable in ONNX Runtime.

Notes:

• Minimum required version of MMCV is 1.3.5

• All models above are tested with Pytorch==1.6.0 and onnxruntime==1.5.1, except for CornerNet. For more details about the torch version when exporting CornerNet to ONNX, which involves mmcv::cummax, please refer to the Known Issues in mmcv.