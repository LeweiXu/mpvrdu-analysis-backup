### 14.5 Use pre-trained model

To use the pre-trained model, the new config add the link of pre-trained models in the load_from. The users might need to download the model weights before training to avoid the download time during training.

load_from = 'https://download.openmmlab.com/mmdetection/v2.0/mask_rcnn/mask_rcnn_r50_caffe_fpn_mstrain-poly_3x_coco/mask_rcnn_r50_caffe_fpn_mstrain-poly_3x_coco_bbox_mAP-0.408__segm_mAP-0.37_20200504_163245-42aa3d00.pth' # noqa