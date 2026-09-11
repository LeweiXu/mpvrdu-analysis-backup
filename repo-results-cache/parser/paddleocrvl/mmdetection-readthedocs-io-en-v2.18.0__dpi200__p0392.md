• bbox_pred (Tensor, optional) – Box energies / deltas for, has shape (B, num_boxes, num_classes * 4) when.

• img_shape (torch.Tensor) – Shape of image.

• (obj (cfg) – ConfigDict): test_cfg of Bbox Head. Default: None

## Returns

dets of shape [N, num_det, 5] and class labels of shape [N, num_det].

Return type tuple[Tensor, Tensor]

refine_bboxes(rois, labels, bbox_preds, pos_is_gts, img_metas)

Refine bboxes during training.

## Parameters

• rois (Tensor) – Shape (n*bs, 5), where n is image number per GPU, and bs is the sampled RoIs per image. The first column is the image id and the next 4 columns are x1, y1, x2, y2.

• labels (Tensor) – Shape (n*bs, ).

• bbox_preds (Tensor) – Shape (n*bs, 4) or (n*bs, 4*#class).

• pos_is_gts (list [Tensor]) – Flags indicating if each positive bbox is a gt bbox.

• img_metas (list[dict]) – Meta info of each image.

Returns Refined bboxes of each image in a mini-batch.

Return type list[Tensor]

## Example

>>> # xdoctest: +REQUIRED(module:kwarray)
>>> import kwarray
>>> import numpy as np
>>> from mmdet.core.bbox.demodata import random_boxes
>>> self = BBoxHead(reg_class_agnostic=True)
>>> n_roi = 2
>>> n_img = 4
>>> scale = 512
>>> rng = np.random.RandomState(0)
>>> img_metas = [{'img_shape': (scale, scale)} for _ in range(n_img)]
>>> # Create rois in the expected format
>>> roi_boxes = random_boxes(n_roi, scale=scale, rng=rng)
>>> img_ids = torch.randint(0, n_img, (n_roi,))
>>> img_ids = img_ids.float()
>>> rois = torch.cat([img_ids[:, None], roi_boxes], dim=1)
>>> # Create other args
>>> labels = torch.randint(0, 2, (n_roi,)).long()
>>> bbox_preds = random_boxes(n_roi, scale=scale, rng=rng)
>>> # For each image, pretend random positive boxes are gts
>>> is_label_pos = (labels.numpy() > 0).astype(np.int)
>>> lbl_per_img = kwarray.group_items(is_label_pos,
                                        img_ids.numpy())
>>> pos_per_img = [sum(lbl_per_img.get(gid, []))

(continues on next page)