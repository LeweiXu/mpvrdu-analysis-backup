### 4.6 Comparison with Detectron2

We compare mmdetection with Detectron2 in terms of speed and performance. We use the commit id 185c27e(30/4/2020) of detectron. For fair comparison, we install and run both frameworks on the same machine.

#### 4.6.1 Hardware

• 8 NVIDIA Tesla V100 (32G) GPUs

• Intel(R) Xeon(R) Gold 6148 CPU @ 2.40GHz

#### 4.6.2 Software environment

• Python 3.7

• PyTorch 1.4

• CUDA 10.1

• CUDNN 7.6.03

• NCCL 2.4.08

#### 4.6.3 Performance

#### 4.6.4 Training Speed

The training speed is measured with s/iter. The lower, the better.

#### 4.6.5 Inference Speed

The inference speed is measured with fps (img/s) on a single GPU, the higher, the better. To be consistent with Detectron2, we report the pure inference speed (without the time of data loading). For Mask R-CNN, we exclude the time of RLE encoding in post-processing. We also include the officially reported speed in the parentheses, which is slightly higher than the results tested on our server due to differences of hardwares.

#### 4.6.6 Training memory