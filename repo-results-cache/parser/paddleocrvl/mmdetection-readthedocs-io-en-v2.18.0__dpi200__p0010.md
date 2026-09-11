## INSTALLATION

### 2.1 Prepare environment

1. Create a conda virtual environment and activate it.

conda create -n openmmlab python=3.7 -y
conda activate openmmlab

2. Install PyTorch and torchvision following the official instructions, e.g.,

conda install pytorch torchvision -c pytorch

Note: Make sure that your compilation CUDA version and runtime CUDA version match. You can check the supported CUDA version for precompiled packages on the PyTorch website.

E.g.1 If you have CUDA 10.1 installed under /usr/local/cuda and would like to install PyTorch 1.5, you need to install the prebuilt PyTorch with CUDA 10.1.

conda install pytorch cudatoolkit=10.1 torchvision -c pytorch

E.g. 2 If you have CUDA 9.2 installed under /usr/local/cuda and would like to install PyTorch 1.3.1., you need to install the prebuilt PyTorch with CUDA 9.2.

conda install pytorch=1.3.1 cudatoolkit=9.2 torchvision=0.4.2 -c pytorch

If you build PyTorch from source instead of installing the prebuilt package, you can use more CUDA versions such as 9.0.

### 2.2 Install MMDetection

It is recommended to install MMDetection with MIM, which automatically handles the dependencies of OpenMMLab projects, including mmcv and other python packages.

pip install openmim
mim install mmdet

Or you can still install MMDetection manually:

1. Install mmcv-full.

pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/{cu_version}/
{torch_version}/index.html (continues on next page)

(continues on next page)