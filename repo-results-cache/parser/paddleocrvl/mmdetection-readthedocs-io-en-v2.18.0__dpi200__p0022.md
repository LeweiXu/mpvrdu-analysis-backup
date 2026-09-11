#### 4.4.49 PVT

Please refer to PVT for details.

#### 4.4.50 SOLO

Please refer to SOLO for details.

#### 4.4.51 Querylnst

Please refer to QueryInst for details.

#### 4.4.52 Other datasets

We also benchmark some methods on PASCAL VOC, Cityscapes and WIDER FACE.

#### 4.4.53 Pre-trained Models

We also train Faster R-CNN and Mask R-CNN using ResNet-50 and RegNetX-3.2G with multi-scale training and longer schedules. These models serve as strong pre-trained models for downstream tasks for convenience.

### 4.5 Speed benchmark

#### 4.5.1 Training Speed benchmark

We provide analyze_logs.py to get an average time of iteration in training. You can find examples in Log Analysis.

We compare the training speed of Mask R-CNN with some other popular frameworks (The data is copied from detectron2). For mmdetection, we benchmark with mask_rcnn_r50_caffe_fpn_poly_1x_coco_v1.py, which should have the same setting with mask_rcnn_R_50_FPN_noaug_1x.yaml of detectron2. We also provide the checkpoint and training log for reference. The throughput is computed as the average throughput in iterations 100-500 to skip GPU warmup time.

#### 4.5.2 Inference Speed Benchmark

We provide benchmark.py to benchmark the inference latency. The script benchmarks the model with 2000 images and calculates the average time ignoring first 5 times. You can change the output log interval (defaults: 50) by setting LOG-INTERVAL.

python tools/benchmark.py ${CONFIG} ${CHECKPOINT} [--log-interval $[LOG-INTERVAL]] [--fuse-conv-bn]

The latency of all models in our model zoo is benchmarked without setting fuse-conv-bn, you can get a lower latency by setting it.