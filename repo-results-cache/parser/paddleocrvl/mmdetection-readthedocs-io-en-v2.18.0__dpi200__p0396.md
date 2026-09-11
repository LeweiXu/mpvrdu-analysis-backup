• bbox_roi_extractor(dict) – Config of box roi extractor.

• bbox_head (dict) – Config of box in box head.

init_mask_head(mask_roi_extractor, mask_head)

Initialize mask head and mask roi extractor.

## Parameters

• mask_roi_extractor (dict) – Config of mask roi extractor.

• mask_head (dict) – Config of mask in mask head.

simple_test(x, proposal_list, img_metas, rescale=False)

Test without augmentation.

## Parameters

• x(tuple[Tensor]) – Features from upstream network. Each has shape (batch_size, c, h, w).

• proposal_list (list(Tensor)) – Proposals from rpn head. Each has shape (num_proposals, 5), last dimension 5 represent (x1, y1, x2, y2, score).

• img_metas (list[dict]) – Meta information of images.

• rescale (bool) – Whether to rescale the results to the original image. Default: True.

Returns When no mask branch, it is bbox results of each image and classes with type list[list[np.ndarray]]. The outer list corresponds to each image. The inner list corresponds to each class. When the model has mask branch, it contains bbox results and mask results. The outer list corresponds to each image, and first element of tuple is bbox results, second element is mask results.

Return type list[list[np.ndarray]] or list[tuple]

class mmdet.models.roi_heads.CoarseMaskHead(num_convs=0, num_fcs=2, fc_out_channels=1024,

downsample_factor=2, init_cfg={'override': [{'name':

'fcs'}, {'type': 'Constant', 'val': 0.001, 'name': 'fc_logits]},

'type': 'Xavier'}, *arg, **kwarz)

Coarse mask head used in PointRend.

Compared with standard FCNMaskHead, CoarseMaskHead will downsample the input feature map instead of upsample it.

## Parameters

• num_convs (int) – Number of conv layers in the head. Default: 0.

• num_fcs (int) – Number of fc layers in the head. Default: 2.

• fc_out_channels (int) – Number of output channels of fc layer. Default: 1024.

• downsample_factor (int) – The factor that feature map is downsampled by. Default: 2.

• init_cfg(dict or list[dict], optional) – Initialization config dict.

## forward(x)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while