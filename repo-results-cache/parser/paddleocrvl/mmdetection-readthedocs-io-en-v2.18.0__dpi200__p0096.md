#### 13.3.3 Tweaking loss weight (step 5)

The loss weight here is a scalar which controls the weight of different losses in multi-task learning, e.g. classification loss and regression loss. Say if we want to change to loss weight of classification loss to be 0.5, we can specify it in the config as follows:

loss_cls=dict(
  type='FocalLoss',
  use_sigmoid=True,
  gamma=2.0,
  alpha=0.25,
  loss_weight=0.5)

### 13.4 Weighting loss (step 3)

Weighting loss means we re-weight the loss element-wisely. To be more specific, we multiply the loss tensor with a weight tensor which has the same shape. As a result, different entries of the loss can be scaled differently, and so called element-wisely. The loss weight varies across different models and highly context related, but overall there are two kinds of loss weights, label_weights for classification loss and bbox_weights for bbox regression loss. You can find them in the get_target method of the corresponding head. Here we take ATSSHead as an example, which inherits AnchorHead but overwrite its get_targets method which yields different label_weights and bbox_weights.

class ATSSHead(AnchorHead):
def get_targets(self,
                      anchor_list,
                      valid_flag_list,
                      gt_bboxes_list,
                      img_metas,
                      gt_bboxes_ignore_list=None,
                      gt_labels_list=None,
                      label_channels=1,
                      unmap_outputs=True):