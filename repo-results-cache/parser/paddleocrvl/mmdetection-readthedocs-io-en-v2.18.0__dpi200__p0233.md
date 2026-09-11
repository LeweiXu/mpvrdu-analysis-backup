### Return type np.ndarray

mmdet.core.utils.multi_apply(func, *args, **kwargs)

Apply function to a list of arguments.

Note: This function applies the func to multiple inputs and map the multiple outputs of the func into different list. Each list contains the same type of outputs corresponding to different inputs.

Parameters func (Function) – A function that will be applied to a list of arguments

Returns A tuple containing multiple list, each list contains a kind of returned results by the function

Return type tuple(list)

mmdet.core.utils.reduce_mean(tensor)

“Obtain the mean of tensor on different GPUs.”

mmdet.core.utils.select_single_mlvl(mlvl_tensors, batch_id, detach=True)

Extract a multi-scale single image tensor from a multi-scale batch tensor based on batch index.

Note: The default value of detach is True, because the proposal gradient needs to be detached during the training of the two-stage model. E.g Cascade Mask R-CNN.

## Parameters

• mlvI_tensors (list [Tensor]) – Batch tensor for all scale levels, each is a 4D-tensor.

• batch_id (int) – Batch index.

• detach (bool) – Whether detach gradient. Default True.

Returns Multi-scale single image tensor.

Return type list[Tensor]

mmdet.core.utils.unmap(data, count, inds, fill=0)

Unmap a subset of item (data) back to the original set of items (of size count)