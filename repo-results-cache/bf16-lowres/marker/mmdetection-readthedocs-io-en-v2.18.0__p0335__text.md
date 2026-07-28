```
class mmdet.models.dense_heads.DecoupledSOLOHead(*args, init_cfg=[{'type': 'Normal', 'layer': 'Conv2d',
                                                            'std': 0.01}, {'type': 'Normal', 'std': 0.01, 'bias_prob':
                                                            0.01, 'override': {'name': 'conv_mask_list_x'}},
                                                            {'type': 'Normal', 'std': 0.01, 'bias_prob': 0.01,
                                                            'override': {'name': 'conv_mask_list_y'}}, {'type':
                                                            'Normal', 'std': 0.01, 'bias_prob': 0.01, 'override':
                                                            {'name': 'conv_cls'}}], **kwargs)
```

Decoupled SOLO mask head used in **`**SOLO: Segmenting Objects by Locations.

[<https://arxiv.org/abs/1912.04488>](https://arxiv.org/abs/1912.04488)`\_

**Parameters** init\_cfg (dict or list[dict], optional) – Initialization config dict.

### forward(*feats*)

Defines the computation performed at every call.

Should be overridden by all subclasses.

**Note:** Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

```
get_results(mlvl_mask_preds_x, mlvl_mask_preds_y, mlvl_cls_scores, img_metas, rescale=None,
         **kwargs)
```

Get multi-image mask results.

### **Parameters**

- mlvl\_mask\_preds\_x (list[Tensor]) Multi-level mask prediction from x branch. Each element in the list has shape (batch\_size, num\_grids ,h ,w).
- mlvl\_mask\_preds\_y (list[Tensor]) Multi-level mask prediction from y branch. Each element in the list has shape (batch\_size, num\_grids ,h ,w).
- mlvl\_cls\_scores (list[Tensor]) Multi-level scores. Each element in the list has shape (batch\_size, num\_classes ,num\_grids ,num\_grids).
- img\_metas (list[dict]) Meta information of all images.

## **Returns**

Processed results of multiple images.Each InstanceData usually contains following keys.

- scores (Tensor): Classification scores, has shape (num\_instance,).
- labels (Tensor): Has shape (num\_instances,).
- masks (Tensor): Processed mask results, has shape (num\_instances, h, w).

### **Return type** list[InstanceData]

```
loss(mlvl_mask_preds_x, mlvl_mask_preds_y, mlvl_cls_preds, gt_labels, gt_masks, img_metas,
 gt_bboxes=None, **kwargs)
Calculate the loss of total batch.
```

# **Parameters**

- mlvl\_mask\_preds\_x (list[Tensor]) Multi-level mask prediction from x branch. Each element in the list has shape (batch\_size, num\_grids ,h ,w).
- mlvl\_mask\_preds\_x Multi-level mask prediction from y branch. Each element in the list has shape (batch\_size, num\_grids ,h ,w).