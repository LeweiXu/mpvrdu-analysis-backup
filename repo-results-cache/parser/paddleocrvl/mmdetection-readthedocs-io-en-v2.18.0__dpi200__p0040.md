annotations=annotations,
categories=[{'id':0, 'name': 'balloon'}])
mmcv.dump(coco_format_json, out_file)

(continued from previous page)

Using the function above, users can successfully convert the annotation file into json format, then we can use CocoDataset to train and evaluate the model.

### 6.2 Prepare a config

The second step is to prepare a config thus the dataset could be successfully loaded. Assume that we want to use Mask R-CNN with FPN, the config to train the detector on balloon dataset is as below. Assume the config is under directory config/balloon/ and named as mask_rcnn_r50_caffe_fpn_mstrain-poly_1x_balloon.py, the config is as below.

# The new config inherits a base config to highlight the necessary modification
_base_ ='mask_rcnn/mask_rcnn_r50_caffe_fpn_mstrain-poly_1x_coco.py'
# We also need to change the num_classes in head to match the dataset's annotation
model = dict(
    roi_head=dict(
        bbox_head=dict(num_classes=1),
        mask_head=dict(num_classes=1)
    )
# Modify dataset related settings
dataset_type = 'COCODataset'
classes = ('balloon',)
data = dict(
    train=dict(
        img_prefix='balloon/train/',
        classes=classes,
        ann_file='balloon/train/annotation_coco.json'),
        val=dict(
            img_prefix='balloon/val/',
            classes=classes,
            ann_file='balloon/val/annotation_coco.json'
        ),
        test=dict(
            img_prefix='balloon/val/',
            classes=classes,
            ann_file='balloon/val/annotation_coco.json'
        )
)
# We can use the pre-trained Mask RCNN model to obtain higher performance
load_from = 'checkpoints/mask_rcnn_r50_caffe_fpn_mstrain-poly_3x_coco_bbox_mAP-0.408__→segm_mAP-0.37_20200504_163245-42aa3d00.pth'