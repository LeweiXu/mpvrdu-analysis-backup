simple_test(x, proposal_list, img_metas, proposals=None, rescale=False)

Test without augmentation.

## Parameters

• x(tuple[Tensor]) – Features from upstream network. Each has shape (batch_size, c, h, w).

• proposal_list (list(Tensor)) – Proposals from rpn head. Each has shape (num_proposals, 5), last dimension 5 represent (x1, y1, x2, y2, score).

• img_metas (list[dict]) – Meta information of images.

• rescale (bool) – Whether to rescale the results to the original image. Default: True.

Returns When no mask branch, it is bbox results of each image and classes with type list[list[np.ndarray]]. The outer list corresponds to each image. The inner list corresponds to each class. When the model has mask branch, it contains bbox results and mask results. The outer list corresponds to each image, and first element of tuple is bbox results, second element is mask results.

Return type list[list[np.ndarray]] or list[tuple]

class mmdet.models.roi_heads.TridentRoIHead(num_branch, test_branch_idx, **kwargs)

Trident roi head.

## Parameters

• num_branch (int) – Number of branches in TridentNet.

• test_branch_idx(int) – In inference, all 3 branches will be used if test_branch_idx == -1, otherwise only branch with index test_branch_idx will be used.

aug_test_bboxes(feats, img_metas, proposal_list, rcnn_test_cfg)

Test det bboxes with test time augmentation.

merge_trident_bboxes(trident_det_bboxes, trident_det_labels)

Merge bbox predictions of each branch.

simple_test(x, proposal_list, img_metas, proposals=None, rescale=False)

Test without augmentation as follows:

1. Compute prediction bbox and label per branch.

2. Merge predictions of each branch according to scores of bboxes, i.e., bboxes with higher score are kept to give top-k prediction.

### 39.6 losses

class mmdet.models.losses.Accuracy(topk=(1), thresh=None)

forward(pred, target)

Forward function to calculate accuracy.

Parameters

• pred (torch.Tensor) – Prediction of models.

• target (torch.Tensor) – Target for each prediction.

Returns The accuracies under different topk criterions.