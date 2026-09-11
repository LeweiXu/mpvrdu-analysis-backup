(model, tensor_data) wrapped model which can be called by model(*tensor_data) and a list of inputs which are used to execute the model while exporting.

## Return type tuple

mmdet.core.export.get_k_for_topk(k, size)

Get k of TopK for onnx exporting.

The K of TopK in TensorRT should not be a Tensor, while in ONNX Runtime it could be a Tensor. Due to dynamic shape feature, we have to decide whether to do TopK and what K it should be while exporting to ONNX.

If returned K is less than zero, it means we do not have to do TopK operation.

## Parameters

• k (int or Tensor) – The set k value for nms from config file.

• size (Tensor or torch.Size) – The number of elements of TopK’s input tensor

Returns (int or Tensor): The final K for TopK.

Return type tuple

mmdet.core.export.preprocess_example_input(input_config)

Prepare an example input image for generate_inputs_and_wrap_model.

Parameters input_config(dict) – customized config describing the example input.

Returns (one_img, one_meta), tensor of the example input image and meta information for the example input image.

Return type tuple

## Examples

>>> from mmdet.core.export import preprocess_example_input
>>> input_config = {
>>>     'input_shape': (1, 3, 224, 224),
>>>     'input_path': 'demo/demo.jpg',
>>>     'normalize_cfg': {
>>>        'mean': (123.675, 116.28, 103.53),
>>>        'std': (58.395, 57.12, 57.375)
>>>     }
>>> }
>>> one_img, one_meta = preprocess_example_input(input_config)
>>> print(one_img.shape)
torch.Size([1, 3, 224, 224])
>>> print(one_meta)
{'img_shape': (224, 224, 3),
'ori_shape': (224, 224, 3),
'pad_shape': (224, 224, 3),
'filename': "<demo>.png",
'scale_factor': 1.0,
'flip': False}