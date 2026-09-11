(continued from previous page)

Please replace  $ \{cu\_version\} $ and  $ \{torch\_version\} $ in the url to your desired one. For example, to install the latest mmcv-full with CUDA 11.0 and PyTorch 1.7.0, use the following command:

pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu110/torch1.7.0/→index.html

See here for different versions of MMCV compatible to different PyTorch and CUDA versions.

Optionally you can compile mmcv from source if you need to develop both mmcv and mmdet. Refer to the guide for details.

### 2. Install MMDetection

You can simply install mmdetection with the following command:

pip install mmdet

or clone the repository and then install it:

git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -r requirements/build.txt
pip install -v -e. # or "python setup.py develop"

3. Install extra dependencies for Instaboost, Panoptic Segmentation, LVIS dataset, or Albumentations.

# for instaboost
pip install instaboostfast
# for panoptic segmentation
pip install git+https://github.com/cocodataset/panopticapi.git
# for LVIS dataset
pip install git+https://github.com/lvis-dataset/lvis-api.git
# for albumentations
pip install albumentations>=0.3.2 --no-binary imgaug,albumentations

## Note:

a. When specifying -e or develop, MMDetection is installed on dev mode, any local modifications made to the code will take effect without reinstallation.

b. If you would like to use opencv-python-headless instead of opencv-python, you can install it before installing MMCV.

c. Some dependencies are optional. Simply running pip install -v -e. will only install the minimum runtime requirements. To use optional dependencies like albumentations and imagecorruptions either install them manually with pip install -r requirements/optional.txt or specify desired extras when calling pip (e.g. pip install -v -e.[optional]). Valid keys for the extras field are: all, tests, build, and optional.

d. If you would like to use albumentations, we suggest using pip install albumentations>=0.3.2 --no-binary imgaug,albumentations. If you simply use pip install albumentations>=0.3.2, it will install opencv-python-headless simultaneously (even though you have already installed opencv-python). We should not allow opencv-python and opencv-python-headless installed at the same time, because it might cause unexpected issues. Please refer to official documentation for more details.