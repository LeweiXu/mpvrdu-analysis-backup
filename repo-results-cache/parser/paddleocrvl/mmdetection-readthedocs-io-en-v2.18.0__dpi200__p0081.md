norm_cfg=dict(type='BN'),
**kwargs):
kwargs.setdefault('with_avg_pool', True)
super(DoubleConvFCBBoxHead, self).__init__(**kwargs)
def forward(self, x_cls, x_reg):

(continued from previous page)

Second, implement a new RoI Head if it is necessary. We plan to inherit the new DoubleHeadRoIHead from StandardRoIHead. We can find that a StandardRoIHead already implements the following functions.

import torch

from mmdet.core import bbox2result, bbox2roi, build_assigner, build_sampler
from..builder import HEADS, build_head, build_roi_extractor
from.base_roi_head import BaseRoIHead
from.test_mixins import BBoxTestMixin, MaskTestMixin

@HEADS.register_module()
class StandardRoIHead(BaseRoIHead, BBoxTestMixin, MaskTestMixin):
    """Simplest base roi head including one bbox head and one mask head.
    """
    def init_assigner_sampler(self):
        def init_bbox_head(self, bbox_roi_extractor, bbox_head):
            def init_mask_head(self, mask_roi_extractor, mask_head):
                def forward_dummy(self, x, proposals):
                    def forward_train(self, x, img_metas, proposal_list, gt_bboxes, gt_labels, gt_bboxes_ignore=None, gt_masks=None):
                    def _bbox_forward(self, x, rois):
                        def _bbox_forward_train(self, x, sampling_results, gt_bboxes, gt_labels, img_metas):
                            def _mask_forward_train(self, x, sampling_results, bbox_feats, gt_masks, img_metas):
                                def _mask_forward(self, x, rois=None, pos_inds=None, bbox_feats=None):

(continues on next page)