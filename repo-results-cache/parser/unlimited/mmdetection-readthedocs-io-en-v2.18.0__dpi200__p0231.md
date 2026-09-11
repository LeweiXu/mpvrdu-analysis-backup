MMDetection, Release 2.18.0
- max_num(int, optional) – if there are more than max_num bboxes after NMS, only top max_num will be kept. Default to -1.
- score_factors (Tensor, optional) – The factors multiplied to scores before applying NMS. Default to None.
- return_inds (bool, optional) – Whether return the indices of kept bboxes. Default to False.
Returns
(dets, labels, indices (optional)), tensors of shape (k, 5), (k), and (k). Dets are boxes with scores. Labels are 0-based.
Return type tuple
37.7 utils
class mmdet.core.utils.DistOptimizerHook(*args, **kwargs)
Deprecated optimizer hook for distributed training.
mmdet.core.utils.all_reduce_dict(py_dict, op='sum', group=None, to_float=True)
Apply all reduce function for python dict object.
The code is modified from https://github.com/Megvii-BaseDetection/YOLOX/blob/main/yolox/utils/allreduce_norm.py.
NOTE: make sure that py_dict in different ranks has the same keys and the values should be in the same shape.
Parameters
- py_dict (dict) – Dict to be applied all reduce op.
- op (str) – Operator, could be ‘sum’ or ‘mean’. Default: ‘sum’
- group (torch.distributed.group, optional) – Distributed group, Default: None.
- to_float (bool) – Whether to convert all values of dict to float. Default: True.
Returns reduced python dict object.
Return type OrderedDict
mmdet.core.utils.allreduce_grads(params, coalesce=True, bucket_size_mb=-1)
Allreduce gradients.
Parameters
- params (list[torch.Parameters]) – List of parameters of a model
- coalesce(bool, optional) – Whether allreduce parameters as a whole. Defaults to True.
- bucket_size_mb (int, optional) – Size of bucket, the unit is MB. Defaults to -1.
mmdet.core.utils.center_of_mass(mask, esp=1e-06)
Calculate the centroid coordinates of the mask.
Parameters
- mask (Tensor) – The mask to be calculated, shape (h, w).
- esp (float) – Avoid dividing by zero. Default: 1e-6.
Returns
the coordinates of the center point of the mask.
224
Chapter 37. mmdet.core