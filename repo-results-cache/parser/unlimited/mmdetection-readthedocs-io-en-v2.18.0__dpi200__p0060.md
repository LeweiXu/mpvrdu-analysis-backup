MMDetection, Release 2.18.0
multiscale_mode="value", (continued from previous page)
keep_ratio=True),
dict(type="RandomFlip", flip_ratio=0.5),
dict(type="Normalize", "img_norm_cfg),
dict(type="Pad", size.divisor=32),
dict(type="DefaultFormaBundle"),
dict(type="Collect", keys=['img', 'gt_bboxes', 'gt_labels', 'gt_masks']), test_pipeline = [
    dict(type="LoadImageFromFile"),
    dict(
    type="MultiScaleFlipAug",
    img_scale=(1333, 800),
    flipFalse,
    transform=(
    dict(type="Resize", keep_ratio=True),
    dict(type="RandomFlip"),
    dict(type="Normalize", "img_norm_cfg"),
    dict(type="Pad", size.divisor=32),
    dict(type="ImageToTensor", keys=['img'])
    dict(type="Collect", keys=['img']),
    ])
data = dict(
    train_dict(pipeline_train_pipeline),
    val_dict(cipeline_test_pipeline),
    test_dict(pipeline_test_pipeline))
We first define the new train_pipeline/test_pipeline and pass them into data.
Similarly, if we would like to switch from SyncNB to BN or MYSyncBN, we need to substitute every norm_cfg in the config.
_base_ = ./mask_rcnn_r50_fgm_1s_coco.py'
norm_cfg = dict(type='BN', requires_grad=True)
model = dict(
    backbone-dict(norm_cfg-norm_cfg),
    neck-dict(norm_cfg-norm_cfg),
    ...)
8.6. FAQ
53