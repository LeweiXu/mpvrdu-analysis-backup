## Return type tuple(list[Tensor])

## init_weights()

Initialize weights of the head.

In particular, we have special initialization for classified conv's and regression conv's bias

loss(cls_scores, bbox_preds, objectnesses, gt_bboxes, gt_labels, img_metas, gt_bboxes_ignore=None) Compute loss of the head.

## Parameters

• cls_scores (list[Tensor]) – Box scores for each scale level, each is a 4D-tensor, the channel number is num_points * num_classes.

• bbox_preds (list[Tensor]) – Box energies / deltas for each scale level, each is a 4D-tensor, the channel number is num_points * 4.

• objectnesses (list\[Tensor]) – objectness for each scale level, each is a 4D-tensor, the channel number is num_points * 1.

- gt_bboxes (list [Tensor]) – Ground truth bboxes for each image with shape (num_gts, 4) in [tl_x, tl_y, br_x, br_y] format.

• gt_labels (list[Tensor]) – class indices corresponding to each box

• img_metas (list[dict]) – Meta information of each image, e.g., image size, scaling factor, etc.

- gt_bboxes_ignore (None / list[Tensor]) – specify which bounding boxes can be ignored when computing the loss.

Returns A dictionary of loss components.

Return type dict[str, Tensor]

class mmdet.models.dense_heads.CascadeRPNHead(num_stages, stages, train_cfg, test_cfg, init_cfg=None) The CascadeRPNHead will predict more accurate region proposals, which is required for two-stage detectors (such as Fast/Faster R-CNN). CascadeRPN consists of a sequence of RPNStage to progressively improve the accuracy of the detected proposals.

More details can be found in https://arxiv.org/abs/1909.06720.

## Parameters

• num_stages (int) – number of CascadeRPN stages.

• stages (list[dict]) – list of config to build the stages.

• train_cfg (list[dict]) – list of config at training time each stage.

• test_cfg(dict) – config at testing time.

## aug_test_rpn(x, img_metas)

Augmented forward test function.

forward_train(x, img_metas, gt_bboxes, gt_labels=None, gt_bboxes_ignore=None, proposal_cfg=None)

Forward train function.

## get_bboxes()

get_bboxes() is implemented in StageCascadeRPNHead.

## loss()

loss() is implemented in StageCascadeRPNHead.