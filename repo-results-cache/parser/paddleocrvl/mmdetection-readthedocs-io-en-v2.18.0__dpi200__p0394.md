abstract forward(feats, rois, roi_scale_factor=None)

Defines the computation performed at every call.

Should be overridden by all subclasses.

Note: Although the recipe for forward pass needs to be defined within this function, one should call the Module instance afterwards instead of this since the former takes care of running the registered hooks while the latter silently ignores them.

## property num_inputs

Number of input feature maps.

Type int

roi_rescale(rois, scale_factor)

Scale RoI coordinates by scale factor.

Parameters

• rois (torch.Tensor) – RoI (Region of Interest), shape (n, 5)

• scale factor (float) – Scale factor that RoI will be multiplied by.

Returns Scaled RoI.

Return type torch.Tensor

class mmdet.models.roi_heads.BaseRoIHead(

    (bbox_roi_extractor=None,

    bbox_head=None,

    mask_roi_extractor=None,

    mask_head=None,

    shared_head=None,

    train_cfg=None,

    test_cfg=None,

    pretrained=None,

    init_cfg=None)

Base class for RoIHeads.

async async_simple_test(x, proposal_list, img_metas, proposals=None, rescale=False, **kwargs)

Asynchronized test function.

## aug_test(x, proposal_list, img_metas, rescale=False, **kwargs)

Test with augmentations.

If rescale is False, then returned bboxes and masks will fit the scale of imgs $$ 0 $$ .

abstract forward_train(x, img_meta, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None, **kwargs)

Forward function during training.

## abstract init_assigner_sampler()

Initialize assigner and sampler.

## abstract init_bbox_head()

Initialize bbox_head

## abstract init_mask_head()

Initialize mask_head

simple_test(x, proposal_list, img_meta, proposals=None, rescale=False, **kwargs)

Test without augmentation.

## property with_bbox

whether the RoI head contains a  $ bbox\_head $

Type bool