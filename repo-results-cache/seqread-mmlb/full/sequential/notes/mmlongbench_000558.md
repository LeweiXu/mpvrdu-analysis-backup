## Turn 1 — document page 275 (rank 1 of 20)

class mmdet.models.detectors.SOLO(backbone, neck=None, bbox_head=None, mask_head=None,
train_cfg=None, test_cfg=None, init_cfg=None, pretrained=None)
SOLO: Segmenting Objects by Locations

## Turn 2 — document page 337 (rank 2 of 20)

```markdown
- The current page defines `class mmdet.models.dense_heads.DecoupledSOLOLightHead(*args, ...)` as a "Decoupled Light SOLO mask head used in SOLO: Segmenting Objects by Locations".
- This class is explicitly linked to the SOLO paper.
- The class is located in `mmdet.models.dense_heads`, matching the target namespace in the question.
```

## Turn 3 — document page 336 (rank 3 of 20)

```markdown
class mmdet.models.dense_heads.DecoupledSOLOHead(*args, init_cfg=[...], **kwargs)
Decoupled SOLO mask head used in `SOLO: Segmenting Objects by Locations` (arXiv:1912.04488).
```

## Turn 4 — document page 368 (rank 4 of 20)

```markdown
class mmdet.models.dense_heads.SOLOHead(num_classes, in_channels, feat_channels=256,
stacked_convs=4, strides=(4, 8, 16, 32, 64), scale_ranges=((8, 32), (16, 64), (32, 128), (64, 256), (128, 512)), pos_scale=0.2, num_grids=[40, 36, 24, 16, 12], cls_down_index=0, loss_mask=None, loss_cls=None, norm_cfg={'num_groups': 32, 'requires_grad': True, 'type': 'GN'}, train_cfg=None, test_cfg=None, init_cfg=['['type': 'Normal', 'layer': 'Conv2d', 'std': 0.01], {'type': 'Normal', 'std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_mask_list'}, {'type': 'Normal', 'std': 0.01, 'bias_prob': 0.01, 'override': {'name': 'conv_cls'}]}]
SOLO mask head used in `SOLO: Segmenting Objects by Locations.
<https://arxiv.org/abs/1912.04488>_
```

## Turn 5 — document page 466 (rank 5 of 20)

| Class Name | Module Path | Page |
| --- | --- | --- |
| SOLOHead | mmdet.models.dense_heads | 360 |

## Turn 6 — document page 459 (rank 6 of 20)

none
