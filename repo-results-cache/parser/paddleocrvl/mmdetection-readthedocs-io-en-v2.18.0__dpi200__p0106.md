• Though supported, it is not recommended to use batch inference in onnxruntime for DETR, because there is huge performance gap between ONNX and torch model (e.g. 33.5 vs 39.9 mAP on COCO for onnxruntime and torch respectively, with a batch size 2). The main reason for the gap is that these are non-negligible effects on the predicted regressions during batch inference for ONNX, since the predicted coordinates are normalized by img_shape (without padding) and should be converted to absolute format, but img_shape is not dynamically traceable thus the padded img_shape_for_onnx is used.

• Currently only single-scale evaluation is supported with ONNX Runtime, also mmcv::SoftNonMaxSuppression is only supported for single image by now.

### 15.4 The Parameters of Non-Maximum Suppression in ONNX Export

In the process of exporting the ONNX model, we set some parameters for the NMS op to control the number of output bounding boxes. The following will introduce the parameter setting of the NMS op in the supported models. You can set these parameters through --cfg-options.

• nms_pre: The number of boxes before NMS. The default setting is 1000.

• deploy_nms_pre: The number of boxes before NMS when exporting to ONNX model. The default setting is 0.

• max_per_img: The number of boxes to be kept after NMS. The default setting is 100.

• max_output_boxes_per_class: Maximum number of output boxes per class of NMS. The default setting is 200.

### 15.5 Reminders

• When the input model has custom op such as RoIAlign and if you want to verify the exported ONNX model, you may have to build mmcv with ONNXRuntime from source.

• mmcv.onnx.simplify feature is based on onnx-simplifier. If you want to try it, please refer to onnx in mmcv and onnxruntime op in mmcv for more information.

• If you meet any problem with the listed models above, please create an issue and it would be taken care of soon. For models not included in the list, please try to dig a little deeper and debug a little bit more and hopefully solve them by yourself.

• Because this feature is experimental and may change fast, please always try with the latest mmcv and mmdetection.

### 15.6 FAQs

• None