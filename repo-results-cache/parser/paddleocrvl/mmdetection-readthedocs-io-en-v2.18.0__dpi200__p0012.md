### 2.3 Install without GPU support

MMDetection can be built for CPU only environment (where CUDA isn’t available).

In CPU mode you can run the demo/webcam_demo.py for example. However some functionality is gone in this mode:

• Deformable Convolution

• Modulated Deformable Convolution

• ROI pooling

• Deformable ROI pooling

• CARAFE: Content-Aware ReAssembly of FEatures

• SyncBatchNorm

• CrissCrossAttention: Criss-Cross Attention

• MaskedConv2d

• Temporal Interlace Shift

• nms_cuda

• sigmoid focal loss cuda

• bbox overlaps

If you try to run inference with a model containing above ops, an error will be raised. The following table lists affected algorithms.

Notice: MMDetection does not support training with CPU for now.

### 2.4 Another option: Docker Image

We provide a Dockerfile to build an image. Ensure that you are using docker version >=19.03.

# build an image with PyTorch 1.6, CUDA 10.1
docker build -t mmdetection docker/

Run it with

docker run --gpus all --shm-size=8g -it -v {DATA_DIR}:/mmdetection/data mmdetection

### 2.5 A from-scratch setup script

Assuming that you already have CUDA 10.1 installed, here is a full script for setting up MMDetection with conda.

conda create -n openmmlab python=3.7 -y
conda activate openmmlab
conda install pytorch==1.6.0 torchvision==0.7.0 cudatoolkit=10.1 -c pytorch -y
# install the latest mmcv
pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu101/torch1.6.0/index.html (continues on next page)