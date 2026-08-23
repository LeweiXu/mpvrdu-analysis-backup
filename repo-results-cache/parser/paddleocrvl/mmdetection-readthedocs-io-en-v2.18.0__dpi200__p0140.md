## CONVENTIONS

Please check the following conventions if you would like to modify MMDetection as your own project.

### 29.1 Loss

In MMDetection, a dict containing losses and metrics will be returned by model(**data).

For example, in bbox head,

class BBoxHead(nn.Module):
    def loss(self,...):
        losses = dict()
        # classification loss
        losses['loss_cls'] = self.loss_cls(...)
        # classification accuracy
        losses['acc'] = accuracy(...)
        # bbox regression loss
        losses['loss_bbox'] = self.loss_bbox(...)
        return losses

bbox_head.loss() will be called during model forward. The returned dict contains 'loss_bbox', 'loss_cls', 'acc'. Only 'loss_bbox', 'loss_cls' will be used during back propagation, 'acc' will only be used as a metric to monitor training process.

By default, only values whose keys contain 'loss' will be back propagated. This behavior could be changed by modifying BaseDetector.train_step().

### 29.2 Empty Proposals

In MMDetection, we have added special handling and unit test for empty proposals of two-stage. We need to deal with the empty proposals of the entire batch and single image at the same time. For example, in CascadeRoIHead,

# simple_test method
...
# There is no proposal in the whole batch
if rois.shape[0] == 0:
    bbox_results = [[
        np.zeros((0, 5), dtype=np.float32)
]

(continues on next page)