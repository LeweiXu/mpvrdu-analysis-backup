# MMDET.MODELS

### 39.1 detectors

class mmdet.models.detectors.ATSS(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None, init_cfg=None)

Implementation of ATSS.

class mmdet.models.detectors.AutoAssign(backbone, neck, bbox_head, train_cfg=None, test_cfg=None, pretrained=None)

Implementation of AutoAssign: Differentiable Label Assignment for Dense Object Detection.

class mmdet.models.detectors.BaseDetector(init_cfg=None)

Base class for detectors.

abstract aug_test(imgs, img_metas, **kwargs)

Test function with test time augmentation.

abstract extract_feat(imgs)

Extract features from images.

extract_feats(imgs)

Extract features from multiple images.

Parameters imgs (list[torch.Tensor]) – A list of images. The images are augmented from the same image but in different ways.

Returns Features of different images

Return type list[torch.Tensor]

forward(img, img_metas, return_loss=True, **kwargs)

Calls either forward_train() or forward_test() depending on whether return_loss is True.

Note this setting will change the expected inputs. When return_loss=True, img and img_meta are single-nested (i.e. Tensor and List[dict]), and when return_loss=False, img and img_meta should be double nested (i.e. List[Tensor], List[List[dict]]), with the outer list indicating test time augmentations.

forward_test(imgs, img_metas, **kwargs)

## Parameters

• imgs (List\[Tensor]) – the outer list indicates test-time augmentations and inner Tensor should have a shape NxCxHxW, which contains all images in the batch.

• img_metas (List[List[dict]]) – the outer list indicates test-time augs (multiscale, flip, etc.) and the inner list indicates images in a batch.