### 6.3 Train a new model

To train a model with the new config, you can simply run

python tools/train.py config/balloon/mask_rcnn_r50_caffe_fpn_mstrain-poly_1x_balloon.py

For more detailed usages, please refer to the Case 1.

### 6.4 Test and inference

To test the trained model, you can simply run

python tools/test.py config/balloon/mask_rcnn_r50_caffe_fpn_mstrain-poly_1x_balloon.py work_dir/mask_rcnn_r50_caffe_fpn_mstrain-poly_1x_balloon.py/latest.pth --eval bbox segm

For more detailed usages, please refer to the Case 1.