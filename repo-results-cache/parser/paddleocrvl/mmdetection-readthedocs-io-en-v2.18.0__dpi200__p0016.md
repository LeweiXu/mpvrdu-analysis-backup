# BENCHMARK AND MODEL ZOO

### 4.1 Mirror sites

We only use aliyun to maintain the model zoo since MMDetection V2.0. The model zoo of V1.x has been deprecated.

### 4.2 Common settings

• All models were trained on coco_2017_train, and tested on the coco_2017_val.

• We use distributed training.

• All pytorch-style pretrained backbones on ImageNet are from PyTorch model zoo, caffe-style pretrained backbones are converted from the newly released model from detectron2.

• For fair comparison with other codebases, we report the GPU memory as the maximum value of torch.cuda.max_memory_allocated() for all 8 GPUs. Note that this value is usually less than what nvidia-smi shows.

• We report the inference time as the total time of network forwarding and post-processing, excluding the data loading time. Results are obtained with the script benchmark.py which computes the average time on 2000 images.

### 4.3 ImageNet Pretrained Models

It is common to initialize from backbone models pre-trained on ImageNet classification task. All pre-trained model links can be found at open_mmlab. According to img_norm_cfg and source of weight, we can divide all the ImageNet pre-trained model weights into some cases:

• TorchVision: Corresponding to torchvision weight, including ResNet50, ResNet101. The img_norm_cfg is dict(mean=[123.675, 116.28, 103.53], std=[58.395, 57.12, 57.375], to_rgb=True).

• Pycls: Corresponding to pycls weight, including RegNetX. The img_norm_cfg is dict( mean=[103.530, 116.280, 123.675], std=[57.375, 57.12, 58.395], to_rgb=False).

• MSRA styles: Corresponding to MSRA weights, including ResNet50_Caffe and ResNet101_Caffe. The img_norm_cfg is dict(mean=[103.530, 116.280, 123.675], std=[1.0, 1.0, 1.0], to_rgb=False).

• Caffe2 styles: Currently only contains ResNext101_32x8d. The img_norm_cfg is dict(mean=[103.530, 116.280, 123.675], std=[57.375, 57.120, 58.395], to_rgb=False).