## Return type tuple[Tensor, Tensor]

mmdet.core.export.build_model_from_cfg(config_path, checkpoint_path, cfg_options=None)

Build a model from config and load the given checkpoint.

## Parameters

• config_path(str) – the OpenMMLab config for the model we want to export to ONNX

• checkpoint_path (str) – Path to the corresponding checkpoint

Returns the built model

Return type torch.nn.Module

mmdet.core.export.dynamic_clip_for_onnx(x1, y1, x2, y2, max_shape)

Clip boxes dynamically for onnx.

Since torch.clamp cannot have dynamic min and max, we scale the boxes by  $ 1/\max\_shape $ and clamp in the range  $ [0, 1] $.

## Parameters

• x1 (Tensor) – The x1 for bounding boxes.

• y1 (Tensor) – The y1 for bounding boxes.

• x2 (Tensor) – The x2 for bounding boxes.

• y2 (Tensor) – The y2 for bounding boxes.

• max_shape (Tensor or torch.Size) – The (H, W) of original image.

Returns The clipped x1, y1, x2, y2.

Return type tuple(Tensor)

mmdet.core.export.generate_inputs_and_wrap_model(config_path, checkpoint_path, input_config,

cfg_options=None)

Prepare sample input and wrap model for ONNX export.

The ONNX export API only accepts arguments, and all inputs should be torch.Tensor or corresponding types (such as tuple of tensor). So we should call this function before exporting. This function will:

1. generate corresponding inputs which are used to execute the model.

2. Wrap the model’s forward function.

For example, the MMDet models’ forward function has a parameter return_loss:bool. As we want to set it as False while export API supports neither bool type or kwargs. So we have to replace the forward method like model.forward = partial(model.forward, return_loss=False).

## Parameters

• config_path(str) – the OpenMMLab config for the model we want to export to ONNX

• checkpoint_path (str) – Path to the corresponding checkpoint

• input_config(dict) – the exactly data in this dict depends on the framework. For MMSeg, we can just declare the input shape, and generate the dummy data accordingly. However, for MMDet, we may pass the real img path, or the NMS will return None as there is no legal bbox.

## Returns